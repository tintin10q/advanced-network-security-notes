
VoLTE is a way to use a 4g data connection to make calls as opposed to the standard voice network to operate phone calls. 

Does anyone use this? Yes 253 operators in 113 countries. They use it for better call quality and LTE security features. 

However, there is an [[Mobile network standard|implementation]] fault which causes keystream reuse on the phone calls if you call soon enough after another call. Then you can do:

EncryptedCall1 + EncryptedCall2 + PlaintextCall2 = EncryptedCall1 + Keystream = PlaintextCall1

The idea is to have a wireless sniffer between the [[Mobile Network|UE]] and [[Mobile Network|eNodeB]] that records the first phone call. Then when it is done you make another call quickly. This call will use the same keystream as call1 so you can use it to decrypt call 1. 

To make VoLTE possible the [[Mobile Network|EPC]] has multiple things. 

- Home Subscriber Service (HSS) 
- Mobility Management Entity (MME)
- Serving Gateway (S-GW) 
- PDN Gateway (P-GW)

The calling can happen in multiple encodings. When different encodings are used the operators transcode. If you don't know the codec you can't decode your voice.

To reduce bandwidth they add **comfort noice** to safe data in periods where calling partner is silient.  Otherwise you have to transmit silence voice  data.
-  Comfort noise is generated through a seed. 
-  Seed is smaller, transmitted on lower frequency. 40bit over 160ms vs 477bit every 20ms
If this happens you can't really decrypt it. But you can also not use the plaintext of call two for that part to decrypt.

We record a call and reconstruct the keystream from a second call. 
These are the challenges:
- Performance: How codecs & compression affect traffic. 
- IMS: RTP bearer as main data transportation. 
- Security: VoLTE AKA and encryption through SRTP.

## Robust Header Compression (ROHC)
is a technique to save bits by removing redundancies in the headers of IP, TCP, UDP, and RTP packets. The compression saves bandwidth by removing redundancies from packet headers with the same connection endpoints.

See example here 
![[VoLTE compressed headers.png]]

The idea is that you send the first header with all header information included. The rest of the headers are stripped after that. The base station decides how to do the compression. 

Why is this relevant? Because if there is compression it is harder to reconstruct the data. 

## Radio Bearers 

You can only get service from the celluar network with a radio bearer. This you get if your phone leaves idle mode. This is a logical link of UE and eNodeB and defines tranmsion required.

**Signaling Radio Bearers** (SRBs) are used to carry control signaling in a cellular network. They are used to establish, maintain, and release connections between devices. SRBs are typically low-priority and have low data rates.

**Dedicated Radio Bearers** (DRBs) are used to carry user data in a cellular network. They are established once a connection has been established by the SRBs, and are used to transmit and receive user data. DRBs are typically high-priority and have higher data rates than SRBs.

DRB1 is internet, DRB2 is SIP (IMS), DRB3..32 is RTP

Why is this relavant. The bearer id is input for the keystream generation. The idea is that you connect using DRB1 and DRB2 and then the rest of the phone call goes with DRB3. The eNodeB decides on the bearer id. 

## IMS 

The voice stuff goes from the LTE network to the IMS IP media subsystem. This makes it possible that the calls happen. The transport goes with RTP (Real-time Transport Protocol) of audio. SIP is a build and control communication session protocol or Session initialization protocol. 

If they use SRTP you can't read things you need. 

----

## The PDCP encryption 

The encyption is done by the PDCP layer using multiple stream chipher algoritms. 

The keystream has these inputs:

![[VoLTE keystream generator.png]]

### Key stream generation 

- Key - Use plane key, established for each new radio connection. 
- Count PDCP sequence number + PDCP hyperframe number 
- Bearer Bearer identity 
- Direction Uplink or downlink (predictable)
- Length of the keystream block (does not influence the keystream generation because its fixed) 

- The lenght is the key stream block length and never changes. -
- The direction is basically uplink or downlink. Uplink is what the victim says. You just record both and you have the direction bit. 
- If you stay in the same radio session (don't do a new AKA) the key doesn't change. That is why you have to call fast. 
- Count The count is reset for each call....., 
- The bearer then, the bearer can be 3-32 but. If a new bearer id is used the keystream changes. If the same Bearer id is reused by the eNodeB when making another call the keystream is reused. it is an implementation flaw. This is what they did wrong! Always bearer 3.

![[VoLTE.png]]

So they drove around and checked which networks changed the bearer id for the keystream with the next call. 12/15 eNodeB reused the same bearer id. 

![[VoLTE-1.png]]

(PlanA + KeystreamA) + (PlanB + Keystream) = (Plain A + PlainB)
(Plain A + PlainB) + PlainB = PlainA

We have to however:
- Avoid comfort noice (in our call and take care of it in the other call)
- Anticipate the audio codec
- Only works without SRTP (see below) (usually not enabled)

## VoLTE AKA 

After the UE connects to the EPC with the [[Mutual Authentication and Key Agreement AKA]]. There has to be another AKA between the UE and the IMS to make calls. BECAUSE IMS IS OUTSIE OF EPC network!! All messages use the encryption already setup by the first AKA. 

![[VoLTE AKA.png]]

![[VoLTE 2.png]]


---- 

NOT ASKED BELOW at the exam!!!! SKIP:

1. Radio connection between UE and eNodeB
2. VoLTE traffic is treated as user plane data -> handled in Serving Gateway (S-GW
3. PDN Gateway (caries data) (exit of EPC to global interent)
4. IMS checks whether user is allowed to recieve server
5. Checks identity at HSS (Home subscriber server) 

We can see in this picture that the EPC consists out of some parts: 

The **S-GW** is responsible for routing data packets between the PDN and the device, and for managing the device's mobility within the network. Service gateway so here thigns come in that have to go to the IMS. 

The PDN Gateway (P GW) is responsible for routing things from the EPC to the ip network. 

The HSS (home subscriber subsystem) has all the identites of subscribers to the EPC. 

THE MME is responsible for the responses to the UE trough the EUTran

![[VoLTE aka2 diagram.png]]

----

The SIP (session initiated protocol) is used for the second AKA.

If the authentication has happened (and know which keys we are using)  we can switch from RTP (Real-time Transport Protocol) to Secure Real-time Transport Protocol. However, **using srtp is optional.** It is up to [[Mobile network standard|provider]] to turn this on. If SRTP is used  the attack doesn't work. 

How often does the second AKA happen? How often is SRTP used?