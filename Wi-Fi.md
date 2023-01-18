Wi-Fi is a local area Network (LAN), the idea is threat you have small network instead of a wide area network that you get with [[Mobile Network]]. How this works is specified in standards. IEEE 802.11 IEEE 802.1X, only the lowest 2 layers, (mac and physical) are different from the traditional network stack. Nevertheless, the standard is still 4000+ pages. 

It specifies mobile (walking around) and stuck devices.

## Terminology  IEEE 802.11 

- **Station (STA)**: device with wireless interface (logical entity with interface to wireless medium), 
- **Basic Service se**t (Bss) : set of stations in the same wireless network area
- **Service set identifier (SSID) name of the network used to connect
- **DSM** DSM medium used by ds
- **Access point (AP)**: station that provides access to the distribution system services via the wireless medium for associated STA
- **Message integrity check** MIC: Message authentication control 

![[Wifi bsa.png]]

Association is a mapping between an access point (AP) and a station (STA)

The station (STA) is usually the authenticator.

## Terminology IEEE 802.1x

Only about 2000 pages for security and access control.

- **Port** (basic): service point within each station attached to LAN (local area network), used to  and receive data frames at mac layer.
- **Control port** provides secure access controlled communication. 

## Association 
An association is how station (device like your phone) can connect to AP
We also have a standard for this 802.11 which talks about the mapping between access point (AP)  and station STA.  

You got a secure and not secure version. 

## Wi-Fi is not in the standard (Wi-Fi Alliance)
Wi-Fi is not actually part of the above standard, it is a trademark of the Wi-Fi alliance which has a bunch of companies to make sure that the devices work together. 

We are now at Wi-Fi 6. It is newer versions of the 802.11 standards by adding letters. 

Wi-Fi is for local area network and [[5g]] is for WAN wide area network. 

When wireless technology were first developed there was no security. 

## Wi-Fi Security
- First area = **WEP**, which is broken
- Second era **WPA**, different crypto now TKIP for encryption add-on to WEP
- Third era **WPA2**, from TKIP to AES-CCMP and stronger auth 
- Fourth era **WPA3** recently, AES-GCMP (Galois counter mode) and enhanced privacy

80% of traffic is encrypted.

There are different [[Types of Wifi]].

## Signals 
It works by transmitting a signal which is sent in a sphere from an antenna. In the radio wave, there are channels. Channels 1, 6 and 11 are the best ones.


![[Wifi the whole story.png]]