
[[Botnets]] are used to do DDOS attacks distributed denial of service attacks. 1.2 TB/s In  2016 by [[IoT botnets#Mirai botnet|Mirai botnet]].

## Network layer
You use weakness in internet protocols to flood the system. You can also amplify response by spoofing source ip to redirect the many responses from a security protocol to a victim. Or you just send malformed packets. 

## Application layer
You can also use the HTTP protocol to exhaust resources available to servers. Session flooding, request flooding, high workload requests. This is difficult to detect because what's right what's wrong?

## Mitigation 

Redirect traffic via DNS or BGP to filter/block traffic before passing it to destination. Cloud security providers also offer DDoS attacks as protection-as-a-service. Cloudflare and Akamai. These are really popular. Used by 80% of users and the other 20% can't because of privacy like governments. 

Cloudflare analyses traffic for DDoS attack using various techniques while trying to avoid latency. Once an attack is detected the signature with characteristic attack is generated and blocked.

DDoS attacks get more powerful every year. 37 → 68 → 140 → 200 Gb/s in 2017-2020 (max) in NL
Most attacks take 15-60 minutes. FBI and Dutch police take down websites offering DDoS attacks.

National scrubbing center against DDoS attacks (NaWas) for ISPs and VoIP providers 
 - initiated after DDoS attacks on banks in 2014 
 - rerouting traffic by BGP announcements

And finally you got the **anti DDoS coalition** since 2018 with tries to do DDoS pattern recognition.