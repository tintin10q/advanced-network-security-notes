# Mobile Network

A  network has a phone, a base station, then a server with the code and then the internet. 

The phone connects to the base station
The base station provides the radio connection 
The core network provides the mangement
The internet is where you want to go 

In 4g this is all called:

| component| LTE Acronym | LTE component| 
| --------| -------| ---------|
|Phone | UE | user equipment |
|base station| eNodeB | evolved node b |
| core network | epc | evolved packet core | 
| internet | ... | ... |


The connection between UE and EnodeB is the air interface. 
This is the radio access network. Called **E-UTran** in 4g. 

lte = 4g



## The LTE Protocol stack

You have L1, L3, L3.

L3 = RRC, NAS
L2 = MAC, RLC, PDCP
L1 = PHy

The layers in L2 are basically the data link layer. 

![[Mobile Network stack.png]]

At the ue there is also the nas layer in the control plane.

 - **Nas** (Non Access Stratum) = Connects the UE inside the E-Utran with the MME (entrence into epc) outside the E_Utran, with a logical connection. This does Authentication of UE, security control, paging. It is a logical connection
- **RRC** (Radio Resource Control) = Manages the connection between the UE and the eNodeB. Connection establishemnt/release, radio bearer establishemtn, reconfiguration. This is the physical connection 
- **IP** (internet protocol)
- **PDCP**: Transport of data with ciphering and intergrity protection (RRC) and the transport of IP packets 
- **RLC**: Transport PDCP data in different modese (Acknowledged (AM), unacknowledged (um), transparent (TM))
- **MAC**: Logic la channels for RLC for multiplexing into the physical transmission scheduling of withing and betweeen UEs.
- **PHy**: transport the data actually (phisical layer) 

### User plane
The user plane is your data. What you want to connect to. This is a bit of a different stack at L3

### Control plane
The control plane is data needed to connect. Network data, what’s needed to manage the connection.

# Processors 
You have the **application processors** and the **baseband processors**. The baseband processor is what supports the mobile networks. The application processor runs the browser and the **baseband processor** takes over. At some point in the normal network stack the application processor hands over control to the baseband processor. This happens at the **network layer**. 

The baseband processor recives an ip packet from the application processor and encapsulates that in the pdcp layer. 

The L2 layer is the data link layer of the normal protocol 
