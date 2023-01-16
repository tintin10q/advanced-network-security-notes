
As we know in [[mobile generation#4g|4g]] there is no [[Security Goals#Integrity|integrity]] protection for the userplane in the [[Mobile Network|PCEP]] layer:

![[Data Redirection Attack.png]]


## Plaintext modification & Dns spoofing 

This means that we can modify ciphertexts and get away with it. If you know the ip of where someone was going you can modify the plaintext with a known plaintext attack. Great for modifing the ip for ip in dns requests:

Chipertext = keystream + ip
keystream = Chipertext + ip 

now replace the ip with the keystream which goes unnoticed because of lack of integrity protection. 

NewChpiertext = keystream  + badurl

![[known plaintext attack.png]]

Why do we know the plaintext? Because dns providers have standart ips. Most people use 8.8.8.8 for instanace. So you just xor with b"8.8.8.8" to get the keystream and the you xor again with your dns server ip: b"6.6.6.6". We can also just have a mask that does bitflips to turn 8.8.8.8 into 6.6.6.6 which we can do because its a stream cipher (AES-CTR) and not a block cipher. The mask has 1 in positions where you want to flip a bit.

## Man in the middle -> aLTEr attack


Alter attack. you alter it. 

We have a malicious [[Mobile Network|eNodeB]] in the middle that does the spoofing like this:

1. UE and eNodeB conduct AKA (authentication and key agreement).
2. UE sends a website request with url including desIP of the wanted dns server.
3. Malicious eNodeB captures request and replaces destIP with MALICIOUS dns server.
4. eNodeB sends traffic to epc.
5. Malicious DNs server responds with malicious ip for url.
6. On the way back eNodeB replaces srcIP of the dns server with the intended DNS.
7. UE now has spoofed response and sends website requests to malicious http server. 

It was not seen that the request was modified because no integrity protection.

