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
