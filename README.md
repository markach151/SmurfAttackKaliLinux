# DDoS Threats in the Network Layer: Smurf Attack 

## Purpose 

Of the many types of criminal activity that occur on the web, few are more puzzling and difficult to prevent than distributed denial-of-service (DDoS) attacks. These attacks can bring down even the largest websites by overloading servers with more requests than they can handle. Recent data trends show that:
* DDoS attacks are still on the rise
* DDoS attackers are now using multi-vector attacks more frequently 
* DDoS attacks are getting more expensive for victims [1]

My goal for this project was to provide knowledge on a specific attack and implement this method in a practical manner.  

## What is a DDoS Attack?

A distributed denial-of-service (DDoS) attack is a malicious attempt to disrupt the normal traffic of a targeted server, service or network by overwhelming the target or its surrounding infrastructure with a flood of Internet traffic. These attacks achieve their effectiveness by utilizing multiple compromised computer systems as sources of attack traffic [2]. These individual devices are referred to as bots (or zombies), and a group of bots is called a botnet. Because each bot is a legitimate Internet device, separating the attack traffic from normal traffic can be difficult.

## Smurf Attack 

A smurf attack is a form of distributed denial-of-service (DDoS) attack in which an attacker attempts to flood a targeted server with Internet Control Message Protocol (ICMP) packets. By making requests with the spoofed IP address of the targeted device to one or more computer networks, the computer networks then respond to the targeted server, amplifying the initial attack traffic and potentially overwhelming the target rendering in inaccessible. In an IP broadcast network, a ping request is sent to every host, prompting a response from each of the recipients [3]. With smurf attacks, perpetrators take advantage of this function to amplify their attack traffic.

## Attack Scenario 

A Smurf attack scenario can be broken down as follows: 
1. Smurf malware is used to generate a fake Echo request containing a spoofed source IP, which is actually the target server address. 
2. The request is sent to an intermediate IP broadcast network. 
3. The request is transmitted to all of the network hosts on the network. 
4. Each host sends an ICMP response to the spoofed source address. 
5. With enough ICMP responses forwarded, the target server is brought down. 

## Experimentation 

An implementation of a smurf attack was performed in Kali Linux. 
* It is a Debian-derived Linux distribution designed for digital forensics and penetration testing. 

The packet generator ‘hping3’ was used to create ICMP packets with a spoofed source IP address [4].  
* --icmp to put us into ICMP mode. 
* -c for the packet count which is 1. 
* --spoof spoof source address. 

Wireshark is a free and open source packet analyzer. It captures network traffic on the local network and stores that data for offline analysis.
* enp0s3 to listen on this specific interface

## Results 

Find the IP address of the target host:

![image4](https://github.com/markach151/SmurfAttackKaliLinux/assets/84886088/6fd298a7-975b-4dc1-8723-94a72f1c0271)

Confirming the target host is up:

![image3](https://github.com/markach151/SmurfAttackKaliLinux/assets/84886088/84c23807-ab71-4647-a438-e7928269ecb5)

Command to generate the smurf attack: 

![image1](https://github.com/markach151/SmurfAttackKaliLinux/assets/84886088/e3098122-b240-4ce4-89e8-5acf7b9b18ed)

ICMP ping responses sent to the spoofed source IP address: 

![image2](https://github.com/markach151/SmurfAttackKaliLinux/assets/84886088/94225c7a-8cf5-429f-8644-afd95e3e3b92)

## Conclusion 

Smurf attacks offer a clever variation of a ping flood attack. The amplification effect provides a large amount of ICMP packets to overwhelm the target host. Some countermeasures include: 
* Configuring the host and routers to ignore broadcast requests. 
* Avoid forwarding packets directed to the broadcast address. 
* If a server is rather weak, ignore ping requests. 

## References 

[1] S. Cook, “DDoS attack statistics and facts for 2018-2022”, _comparitech_, February 2022. 

[2] D. Tang and X. Kuang, “Distributed Denial of Service Attacks and Defense Mechanism”, _The Electrochemical Society_, April 2015. 

[3] E. Georgescu, “What Is a Smurf Attack, How Does It Work and How to Prevent It”, _Heimdal Security_, September 2021. 

[4] D. Adams, “hping3 Flood DDoS”, _linuxhint_, May 2020.
