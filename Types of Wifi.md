There are different types of [[Wifi]] networks. 

## Open Wi-Fi networks 

These are public hotspots for free Wi-Fi. For instance in a train. Could use a pre shared key publicly displayed. There could be a website your linked to log in. 

### Authentication methods open Wi-Fi 

- Open system - no authentication 
- Shared Key - uses pre-shared key
- Opportunistic Wireless encryption (OWE) uses Diffie Hellman to obtain shared key

#### Open System

This is the basic system. The shared key and opportunistic wireless encryption build on this. 

There are 4 phases:

1. Discovery 
	- AP advertises presence to STA by transmitting beacon frames
	- STA can send *probe request*, AP will send back *probe response* (same as beacon response)
2. Open system authentication 
	- STA says to AP pls authenticate me pls
	- AP authenticates
3. Association
	- More parameters like what cipher, but this is quite empty here
4.  Data exchange 

![[Types of Wifi open wifi.png]]


#### Shared key 

Same discovery, open system authentication and association as open system but after association there is a **4 way handshake** this is like WiFi version of [[Mutual Authentication and Key Agreement AKA|AKA]] 

![[Types of Wifi Shared Key.png]]

The 4 way handshake looks like this:

The supplicant (STA) and Authenticator (AP) (Termology from 802.11) or (Termology from 802.11)?  have a preshared key this is called PMK (Pairwise master key).  

1. Authenticator sends suplicant ANonce + identity
2. Supplicant uses PMK and step 1 info to derive session key (PTK) pairwise Transient key, then sends back SNonce + identity and integrity check MIC message integrity check to AP. 
3. Authenticator (AP) checks the MIC and derives the same PTK. Then sends to supplicant ok we start using this PTK from now. 
4. Supplicant installs the PTK and sends ok I installed the key again with MIC

![[Types of Wifi 4wayhandshake.png]]

If the preshared key is known and publically shared an attacker can ofcourse evedrop on the ANonce to get the same PTK and even forge messages. 

If the attacker missed the handshake the attacker can just send deauthenticate to the STA and then the handshake will repeat. 

#### Opportunisitc Wireless Encryption 

Not part of the IEEE 802.11 but part of WPA3. 

Instead of doing a preshared key 4way handshake they do a diffie helman key exchange to obtain shared key. It uses eliptic curve or finite field crypto, mutlipe possible schemes. 

![[Types of Wifi df.png]]

This is still an open network! Everyone can connect!

###### Evil twin attack

Because its diffie helman you have to authenticate the public key of the AP. If you don't you are vulnerable to the evil **twin attack** = an active attack where adversary acts as man in the middle attack. 

![[Man in the middle attack OWE.png]]

Adversary is able to forge packets and inspect modify any data between AP' and AP.

You can actually hide the SSID in the beacon request and then you have to know it beforehand but this is security by obscurity and if it is written down you can find it. You can also evedrop on the STA when it actually makes the request with the SSID. 

##### Karma
A special case of the Evil twin attack is KARMA. Here in the probe requst from STA it includes list of SSID that STA connected to before already, the prevered network list (PNL). Then the attacker can just pick the SSID from the PNL.

You could try prevent some of this by only allowing certain mac to connect to STA or AP but you can spoof mac adress.

## Home networks 

Home networks are networks for peoples homes. Same techniques as open networks but this is a different specification from the Wi-Fi alliance. The idea is that you don't publicly advertise key. 

#### WPS

There is **push button** connect where you push a physical button on the AP, then you confirm by pressing virtual or physical button on STA and during a two minute probe period STA can connect. 
Sometimes for this you have to enter a **pin** but its only 4 numbers.  During the two miniutes everyone can connect.


