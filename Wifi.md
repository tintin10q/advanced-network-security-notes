Wifi is a local area Network (LAN), the idea is theat you have samll network instead of a wide area network that you get with [[Mobile Network]]. How this works is specified in standarts. IEEE 802.11 IEEE 802.1X, only the lowest 2 layers, (mac and phyisical) are different from the traditional network stack. Nevertheless the standart is still 4000+ pages. 

It specifies mobile (walking around) and stuck devices.

## Termologoly  IEEE 802.11 

- **Station (STA)**: device with wireless interface (logical entity with interface to wireless medium), 
- **Basic Service se**t (Bss) : set of stations in the same wireless network area
- **Service set identitie**r (SSID) name of the network used to connect
- **DSM** DSM medium used by ds
- **Access point (AP)**: station that provicdes access to the distribition system services vai the wireless medium for assotionated STA
- **Message integrity check** MIC: Message authenctication control 

![[Wifi bsa.png]]

Asociation is a mapping between an access point (AP) and a station (STA)

The station (sta) is usually the authenticator.

## Termology IEEE 802.1x

Only about 2000 pages for security and access control.

- **Port** (basic): service point within each station attached to LAN (local area network), used to transmist and recieve data frames at mac layer.
- **Control port** provides secure access controlled comunication. 

## Association 
An association is how station (device like your phone) can connect to AP
We also have a standart for this 802.11 which talks about the mapping between access point (AP)  and station STA.  

You got a secure and not secure version. 

## Wi-Fi is not in the standart (Wi-Fi Alliance)
Wifi is not not actually part of the above standart, it is a trademark of the wifi allience which has a bunch of companies to make sure that the devices work together. 

We are now at WiFi 6. It is newer versions of the 802.11 standarts by adding letters. 

Wi-Fi is for local area network and [[5g]] is for WAN wide area network. 

When wireless technology were first developed there was no security. 

## Wifi Security
- First area = **WEP**, wich is broken
- Second era **WPA**, different crypto now TKIP for encryption addon to WEP
- Thirth era **WPA2**, from TKIP to AES-CCMP and stronger auth 
- Fourth era **WPA3** recently, AES-GCMP (galios counter mode) and enhanced privacy

80% of traffic is encrypted.

There are different [[Types of Wifi]].

## Signals 
It works by transmitting a signal which is send in a sphere from an attena. In the radio wave, there are channels. Channels 1, 6 and 11 are the best ones.


![[Wifi the whole story.png]]