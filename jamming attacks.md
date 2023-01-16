
Before a [[Wifi|STA]] to transmit over a network it first senses the channel to determine if another STA is transmitting IDL or not. STA use the CSMA/CA method (carrier sense mutiple access with collision avoidenance). If the channel is busy the STA waits for a random backoff period so that there is a chance that they can send later. 

![[CSMA backoff period.png]]

However if you just have a bad STA that always sends something then nothing will send. This is what a **jammar** does. 

![[jamming attack.png]]

Basically with a jammar the channel never becomes idle not for sender and reciever.
Jamming may vary in: **timing** (constant/intermittent/reactive), **signal strength** (constant/adaptive) and **signal type** (constant/deceptive/intelligent). 

- **Constant**: is just fireing a jammer signal all the time (most simples one)
	- Works with any wireless system with limited bandwith and power
	- Takes a lot of energy and not effecient
	- Detected by RSS and CST and PER 
	 - Can be defeated by frequency hopping (just going to another frequency)
- **Intermittent/random**: jamming signal is transmitted from time to time
- **Reactive**: jamming signal is transmitted only when legitimate transmission is detected so channel is busy
	- More energy effiecient
	- Only detected by increase of RSS and PER but no change in CST
	 - Can be defeated by frequency hopping (just going to another frequency)
	 - Also defeated by spread spectrum technique, spread radio signal over very wide frequency bandwith, so that signal has low power spectral density, even below background noise level. You then add redundancies so that you really have to block the whole bandwith which is hard. 
- **Adaptive**: Same as reactive, but jamming power is adjusted dynamically to any specific level required for disrupting the legitimate receiver.
	- Most energy efficient but success depends on choosing right power level
	- Dected by increase of RSS and PER but no change in CST
	- Can be defeated by frequency hopping (just going to another frequency)
	- Can be defeated by spatial retreating (move legitimate nodes away from jammed area)
- **Deceptive**: constantly injects regular packets in channel (to keep reciever busy)
- **Intelligent**: exploits weakness in upper layer protocols to block legitimate transmission (DoS) like  Smurf attack,  TCP/UDP flooding or malware attack

![[jamming types.png]]

## Detecting jamming 

Can we find out if a jammer is active?

### Received Signal Strength (RSS) 

- Receiver measures the energy level of received signal 
- Increased signal strength may indicate jamming because it tries to shout loud 

![[Jamming RSS.png]]

Here the top 2 is the normal signal the others are jamming signal. 
With the recieved signal strenght (RSS), CBR is hard to distingish from reactive jammer. MaxTraffic is hard to distingish from constant/deceptive jammar.

So RSS is not so good for jamming detection becuause loads of false positives. 

### Carrier Sensing Time (CST)

Measure how long it takes for the channel to become idle again. If this increased a lot then you might be jammed.

- CSMA/CA (transmitter senses whether channel is idle before transmitting a frame) 
- Measure signal strength and compare with threshold (fixed or adapted to noise level) to determine if channel is idle or busy 
- Increased waiting time for busy channel to become idle may indicate jamming 
- Delayed transmission may cause packets are dropped (transmit buffer full) or timeout

CST is good for distingishing constand/deceptive from MaxTraffic because in Max traffic there are still gaps but that is not the case of constand/deceptive because then it really takes long before you become active again.

It doesn't work at all for reactive/random traffic because the CST is smallar than for MaxTraffic.

![[CTS jamming detection.png]]

### Packet Send Ratio (PSR) 
If the number of packets that where successfully send drops then you might be jammed.  Lower PSR may indicate jamming. 


### Packet Delivery Ratio (PDR) & Packet Error Ratio (PER)
Ratio of packets that pass (PDR) or fail (PER) CRC-integrity check. Increase in failing integrity checks may indicate jamming. 

For PSR (packet send ratio) and (packet delivery ratio) you can expirment with different variables.

- Use CSMA/CA to measure if channel is busy and compare to fixed (1.1.1 mac) or variable (BMAC) treshold. 

- Then for jammers you have variables like dXA (distance to jammer) and sending mode, 
- Sleeping time for random jammers ($t_s$)
- For reactive jammer: size of legitimate packers (m)

![[jamming attacks PSR PDR.png]]

