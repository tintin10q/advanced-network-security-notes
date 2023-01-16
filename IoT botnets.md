
IoT botnets are [[Botnets]] where to bots are IoT devices. IoT devices have to be cheap so they have bad security and bot masters exploit this. Each IoT device on its own is weak but together they are a force to be reconed with. 

- Because of this it is easy to turn IoT device into Bot. Because there are many IoT devices they are threated as much more disposable with simpler techniques like hardcode ip (or domain name in 10% of cases)
- Only brief distribution of bot binary. 
- C&C hosted at cloud provider and usually only for a short time. 

## Mirai botnet 

One famous IoT botnet is **mirai botnet**

1. Scan for victim
2. Login on victim using preset known passwords  
3. Infect mallware 
4. Conceal, 
	- delete binary and obfuscate process name with random string. Usualy people rarely turn off their Iot device
5. Scan & wait for isntructions 

![[IoT botnets Mirai.png]]