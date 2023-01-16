
When a [[Mobile Network|UE]] connects to the [[Mobile Network]] an AKA happens. This is a mutual key agreement where both the service provider and UE authenticate eachother. It is a challenge response protocol. 

The protocol is based on symmetric key cryptography. The UE has a secret key on the sim card that the service provider also knows. Which is stored in the **hss** home subscriber service. 



![[Mutual Authentication and Key Agreement AKA.png]]

The eNodeB only does the communication. All important computations are done in the core network EPC evolved packet core. 

At some point the phone sends the idenitty to the MME and to the HSS home subscriber service (identity of customers) on EPC.  Based on that the server uses K to encrypt challenge C and Auth token into XRES (expected response). The auth token and nonce C are then send to the UE. The auth token authenticates the server to the UE and then UE makes response RES. If RES = XRES everything is ok. 

You can't really forge the auth token which makes man in the middle harder.

EPC and UE use AKA for mutal authentication after this all traffic is encrypted. 
