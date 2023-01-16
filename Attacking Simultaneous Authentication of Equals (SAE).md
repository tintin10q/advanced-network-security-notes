
The [[WPA#Simultaneous Authentication of Equals (SAE)]] is a step during establishment. It involves crypto, namely adding points on an elliptic curve. This is quite resourcefull so you can easily dos the [[Wifi|AP]] by just connecting with it often by sending a bunch of commit messages. 

Only 8 connection attempts is already enough for 521 bit prime. 70 connection for 256 bit prime. 

This is is adressed by the AP keeping track of the ungoing SAE handshakes. If the number goes above a threshold the AP responds to a new commit with an **anti clogging token** instead of doing the crypto. This token is derived from a hash of random secret and mac of connecting device. In the next try the STA should send the anti clogging token with the commit message.  Otherwise the AP just rejects the message. The stations that were trying to connect earlier get priority. This way even though you DoS you will still get through.

This prevents that adversary launch DoS attack by sending commit messages with spoofed MAC addresses, but adversary can still eavesdrop, capture anti clogging token, and send commit message with token and spoofed MAC addresses. 

This was inspired by IP cable anti clogging tokens where if you spoof the ip you came from (like spoofing mac) the message won't come back to the attacker but the ip you said it came from. But with the air interface this is not an issue for the attacker because you can still just eavesdrop. 

