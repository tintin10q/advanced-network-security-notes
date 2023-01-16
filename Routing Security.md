Internet routing is the system that makes sure that if a host A sends a message to host B that it actually happens and ends up at host B. This works by a network of interconnected routers. Routers send on their messages to other routers until it reaches the destination.  

![[Routing.png]]

DNS is used to resolve IP into domain name. 

How do the routers know how to route? The routers are composed of interconnected networks called **autonomous systems (ASes)** so like KPN is an AS and Amazon is also an AS. There are about 75k active AS. These are usually competing entities that make their own decisions. 

![[Autonomous systems.png]]

Every AS is allocated a block of IP addresses that they can use. This works with prefixes:

- 145.97.24.0/21 (10010001.01100001.00011xxx.xxxxxxxx), the x part can vary. All the IP addresses that you can make with this prefix the AS owners can give to devices in the AS. 

**Intra routing** is routing inside one AS uses IGP protocol RIP, OSPF but whatever
**inter AS routing** is routing between multiple **AS** that uses [[BGP]] protocol. 

You have 3 types of relations between AS:

- **Peers** - traffic is transferred for free. 
- **Customer-provider** - Customer pays for access. So AS20 is customer of AS0
- **Multi homing** - As has multiple upstream providers to provide reliability

![[Routing relationships.png]]



