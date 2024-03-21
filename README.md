# PROJECTNAME

## Objective
[Brief Objective - Remove this afterwards]

The Detection Lab project aimed to establish a controlled environment for simulating and detecting cyber attacks. The primary focus was to ingest and analyze logs within a Security Information and Event Management (SIEM) system, generating test telemetry to mimic real-world attack scenarios. This hands-on experience was designed to deepen understanding of network security, attack patterns, and defensive strategies.

### Skills Learned
[Bullet Points - Remove this afterwards]

- Advanced understanding of SIEM concepts and practical application.
- Proficiency in analyzing and interpreting network logs.
- Ability to generate and recognize attack signatures and patterns.
- Enhanced knowledge of network protocols and security vulnerabilities.
- Development of critical thinking and problem-solving skills in cybersecurity.

### Tools Used
[Bullet Points - Remove this afterwards]

- Security Information and Event Management (SIEM) system for log ingestion and analysis.
- Network analysis tools (such as Wireshark) for capturing and examining network traffic.
- Telemetry generation tools to create realistic network traffic and attack scenarios.

## Steps

1. Used Draw.io to create the network diagram. This highlights basic data flow between the platforms.
   
![Screenshot 2024-03-21 104506](https://github.com/Benrosan/Detection-Lab/assets/160042310/f2712f60-5e33-4212-8239-7cad515fbf8e)

2. Second step was to start installing the various platforms. I used a hybrid cloud infrastructure model. I used LXC containers in Proxmox to host Wazuh and TheHive. It's always good practice to configure and launch VMs and containers, especially on a platform as intuitive and flexible as Proxmox. 
   
![2024-03-21 10_58_27-pve01 - Proxmox Virtual Environment](https://github.com/Benrosan/Detection-Lab/assets/160042310/293ff2af-9ca5-46a4-bd74-9964b6a66edc)

I may reduce the resources allocated to some containers as some are being under-utilized.



