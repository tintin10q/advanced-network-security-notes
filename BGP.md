BGP border gateway protocol is the protocol used by [[Routing Security|Autonous system]] (as) to comunicate which ip prefixes they own.

The routers in an AS know which prefix their AS owns. If their AS doesn't know the ip the router sends the ip to a border router. These routers know the prefixes for all AS and can construct a path from the source to the destination. Path is based on cost, path length and lenght of prefix. **BGP assumes all networks are trust worthy**.

### BGP advertisements

In the BGP protocol routers send advertisements to let neighboring AS to let them know what prefixes they own. these advertisements are send every 10-60 seconds. Each **router** builds own routing table of prefixes and learns the topology of the network at AS-level from its neighbors.  Over the years the average routing table has increased from 20k to 1M for ipv4 and ipv6 is coming. 

A BGP routing table consists of **routes**. Routes consist out of: 
- **Ip address prefix** owned by the AS
- **Origin AS** (who owns the specified prefix)
- **AS path** (path vector of ANS, how to get to prefix)
- **Next hop**, where to go next if you want to get to AS

In the image follow the path.  
The actual path taken is not always the shortests path it could also be the cheapest path. The AS al have underlying agreements.

![[BGP advertisements.png]]

You got the AS can send BGP route announcements and BGP withdrawals to eachother. 

The **route announcements** contain new info about routes. This is compared to the info which it already had and if the info is better like a better path the route table is updated. 

The **route withdraws** cause routing table to delete routes. AS send these to their neighbors if they can't provide a path anymore. These cause routes to be removed from routing table. 





