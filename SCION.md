
The [[BGP]] protocol has many problems. The SCION architecture has been probosed as an alternative. Designed to provide route control, failure isolation, and explicit trust for end-to-end communication.

SCION Introduces additional hierarchical layer by grouping ASes into isolation domains (ISDs)

Apperenlty 200x faster then [[BGP]].


![[SCION.png]]

Then the IDS is govered by trust root configuration (TRC). TRC defines roots of trust for PKI within ISD by specifing a version number and trusted public keys. 

- Path-based architecture where routing is based on Packet-Carried-Forwarding State (PCFS)
This is a special header that contains th AS level path from source to destination.
The idea is that senders already decide the whole path beforehand. 

You got the control plane for discovering paths and making those pathds available to end hosts and data plane where you got packet forwarding using provided paths.

## Control plane

This is componets within AS:

- Beaconing servers are responsible for beaconing process •
- Path servers store path segments 
- Certificate servers store cached copies of TRC and assist with validating path information (PCBs and path segments are signed ) 
- Border routers provide connectivity between ASes (ingress and egress interfaces) 
- Internal routers forward packets within AS

![[SCION Beaconing.png]]

### Intra ISD paths 

The idea is that there is a beaconing process for discovering paths within the same ISD. This is done by the core ASes. This is called path-segment construction beacons (PCBs) and they are send downstream to neighboring non-core AS. Non core AS recieves the PCB add their own identity and **hop field** to PCB protected with integrity check (MAC), signs the PCB and sends the PCB to other neighbors further down etc. This generates (ingress and egress interfaces)
Each AS then sends back to ISD core the (PCB) as path segments that they like and over which path they can be reached. Finally the ISD core knows how each AS can be reached and AS can also know how ISD core can be reached. 

This process is repeated every couple seconds. 

The hops are used to specify the map for forwarding by AS. This also has an exporation time. 

### Inter ISD paths

Inter-ISD beaconing process between core ASes also uses PCBs 
- follows flooding approach similar to BGP. 
But only between ISD cores? 

![[SCION inter isd paths.png]]

## Data plane

Now that we have all the paths we can do routing. This happens in the data plane. 

There are two steps. 
1. The sender does path lookup to obtain path segments to destination. 
2. The sender does a path combination by combining up to three paths 

- on-path with single up-segment (eg. A → E) 
- immediate combination of up- and down-segments (eg. B → D) 
- combination of up-, core-, and down-segment (eg. A → D) 
- peering shortcut by peer link (eg. A → B); 
- same peering link is announced in two path segments 
- AS shortcut (eg. B → C); up-segment and down-segment intersect at a non-core AS


![[SCION Path combination.png]]

These paths basically consist in the up segment (A->C) the core segment (C->D) and the down segment (D->E).

![[SCION path combination simple.png]]


The SCION packet contains AS-level path (with ingress and egress interfaces) to get from source to destination and also MAC. This requires key mangagement with border routers and becon servers. Only the ISD border routers have to decide on paths and so only border routers use the ingress and egress interfaces. This way intraAS can have its own adressing. Destination can respond to source by just inverting the path that is in the header or perform own path lookup. 

There is SCION control message protocol SCMP (literally an ancronyms in an acronyms...) for link revocation.  

## Origin and Path Trace (OPT) 

This is an exstension to SCION to validate packet sources and traces and integrity of data and  paths. 

The idea is that the SCION headers contain a Origin Validation (OV) header. This requires everyone to actually have symetic keys!

The cool thing is that every AS will add their signature to the packet by sining the datahash. This is then send back and then you know that the path was also taken. This is send in the path validation field. 


