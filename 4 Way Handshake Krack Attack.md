
The krack attack is an implementation flaw attack where you force the AP to reinstall the key and reset the counter which causes a Nonce reuse.

The the [[Types of Wifi#Shared key|4 way handshake]] you got 4 messages. 

![[4 Way Handshake with data.png]]

- Every message also has an r value. This is a counter to protect against replay attacks. Each message, r is increased. The first message does not have a mic. The second message has a mic using the ANonce. At the end there is mutual authentication and you derive the session keys 
- PTK (Preshared transient key) -> TK, KCK, KEK from Preshared Master key PMK. 

Do not confuse ANonce with SNonce. ANonce is first and then Snonce. Then after the 4 way handshake the encryption uses a different Nonce **n**. This is a seperate counter that is increased after every transmission of encrypted data.

## The attack

You start by becoming a man in the middle between STA and AP selectify relaying messages. The idea is to go through all the messages but then block message 4 from the STA to the AP. 

But after the STA has send msg 4 it will have already installed the PTK and GTK.
Then because the AP never got msg4 it retransmit message 3. This the mitm lets through and causes the STA to resend message 4 however this time it is encrypted using the key and counter 1. 

Now you have the keystream for the first message that the STA will send because you have a known plaintext attack with the first MS4 and the second encrypted msg4. 

But because the STA got message 3 again from the AP it sends message 4 and reinstalls the PTK and GTK and resets the counter. These keys are the same and now the same keysteam is used that you got by xoring message 4 and encrypted message 4 and you can decrypt the first message that is send.   

![[4 Way Handshake Attack (Krack attack).png]]

![[4 Way Handshake Attack (Krack attack).png]]

![[4 Way Handshake Attack (Krack attack)2.png]]

![[4 Way Handshake Krack attack known plaintext.png]]

Turns out that in practice there are 2 scenarios:

### Scenario 1

The suplicant (STA) still accepts retransmitted msg3 in plaintext. In this case the MITM blocks the first encrypted message and retransmits message 3. 
This will cause STA to resend message 4 but encrypted (with different counter but same content) and reinstall the keys which resets the counter. Now MITM BLOCKS encrypted message 4 and sends plaintext message 4 captured earlier. This message 4 has the wrong counter but an implementation flaw says that AP should excapt any counter that has already been used in message 4. So now AP also installs keys. Now the first message from STA to AP will have the same keystream as the encrypted message 4. You can get the keystream by xoring with the plaintext that you have.

![[4 Way Handshake Krack Attack s1.png]]

You can also wait before you let through message 3 form AP to STA. While you wait AP will send encrypted messages. How long you wait with retransmitted message 3 in step 3 determines which counter is used in the Encrypted(message 4, r, mic) response from STA. This way you can get different parts of the keystream. This works because you have a message 4 in plaintext.

### Scenario 2

After the suplicant (STA) has installed the keys STA only accepts retransmitted MSG3 encrypted. This is more complicated because now you need an encrypted message 3 from the AP.
Luckily you can get one when a the 4-way handshake is initicated again. This happens every hour or so. The man in the middle can also try to force it by sending a rekey request to AP but it only works if MIC is not checked by AP. 

But if it is reiniciated there was already a connection and all the messages will be encrypted, also the handshake. This gives man in the middle the encrypted messages 3 from AP that they need. The mitm intercepts two or more messages and then sends them at the same time to STA. This causes a data race and some messages 4 are send by the STA with the old key and some message 4 are send by the sta with the new key. Then you can get the keystream with the original message 4 that you captured. 

## Impact 

The specification attack flaw works for every encryption algoritm that is used in WPA.  Reuse of nonce is always reuse of keystream and that allows decryption of one packet. 

There was also one version of andriod wpa supplicant that when the key was reinstalled, it was reinstalled it to all zero. This is an implementation flaw. 

With TKIP, the mic key can also be reocered given the plaintext and MIC, due to weak michel algorithm. This allows forging/ injecting frames from client. So don't use WPA only WPA2 or WPA3. 

The 802.1x is more protectected because there every connection has a unique PSK. 

## Formal Proof 

The 4 way handshake has been formally proven as secure. But the model did not include the key reinstallation. This shows limits of formal verification as it only covers pars of the specification and proofs may also be counter productive because once there is a formal proof researchers become less intrested in researching it. 

## Countermeasures 

Install key only ONCE in 4-way handshake. 
- Do not reinstall after recieving msg 3. 

Or do not reset nonces when reinstalling the current key.

### Krr∅∅k attack  (2020)

**Disassociation**: connection between client and AP is terminated (eg. when user turns off Wi-Fi , or due to signal interference)
**Reassociation**: reconnection after disassociation (eg. when client roams from one Wi-Fi AP to another)

The disassociation and association is goverend by special management frames. These are unuathenticated and unencrypted in WPA2. 

- Attacker can forge a mangement frame to trigger disassociation
- **Some WiFi chips set TK (key for data confidentiality and integrity) to all zero** oeps 
- Data frames still left in transmit buffer in chips are encrypted with all-zero key and transmitted, which can be easily decrypted.  

So this is an implementation flaw.