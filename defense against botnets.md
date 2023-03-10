
You can defend against [[Botnets]] with **preventative** or **remedial** measures. 

Preventative is proactive measures before you get infected. 
Remedial helps to recover from a botnet infection.  
-   Defensive - reactive measures to recover from botnet like bot disinfection. Important for users but does not kill botnet
- Offensive: Measures to damage botnet infrastructure 


# Preventive measures

## Host cleanliness
Avoid vulnerabilities in OS and applications and apply patches. Be aware of botnets maybe use antivirus software. Don't use ports favoured by C&C. I should really change the ssh port to something else.

## Network cleanliness
Secure the connection to the host (servers, email etc.), apply a network detection system, make honeypots to see if someone is doing something fishy. Block access to known bad domains and use proxy to scan content. Inbound for malware. Outbound for data leaks.

## Not technical 

- Target botnets business model. To find it
- Make good laws against botnets
- Educate people

# Remedial measures

If you get infected just reinstall. You can also block in the firewall, but you basically just have to reinstall. 

Offensive:
Target botnets business model. For instance anti-spam things. (indirect attack)
Hacking the C&C server: (Direct attack)
DOS the C&C server.

## Responsibility 

Who is responsible: Users and or ISP. 
Is the responsible party willing to take measures?

Users only care if their data is stolen or their machine lags too much.
ISP sometimes care but often also don't care because they argue they don't really make money from preventing botnets. They only prevent it because of peer pressure, reputation and abuse complains, but they are not direct victims,

The more subscribers an ISP has the more infections. Similar size ISP have large differences in infection levels. The main incentive to do something is cost of when it goes wrong and pressure from government. 

Hosting providers are also responsible, but they really don't care. Because of this, botnets have turned towards cloud computing.

Smartphones are also interesting targets and sometimes botnets use social media to communicate. 
