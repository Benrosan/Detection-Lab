# PROJECTNAME

## Objective

The goal of the Detection Lab project was to build a realistic environment for simulating and detecting cyber attacks. The primary focus was to build an entire workflow to ingest, log and analyze events within a SIEM that reflect real-world attack scenarios, thereby providing me an opportunity to familiarize myself with the various tools/processes used by Blue Teams to assess and respond to cyber threats on a daily basis. 

### Skills Learned

- Basic understanding of SIEM concepts and practical application.
- In-depth understanding of log and event generation on host devices.
- Implementing SOAR workflows.
- Ability to generate and recognize attack signatures and patterns.
- Increased knowledge of key security frameworks including the MITRE Att&ck framework.
- Basic Linux server management skills

### Tools Used

- Wazuh - Security Information and Event Management (SIEM) system for log ingestion and analysis.
- Sysmon - Telemetry generation tools to create realistic security event logs
- Shuffle SOAR - for security workflow
- TheHive Security incident Response Platform - for generating alerts
- Proxmox - used to self host LXC containers for Wazuh and TheHive platforms.

## Steps

**1.** Used Draw.io to create the network diagram. This highlights basic data flow between the platforms.<br>

<br>

![Screenshot 2024-03-21 104506](https://github.com/Benrosan/Detection-Lab/assets/160042310/f2712f60-5e33-4212-8239-7cad515fbf8e)


**2.** Second step was to start installing the various platforms. I used a hybrid cloud infrastructure model. I used LXC containers in Proxmox to host Wazuh and TheHive. It's always good practice to configure and launch VMs and containers, especially on a platform as intuitive and flexible as Proxmox.<br>

<br>

![2024-03-21 10_58_27-pve01 - Proxmox Virtual Environment](https://github.com/Benrosan/Detection-Lab/assets/160042310/293ff2af-9ca5-46a4-bd74-9964b6a66edc)

<br>

I may reduce the resources allocated to some containers as some are being under-utilized.<br>

**3.** Both platforms were installed using the Linux CLI. (Ubuntu 22.04). Used common commands including **cat**, **nano**, **systemctl** etc...<br>

<br>

![Screenshot 2024-03-21 110518](https://github.com/Benrosan/Detection-Lab/assets/160042310/5e2d12e6-210b-45a0-bd89-458868e87f1e)

<br>

Also installed **htop** as it's my preferred tool for checking resource use in addition to commands like **top**, **free -h** etc...<br>
<br>

![Screenshot 2024-03-21 094804](https://github.com/Benrosan/Detection-Lab/assets/160042310/88a67d77-7236-43a0-8fb6-148234a8d5ed)

<br>

**4.** Installed Sysmon for more detailed event/log capture. It's interesting to note that configuration files for Sysmon can vary greatly and are absolutely essential to security event logging within both Windows and the SIEM. I used Olaf Hartong's <a href="https://github.com/olafhartong/sysmon-modular">config file</a><br>

<br>

![Screenshot 2024-03-21 111708](https://github.com/Benrosan/Detection-Lab/assets/160042310/b9443f7b-2231-4f67-81c1-a7dd0b7a07c0)

<br>

**5**. After installing the Wazuh manager, I installed my Wazuh manager on my chosen endpoint. This was done quickly via PoweShell script. I then confirmed the service was running on the host.<br>

<br>

![2024-03-21 11_19_53-Services](https://github.com/Benrosan/Detection-Lab/assets/160042310/903e80ea-2b18-46a2-ad6b-423796488bac)

**6.** Next step was to update the config file for Wazuh to have it ingest the Sysmon logs.<br>

![2024-03-21 11_29_11-ossec conf - Notepad](https://github.com/Benrosan/Detection-Lab/assets/160042310/b41c2d29-c4d0-486d-8bf7-ee6d95678a0e)

I then restarted the Wazuh service and confirmed the logs were appearing in the Wazuh dashboard.<br>

![2024-03-21 11_33_48-Wazuh - Wazuh](https://github.com/Benrosan/Detection-Lab/assets/160042310/b811216d-4042-4747-955b-cd2b9d82d049)

**7.** Next step was to create a custom rule within Wauzh to track a specific event: the launch of the Mimikatz executable (which I had downloaded on my host).<br>

![Screenshot 2024-03-21 094017](https://github.com/Benrosan/Detection-Lab/assets/160042310/5732f07e-6544-4a2c-9c27-d27e78fd173d)

It's was interesting to learn more about how custom rules are created, but also how certain threats are classified based on the MITRE Att&ck Framework, which is something I studied as part of my CompTia Security+ certification.<br>

**8.** It was now time to move on the the SOAR platform and start connection all the pipes i.e. the flow from Wazuh > RegEx > TotalVirus > TheHive. I created the workflow below as part of that exercise.<br>

![Screenshot 2024-03-21 084603](https://github.com/Benrosan/Detection-Lab/assets/160042310/05c1af6a-ac3d-4f34-ae6c-395322f5a6cc)

This was a great opportunity to learn more about key aspects of platform security and management including:<br>
###
   -**Webhooks**  Event Triggering, GET/POST request, JSON<br>
   -**APIs**: self-explanatory. It was nice getting hands-on experience generating and implementing API keys as part of the workflow.<br>
   -**RegEx**: i.e. matching strings with patterns. Used to pass along the output of the releveant SHA256 hash to VirusTotal.

![Screenshot 2024-03-21 084701](https://github.com/Benrosan/Detection-Lab/assets/160042310/174638f9-b521-46b2-a382-062a036737e6)<br>

The trickiest part of the setp was configuring TheHive to properly generate the alerts. The JSON inputs had to be precisely formatted.<br>

![2024-03-21 12_19_58-Workflow - SOC Automation Project](https://github.com/Benrosan/Detection-Lab/assets/160042310/1b1c14f6-986a-4980-9e5c-c626e304bf24)

<br>

After some troubleshooting, I was eventually able to get the workflow to work properly and generate the necessary alerts in TheHive.
<br>

![Screenshot 2024-03-21 090215](https://github.com/Benrosan/Detection-Lab/assets/160042310/979282f2-cbed-4283-9b86-154b69e21561)

At this point of I have a fully functioning workflow that sends alerts to TheHive when I launch Mimikatz on my local device. 

### Next Steps

- As the diagram show, the next steps are to continue to work in Shuffle/Wazuh to created an automated response to the threat. At this point however, I feel it would be more beneficial to continue to explore the capabilities of the Wazuh platform and continue to hone skills around log/event analysis, as I feel it's more relevant to a Level 1 SOC Analyst position.
- While working on the above, I'm also going to start familiarizing myself with Wireshark and deepen my knoweledge of PCAPs and network log analysis.







