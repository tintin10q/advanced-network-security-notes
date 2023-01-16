When a user connects to a server the target ip address allows fingerprinting.  You can protect this using encryption. 

You can still do **tracffic recording attacks** (tracking time of messages) and look at them using **wireshark** - record traffic and run **classification system** (WF) using earlier data. The recordings is called **packet capture** and in .pcap files. 

WF: Classification attack where pre-recorded data set is compared to attack trace.

In mobile networks a malicious eNodeB can record all the traffic. The user connects to it and oops.

If the eNodeB is bad it can track everything coming throug  the air interface (EUTrans).

You can also just record the traffic in the EUTrans with a sniffer.

![[Fingerprinting attack.png]]

## Meta data

The PDCP and MAC layers are the most intresting for the malicious eNodeB. In PDCP we get the data decrypted and in MAC we get the message identitifers. But you must first go through the pysical layer before you can do this. You have to know what metadata there is. This is unencrypted. 

![[Physical layer packet.png]]

You can also capture [[RNTI]]. Tempory identifiers. 

# PDCP packets  

The most intresting is the PDCP layer as it transport the control plane and user plane data and can apply features like header compression, ciphering, or integrity protection. This is the data we care about. 

## Summary Fingerprinting 

![[Fingerprinting attack summary.png]]

