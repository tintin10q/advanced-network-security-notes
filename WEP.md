
WEP was the first version of IEEE 802.11. Pre-RSN (Robust security network) security’.

Introduced the discovery, authentication, association and data exchange phases. 
The authentication goes with preshared key. Its a simple scheme:

### WEP authentication 

This is not the 4 way handshake.

- STA sends authentication request 
- AP Send cleartext challenge
- STA encrypts with K
- AP checks if its right. No integrity protection. 

AP is not authenticated. There is no integrity at all. 

We got WEP-40,  40 bits + 24 bits IV = 64 bits seed.  
We got WEP-104,  104 bits + 24 bits IV  = 128 bits seed. 
The key is only 40 bits + 24 bits IV. 


![[WEP RC4 cipher.png]]

IV of 24 bits is not that much. If the keystream is repeated then you got a keystream reuse. 

RC4 is also broken because about 9000 IV lead to weak keys and you can recover the key. 
WEP also has no support for key mangement. The key has to be configured in it. 

Also in the authentication step. You can just snif the plaintext and ciphertext to get the keystream and then you can actually do every challenge ever......


