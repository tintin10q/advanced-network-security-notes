

## Bot detection:

**Active detection** means actifly trying to attack a [[Botnets|botnet]]. You can do this by participating in a botnet and acting like you are a bot and see if you can get onto C&C or peers (infiltration). Then you could try hijack the C&C. 
If you do hijack C&C, you know who all the bots are. Either you phyiscally seize the C&C or you try hack it or BGP or DNS blacklist it.

**Passive detection** try to **detect bots** on hosts or on network. Either based on code **(syntax)** or **signature (hash)** - but botnets just change these things and signatures get out of date. 
You can also try **semantic techniques** to detect **behavior** but hard and false positives.  Correlational analysis is also something like this.  

You can do a correlation analysis, you look at machines that should do the same thing and if one starts to deviate it could be part of a botnet.

## C&C communication detection 

### Active C&C communication 

**Inject** blindly traffic into sus network flow and see response. **Supress** some incoming outcoming packes.  But this is difficult and generates more false positives

### Passive C&C communication 

Again **syntactic** or **behavior based** (semantic). Syntactic works well but is outdated by definition and semantic has false positives. For semantic you have:
- Statistical approuches - machine learning for network traffic classification
- Correlation based method - check for similar simiar communication in router
- Behavoir based models - Identity deviation from normal traffic or similarity with "normal" behavior. Typically host by host basis.

## Botmaster detection: 

### Active botmaster detection

- **Packet marking** 
	- Information is written into packets by a victim machine or intermediate routers. This allows to help locate attacker.
       This is used a lot 

### Passive botmaster detection

- Logging by routers about packets
- Stepping stone detection. You have to recursifly identity the bot master based on correlation with content, host activity or packet timing. 
- Dificulties with this:
	- Bot master may manipulate and forge log information
	- Random delays in arrival times of packets induced by network or botmaster
	- Botmaster may add additional packets to confuse the detection 
	- Tor
	- Encryption 


Botnets detection:
![[Attacking botnets.png]]
