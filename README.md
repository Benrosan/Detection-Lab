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

**1.** Used Draw.io to create the network diagram. This highlights basic data flow between the platforms.
   

![Screenshot 2024-03-21 104506](https://github.com/Benrosan/Detection-Lab/assets/160042310/f2712f60-5e33-4212-8239-7cad515fbf8e)


**2.** Second step was to start installing the various platforms. I used a hybrid cloud infrastructure model. I used LXC containers in Proxmox to host Wazuh and TheHive. It's always good practice to configure and launch VMs and containers, especially on a platform as intuitive and flexible as Proxmox. 
   

![2024-03-21 10_58_27-pve01 - Proxmox Virtual Environment](https://github.com/Benrosan/Detection-Lab/assets/160042310/293ff2af-9ca5-46a4-bd74-9964b6a66edc)


I may reduce the resources allocated to some containers as some are being under-utilized.

**3.** Both platforms were installed using the Linux CLI. (Ubuntu 22.04). Used common commands including **cat**, **nano**, **systemctl** etc...


![Screenshot 2024-03-21 110518](https://github.com/Benrosan/Detection-Lab/assets/160042310/5e2d12e6-210b-45a0-bd89-458868e87f1e)


Also installed **htop** as it's my preferred tool for checking resource use in addition to commands like **top**, **free -h** etc...


![Screenshot 2024-03-21 094804](https://github.com/Benrosan/Detection-Lab/assets/160042310/88a67d77-7236-43a0-8fb6-148234a8d5ed)

**4.** Installed Sysmon for more detailed event/log capture. It's interesting to note that configuration files for Sysmon can vary greatly and are absolutely essential to security event logging within both Windows and the SIEM. I used Olaf Hartong's <a href="https://github.com/olafhartong/sysmon-modular">config file</a>

![Screenshot 2024-03-21 111708](https://github.com/Benrosan/Detection-Lab/assets/160042310/b9443f7b-2231-4f67-81c1-a7dd0b7a07c0)

**5**. After installing the Wazuh manager, I installed my Wazuh manager on my chosen endpoint. This was done quickly via PoweShell script. I then confirmed the service was running on the host.

![2024-03-21 11_19_53-Services](https://github.com/Benrosan/Detection-Lab/assets/160042310/903e80ea-2b18-46a2-ad6b-423796488bac)

**6.** Next step was to update the config file for Wazuh to have it ingest the Sysmon logs.

![2024-03-21 11_29_11-ossec conf - Notepad](https://github.com/Benrosan/Detection-Lab/assets/160042310/b41c2d29-c4d0-486d-8bf7-ee6d95678a0e)

I then restarted the Wazuh service and confirmed the logs were appearing in the Wazuh dashboard.

![2024-03-21 11_33_48-Wazuh - Wazuh](https://github.com/Benrosan/Detection-Lab/assets/160042310/b811216d-4042-4747-955b-cd2b9d82d049)





