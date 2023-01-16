Stands for Radio Network **Temporary** Identifier. They are used to differentiate between multiple connected UEs.

MAC sub-layer manages active radio connections. 
Every active connection has its own RNTI 
There are many different types of RNTI 


We got:

## TMSI
Temporary Mobile Subscriber Identity, randomly assigned temporary identity. For security reasons, the TMSI is a placeholder for the unique IMSI of a user. It can be updated after a certain time period.

## iMSi
International Mobile Subscriber Identity, uniquely identifies every mobile user. It is **not** the identifier of the SIM card, but still part of the profile.

The TMSI is used for security reasons! It can be reset if compromised. The IMSI cannot be reset.