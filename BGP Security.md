
In the [[BGP]] protocol it is assumed that all [[Routing Security|AS]] can be trusted. This is not the case and incidents happen often.

# BGP attacks

## BGP hijack

In a BGP hijack an AS announches it owns prefixes that it does not own. This is bad because traffic will be redirected to the bad AS instead of the real one. This can cause Avaiability problems and Impersonation attacks. An As can also announce to own a prefix that has not actually been allocated yet. 

The longer the prefix is you say you own the more traffic is transfered to you.

The lenght of the prefix is number of specified numbers like: 129.12.12.0/17 is more specific than 129.12.0.0/16. This is called sub-prefix hijacking. 

Serial hijackers are AS that repeatedly abuse BPG but are still connected to internet. 

## BGP leak

Here an multihoming AS annouces to one upstream provider that it has a route to a destination through another provider. So the idea is that you have a child AS with two parents and the child announces to parent A that it can reach AS C through parent B. 

![[BGP Security leak.png]]

So here the example is that AS64501 (the red one) annouces to AS64500 (the one with the red circle) that it can route traffic through other parent ASB (gray one). this causes AS65400 (red circle) to route traffic from AS26502 orange circle through red and gray. 

This is a longer path and can cause congestion and surveillance. 

# Improving BGP security 

Several ways of improving BGP security have been proposed. But they all have limitations and its probably better to start over. Scalability, Control, and Isolation On Next-generation Networks ([[SCION]])

## MANRS (Mutually Agreed Norms for Routing Security)
This is an initiative by network operators to agree to rules with how to deal with BGP.  882 participants as of november 2022. [MANRS Website](https://observatory.manrs.org)


- Filtering - Ensure correctness of own announcement. Check if prefix is allocated to this AS.
- Anti Spoofing 
	- Source address validation - check if source address is in frefix allocated  to sender
- Coordination: maintain globally accessible up to date contact information of network operators
- Global validation: Publish data so that others can validate routing information 

## Generalized TTL Security Mechanism (GSTM)

In the ip protocol there is something called TTL (IPv4) and Hop Limit (IPv6). An 8 bit field that indicates the lifespan of packet. Every host reduces the TTL value. If TTL reaches 0 before packet arrives at location it is discarded and an error is send back to the sender. 

However, the majority of BGP peering sessions are established between routers that have a direct connection.  GSTM says that senders should set TTL to 255 and a reciever should disregard TTL below some threshold. Probably just 255. This will disregard all BGP packets that passed at least one hop between sender and reciever. This makes it harder to send fake BGP because you have to inject it on the cable between AS. 

## Filtering using IRRs

There are 5 regional internet registries (RIRs). They decide ip space and AS numbers and maintain IRR that contain information about routing. BGP annouchementes can be checked with this db. 

But that has issues because who knows if RIR is ok or up to date

## Route Origin Authorization (ROA)

Owner of address block is given the authority by RIR to register more ROA for a (subset of) the addresses in a block.

A ROA specifies:
- Adress block
- Acceptable prefix length
- AS that is allowed to originate an annouchement for that block
- This is secured with a digital signature!

You can check the origin acording to the ROV. 

The annouchements can be verified using the signature. 

![[BGP Security ROV example.png]]

ROV = route origin validation. 

SURF can see that the attacker origin does not own the kpn path. 
It might not be a hijack though because the ROA data could just be outdated.

• ROAs and ROV reduce visibility of hijacked prefixes (since announcements are dropped) only if already some AS are using it. 

![[BGP origin validation example.png]]

### ROV limitation

Sometimes you do want to do a BGP hijack like with cloudflare. 

Doesn't work against invalid path hijack where malicious AS advertises route containing non-existing connection.

ROV only checks the origin of the BGP annouchement but not the path. This is called **path hijack**. So if AS3 is origin for prefix P and AS666 announces to AS6 path P,AS3,AS666 while claminig to be AS3. AS6 does accept  this because the origin checks out. You can even add fake AS. 

Apperently this happens often were AS add themselves to the end of path to make the route look longer.

### Resource Public Key Infrastructure 

This requires a resource public key infrastrucute (RPKI). This has been developed and is based on administrative hierachy for allocation of resources. In real life the RIG hold the top certificate CA (certificate authority). All the way down to ISP (End entity) certificate. The end entity can not sign other certificates. They are used to sign the ROA information.

![[BGP Security RPKI.png]]

In the certificate the resource (ip prefix) is bound to the public key of the AS. The ROA information is backed up by the certiciate of the end certiciate directly. If the certificate is revoked then the corresponding information in ROA is revoked. 

**Certiciate Authority** RPKI is different from WebPKI because in webpki any certificate can sign other certificates. In RPKI only parent certificate can sign any certificate, there are rules for this. 

**Accessability** WebPKI: certificates are passed between server and client as needed 
In RPKI each relying party needs to have continual access to entire RPKI certificate collection.

**Subject name** In WEBPKI certificate have a subject name (www.ru.nl) which is meaningfull for the website. 
With RPKI the subject name is not describtive and provides authorization, not authentication. 

Because the repository is stored in ROA the great thing is that you don't need private key of END certiciate after end party send it to ROA. The information should not really change unless revoked. So they can just trow away the private key of the END to end certiciate and just revoke if needed.

The RPKI has been adopted more often the years.

## Path Validation BGPsec

With ROV you only check the origin. This is still not perfect. To adress this they came up with BGPsec. This adds verification of complete path in BGP annouchement because every AS adds a signature. Then you validate the path later. You can also ensure that the AS pairs in the path are adjacent. 

It works with forward siging. So you sign saying who you are going to send the announcement to next. Then you can basically use the chain of signatures when it comes in as proof that the path is real. This uses the RPKI from before but now EE certiciates have to keep private key. 

It is not really implemented because it only work if the whole path has to do it. Also requires more crypto processing + key management. 

![[BGPSec example.png]]

![[BGPSec example 2.png]]

No protection against spurious withdraw messages and route leaks can still occur

## ASPA (Autonomous System Provider Authorization)

This looks at the comercial agreements between AS. Then checks BGP annouchements based on this. This can detect BGP leaks:

![[BGP ASPA example.png]]

If AS wants to be involved in this they have to reveal the relationships between AS.

## BGP blackholing

BGP blackholing is a DoS mitigation strategy. A victim announces that it is being DoS attacked. Then other BSP will stop sending packets to the victim. After this the victim is not avaialble anymore. 

In the BGP blackjack attack a malicious AS2 sends a blockhole as AS1 and then the other AS will drop connections to AS1. This is really funny. You can use ROA to get around this.





