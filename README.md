# Network-Security

This is basic knowledge about Network Security 


## APT (Advanced Persistent Threat) 

APT is a broad term used to describe an attack campaign in which an intruder or team of intruders, establishes an illict, long-termpresence on a network in order to mine highly sensitive data

- They know who they want to target
- Try to get all the resources 
- Undercover longer period (Monitor/Pull the information out) 

ICS (Industrial Control System) - Hardware and Software communication that are used to monitor and control industrial processes (i.e., Power Grid, Water Supply, Transportation, and etc..) 

SCADA (Superviosry Control and Data Acquisition) - ICS that monitors and controls field devices at a remote site (centralized) system. (Centrailized system monitors and contorls an entire system in real time) 

## IT vs OT/ICS 

IT would be used by humans dealing with data alone and serving the employees / OT would be dealing with actual manufacturing process

IT Threat -> CIA Traids (Confidentiality, Integrity, and Availability) 

OT Threat -> Human Injury & Environmental Disaster, Damaged Equipment & Physical Process downtime, and Unauthorized information disclosure

## Why OT is more ciritical than IT?

Vulnerabilities on OT is more directly to human life system. IT might be just compromising the data.

Many of IT system is connected to OT maybe testing equipment and management report to supervisor 

Remote control system that not always human can be present at the location. They need to send the data to the other part 

## Purdue Model 

Hierarchical model for ICS network segmentation defines six layers within these networks, the components found in the layers, and logical network boundary controls for securing these networks. 

![image](https://user-images.githubusercontent.com/79100627/195395203-6f9486dc-8104-459e-89e2-a5e8ed739996.png)

Internet DMZ Area - Publicly accessible server does require some attention and some protection even though these are publicly accessible servers. You need to access them interent community you still do not want anything to happen there (Ligher Firewall) 

Enterprise Zone - Employees server. 

Physical Process: Field of I/O Devices - These are known as Crown Jewels. Most protected. That are the key of overall operation you should not allowy any manipulation. 

## Zero Trust 

Fact that as you go down the layer, you have to protect more but one major issue is that the model is assuming all traffic coming from the internet towards Crown Jewels is taking one single path. However, most of PLC is nowadays with WiFi and Bluetooth. This could cause a potential problem that if the hacker physically come to PLC, he can bypass all the firewaalls and start the direct communication

Zero Trsut is that internal trust (Even employee) is not trustable. (What if a hacker hacks higher layers (with less protection) and execute the command?) 

PLC - Preventable Logical Controller (That control machine remotely) 

## Pipedream (Dragos) Incontroller (Mandian)

Hacking toolkit with an array of components designed to disrupt or take control of devices, primarily programmable logic controllers (PLCs) sold by Schneider Electric and OMERON 

- It is not single malware it's a combination of a tools 
- Many other manufacture use same type of software 
- Currently exploits underlying software in those PLCs (Codesys), which is used across hunred of other types of PLCs 
- Not clear where the US government agencies found malware or who exactly has created. 
- Has not been deployed yet but likely desgined to eventually strike against electric utilities

## Pipe Dream/ Incontroller Components 

- Evilscholar: It always discover access and manipulate Schneider Electric PLCs. It has been developed with Python and Linux ELF Library 
- Badomen: It allows to scanning, identifying and accessing Omron software PLCs. 
- Mousehole: It allows to interact and access OPC unified server architecture allowing brute-forcing attack or node ids enumeration. It has been coded with a Python framework and target OPC-UA server (Central Server where you keep the information and contact of all system (encryption, other important information). Database (list of all the other components to IoT, form communication group). 
- Dusttunnel: It allows for persistence and command & control remotely. It has been coded in C++ and target Microsoft Windows Devices. (Command and Control)
- Lazycargo: It allows elevating credential by exploiting a known vulnerabilitiy ASRock driver (Windows -> targeting laptops) two way of compromising: Sensor and administrator window machine. 

![image](https://user-images.githubusercontent.com/79100627/195409022-55fe7830-4a0c-4020-8528-e380862b0f6f.png)

## Purdue Model

IT (Dusttunnel, Mousehole) OT (LazyCargo, Evil Scholar, Badomen). If they are targetting same application, why do they have two different instances?

Beacuse, maybe they are using differnt way and they are using different port. Given two companies, software is same but port is different 

## Behavior Towards Schneider Electric Devices

- It can scan with UDP multicast over port 27127 in order to identify all Schenider PLC's very fast on another network.
  - To find communication route 
- Use brute force on Schneider PLC password via CODESYS over port 1740 
  - Guess the Password for PLC devices 
- Conduct DoS attack to avoid network communication to PLC 
  - Administrator send the command but if DoS of the PLC, command might executed much time later (Which it will affect system) time out
  - TCP -> TCP might break if you have not received packet in time 
  - Sensitive to format 
- Cut connection in order to force re-authentication to the PLC and then gather credential information 
  - Why brute force vs cut re-authentication? 
    - Brute Force is very noisy: Possibilities of defender can catch this 
    - Less noisy then Brute Force 
    - Certificate -> every device has preloaded certificate 
- Crash the PLC, for power cycle and configuration recovery 
- Push custom Modbus commands/packets 
- Find files/directory listings in the device and the subnet 
- Delete files in the device and the subnet 
- Add a route if the device gateway IP exist on a different interface 
  - Pipedream can change the gateway route 
     - ARP attack
     - Path can be more easy for hacker (Port Change)
     - Sensors 

## Threat Agents 

National State - Geopolitical 
Sate - Sonsored group (Not government direct but connection) 
Cyber Criminals - Profit 
Hactivist - Ideological 
Terrorist Groups - Ideological 
Thrill-Seekers - Satisfaction 
Insider Threats - Discontent

## APT Again (Adavnaced Persistent Threat) 

- Stealthy threat actor, typically a nation state or state - sponsored group but recently also criminal groups 
  - Gain unauthorization access to a computer network system 
  - Remain undetected for an extended period of time 
  - Infiltrate and/or exfiltrate as much valuable data as possible without being discovered 
  - APT's typical motivations are political or economic 
  - Sectors typically targeted by ATPs: government, defense, finanacial services, legal services, telecoms, industrial 
  - In 2019, mean 'dwell time' was 197 days but it is 24 days -> not want to risk wait so long to be discovered 
  
 ## Dwell Time 
 
 Amount of time APT is willing to quietly sit in the system but they are not doing major 
 
 APT 
  - Advanced = adversary possesses sophisticated levels of expertise & resources which allow it to achieve its objectives using multiple attack vectors 
    - Use full spectrum of state-level intelligence-gather: techniques and resources 
    - Use latest attack strategies 
    - Use multiple methods, tools and techniques 
  - Persistent = Adversary pursues its objective repeatedly over an extended period of time; adapts to defender's efforts to resist it; and if it loses access to the target it usually re-attempts access 
    - Persistent also indicates that cyber criminals remain in the network once it has been infiltrated/compromised vs. other types of attacks in which the attacker strike quickly and then leaves the network 
  - Threat = APTs are threat because they have both capabilities and intent 
  
## Hacking Phases 

1. Reconnaissance - Sitting on the back 
2. Scanning - What server, port is open
3. Gian Access - Vulnerability access and implement malware 
4. Maintaining Access - Malware 
5. Clearing Tracks - Clear and go out 

## ARP Protocol

## Why Address Translation 

We need both physical (MAC) address and logical(IP) address for packet delivery

- IP addresses are needed for packet routing 
- MAC addresses are needed for packet delivery within the LAN 

## When is Address Translation Happens?

Anytime a host or a router has an IP packet to send, it must be able to encapsulate the packet in the corresponding data-link layer frame

- IP sender knows the address of IP receiver but also needs to know MAC address of next hop receiver 

![image](https://user-images.githubusercontent.com/79100627/198148623-adb235b5-76e6-4bec-8fd4-30ce4bc55fcb.png)

## How is Address Translation Performed?

- There are two main approaches that facilitate IP <-> MAC address translation

1. Static Mapping
2. Dynamic Mapping 

## Static Address Translation 

- Create a table that associates a logical address with a physical address and store in each machine 

Issue: 

1. For every new device added to the LAN Network, the tables would have to be manually updated (For every computer)
2. Gateway could change its NIC resulting in a new physical address
3. Mobile station can move from one LAN network to another, resulting in a change in its logical address

## Dynamic Address Translation

Use a protocol to find another address. Keep the obtained results in a table 

## Address Resolution Protocol 

Accpets a logical address from IP layer (protocol) and maps the address to the corresponding physical address

- Supports its main function through 2 key operations:

1. Maintenance of a cache/table of ARP mappings
2. Exchange of ARP requests & replies 

## ARP Cache 

There are static ARP and Dynamic ARP cache entries 

1. Static ARP entries are manually configured and kept in the ARP cache table on a permanent basis (They don't age out) 
- Static entries are best for devices that have to communicate with other devices in the same network on a regular basis 

2. Dynamic ARP entries are added as a result of ARP requests & reply exchange with other devices, are kept for a period of time and then removed (expires) 

![image](https://user-images.githubusercontent.com/79100627/198149732-998d27f3-cc03-4942-be33-747d6130d9cd.png)

## Exchange of ARP Request and Reply 

- Host A broadcast the ARP request message that who has the IP Address of x.x.x.x ?
- All the machine receives the ARP requeset and one with the IP Address of x.x.x.x replies back with the MAC address 

## ARP Packet Format 

![image](https://user-images.githubusercontent.com/79100627/198150519-e4e4ea35-e270-4cc7-bda6-d2631e5b6d81.png)

- Hardware Type : defines the type of data link network (Ethernet - type1) 
- Protocol Type : 16 bit field defines the type of higher layer protocol 
- Hardware Length : 8 bit field, defines the length of physical address in bytes (e.g. for Ethernet - value = 6) 
- Protocol Length : 8 bit field, defines the length of logical address in bytes (e.g. for IPv4 - value = 4) 
- Operation: 16 bit field defines the type of ARP (opcode == 1 ARP Request, opcode ==2 ARP reply) 
- Sender Hardware Address: variable-length field defines the physical address of the sender in bytes 
- Sender Protocol Address: variable-length field defines the logical address of the sedner in bytes 
- Target Hardware Address: variable-length field defines the physical address of the target 
  - for an ARP request, this field all 0s because the sender does not know physical address of the target 
- Target Protocol Address: variable-length field defines the logical address of the target

## Gratuitous ARP - an ARP Response that was not prompted by an ARP Request. Gratutious ARP is sent as a broadcast message and is a way for a node to announce or update its IP to MAC mapping to the entire network 

How to recognize if an ARP packet is 'gratutious'?

- OPCode == 2 (ARP Reply) 
- Source IP = Destination IP 
- Target MAC = ff:ff:ff:ff:ff:ff 

This prevents ARP entries aging out and Prevent Gateway Spoofing 

## ARP Vulnerabilities 

1. ARP does not authenticate request or replies, ARP Requests & Replies can be forged 
2. ARP is stateless - ARP Replies can be sent without a corresponding ARP Request 
3. A node receving an ARP Packet (Request or Reply) must update its local ARP cache with the information in the source fields

## ARP Attacks 

1. ARP Flooding / DDoS - typically targeting gateways 
  Any defence? 
    - To avoid rate limit on ARP packets (Certain threhold in ARP packet) 
    - Strict ARP -> the gateway learns only the ARP Reply packets in response to the ARP Request packets that it has sent. This action prevents ARP entries on the gateway from being exhausted when the gateway processes many ARP packets 
    - ARP entry limit 
 
 
2. ARP Spoofing / ARP poisoning 

- 3 main flavours 
  - Gateway Spoofing 
  - User Spoofing 
  - User-User Spoofing 

Defense of Spoofing (ARP)
- Gratutious ARP Packet Discarding 
- Strict ARP Learning 
- ARP Packet validity check 

## The Internet Protocol = IP 

Provides basic data transfer function in the form of data blocks (datagrams) from a source to a destination host across multiple/different nets 

![image](https://user-images.githubusercontent.com/79100627/198156520-e4da27b4-70d5-45ee-ac47-b1a11bade5ad.png)


![image](https://user-images.githubusercontent.com/79100627/198156533-6698ba47-3dc8-480b-a012-4409909169c9.png)



