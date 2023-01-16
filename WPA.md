
WPA came after [[WEP]] and is RSN robust security network. Comes with:

- Data confidentiality and integrity 
	- WPA -> TKIP (Temporary key integrity protocol) 
		- just like WEP based on RC4 stream chipher
		- Adds integrity (MIC), key mixing and sequence number
	- WPA2 -> AES-CCMP instead of RC4, PN for relay protection 
	- WPA3 -> AES-GCMP instead of AES CCMP
- Integrity for management frames (BIP) 
- Authentication based on IEEE 802.1X or SAE 
- Key management

It is an addon to WEP. You still take the WEP steps for historic reasons but then and you do the [[Types of Wifi#Shared key|4-Way handshake]]. Optionally, if your enterprise you ALSO do 802.1x (here it is). This is mutual authentication using EAP (Extensible authentication protocol).

![[WPA protocol.png]]
\*web is now obsolete.

So we have personal and enterprise networks 

## WPA Personal  
This is a personal network. For WPA and WPA2 this uses Pre shared key (PSK) 4 way handshake and WPA3 has simultaneous authentication of equals (SAE). 

### PSK WPA & WPA2

![[WPA PSK.png]]

With the PSK 4 way handshake the PTK derived from PMK (pairwise master key), mac of STA and Snonce.  and then split in KCK (Key Confirmation Key): for generating MIC, KEK (Key Encryption Key): for encryption of keys and TK (Temporal Key): for data confidentiality and integrity

There is also the group keys GMK and GKT. The GTK is shared between al connected clients and access points. This is used for broadcast of multicaset traffic. 

### PSK Attack

The PSK is derived from a password. This is what you actually type in when you connect to the Wi-Fi. Then a key derivation function is used to get to the PSM. You can then do a brute force attack if you have mac address and SSID and Nonces which is doable to get. Then you can do a brute force.

Often however restaurants just share the PMK and then the attacker can just evedrop anyways.

So for that they introduced:

### Simultaneous Authentication of Equals (SAE)
Since WPA3 we use:

Improves security of PSK method when using a password 

- Password-authenticated key exchange method based on Diffie-Hellman 
- No notion of “Initiator” and “Responder” (or “Supplicant” and “Authenticator”); each side is able to initiate the protocol 
- SAE = [[Types of Wifi#Opportunisitc Wireless Encryption|OWE]] + password

Just for illustration: 

![[SEA.png]]

## WPA Enterprise  IEEE 802.1x

This is an Enterprise network and here you also use 802.1x to authenticate using a special authentication server before the 4 way handshake. This is an extra feature. This uses the Extensible Authentication protocol (EAP) over LAN (EAPOL). This way you can use another auth system then one password for WiFi Access. The IEEE 802.1x is used to get a PMK for the 4 way handshake later on. 
The PMK is actually derived from the authentication data. The STA knows because they entered in this data so they just derive the PMK from this and the authentication server also has to know and can then derive the PMK from the authentication data.  

What happens here is that the acutal authentication of input is done by another server that has to decide if its ok. Any method can be used here. So AP requests identity, STA responds. AP relays this to a server typically a RADIUS server. Then **mutual authentication happens between STA and Authentication server** and they generate a PMK. The the authentication server gives PMK to AP. 

The connection between AP and authentication server has to be secure!

![[WPA IEEE 802.1x.png]]

There are different ways to do the Authentication exchange. Here they are:

### EAP-TLS 

Mutual authentication between client and authentication server via TLS using certificates on both sides. This is hard to setup as all users need a keypair and certificate that the authentication server knows about.

![[WPA TLS.png]]

### EAP-TTLS 

Improves the hardness of setting up key pair. Basically now only the authentication server has a certificate. This is how to authentication server authenticates to STA (which the STA has to verify) but the STA uses some other method like username-password to authenticate to the server. 

Handshake phase (inner authentication) auth server auths to  STA and the data phase (inner authentication) STA auths to auth server.

#### Handshake phase (outher authentication)
-  STA authenticates auth server using server certificate. 
- Important to verify server certificate
- This creates a secure tunnel between STA and auth server

#### Data Phase (inner)
- Client is authenticated to the server (or mutual authentication) using arbitrary authtentication
- Uses the secure tunnel to send this PAP (Password authentication protocol) or MS-CHAPV2

### EAP-PEAP (protected extensible authentication protocol)

This is similar to EAP-TTLS but this provides protection layer of legacy EAP methods (inner authentication methods) in particular MS-CHAPv2.

TLS tunnel between client and authentication server – Typically only server authentication

Still important to check certificate. 


#### Example of this is EDU-ROAM. The AP 

You still have to say who you are to be redirected to the right authentication server but then the right authentication server will make a tunnel between STA and and authentication server. Which one is based on the email domain you give. So like s107212@ru.nl. This is then given to the AP and the AP forwards it to the authentication server. Then this makes a tunnel and you login and the PMK is established and you do the 4 way handshake with the AP. 

![[WPA EAP-PEAP.png]]

![[WPA eduroam.png]]

![[WPA eduroam 2.png]]

Some issues with eduroam are **privacy** because the identity of the client in outer authenitcation is send in plaintext because we need to know which server to connect to. Client should basically have like an anonomous identity and then ap knows who to reach for.

You have to check the certificate of the outer authentication!!!! Otherwise you got evil twin attack. People never check it. 

However if the outer authentication gets attack by an evil twin then you at least still have the inner authentication. But not really this is mostly just PAP -> send username password in plaintext or MSCHAPv2 -> Password also but could be cracked if weak password. So then someone knows your password if they have the outer authentication. 