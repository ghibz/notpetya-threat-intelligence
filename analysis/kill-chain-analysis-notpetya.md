# Cyber Kill Chain *NotPetya*

## 1. Reconnaissance - What has the attacker researched beforehand ?

**What is this phase**
The initial phase in which the attacker gathers intelligence on the victim/target. This is extremely important as it can lead to identifying key vulnerabilities which can later be exploited. There are mainly two types of reconnaissance; the first one being **Passive Reconnaissance** in which the attacker gathers data without directly interacting with the system, e.g publicly available data such as social media pages, websites, databases. The other type is **Active Reconnaissance** where the attacker tests the ground directly on the system, through Network Scanning (nmap) or Web Vulnerabilities (outdated software or SQL injection points).

**What happened in the context of NotPetya**
The **Reconnaissance** phase in the context of NotPetya is probably the least descriptive phase in terms of available information that we have. This is because **Sandworm**, the group responsible for this is part of the GRU, a cyberwarfare unit of Russia's military intelligence service, making their tracks very hard to detect. What we know however, is that **Sandworm** had been very active in the hacking of Ukraine's power grids, making it obvious that they have had **Long-term Strategic Recon** over the landscape and infrastructure of Ukraine's institutions. 

There is however, more information regarding NotPetya which we can place in the Reconnaissance phase, and that is, the **Operational Recon in M.E.Doc**. Once **Sandworm** had infiltrated **Linkos Group** servers (the developers of M.E.Doc), they had several weeks of studying the victim's networks, mapping the systems and accounts they would target as well as identifying SCCM/AD (System Center Configuration Manager, now known as Microsoft Endpoint Configuration Manager, and Active Directory) credentials, which would later be used in the following phases.

**Tools/Techniques used**

**Detection Opportunity (What could have been done)**

## 2. Weaponisation - What malicious weapon have they built ? 

**What is this phase**
In this phase, the attackers start to develop the malicious payload, based on the vulnerabilities identified in the **Reconnaissance** phase. The most common sub-steps in this phase include the actual **Malware Development** in which the malware is tailored based on the victim environment, leveraging existing exploits. The next step is **Payload Delivery** in which the attackers decide the means in which the payload will be delivered into the target systems, which can be either email attachments, links or removable media (USB).

**What happened in the context of NotPetya**
In the **Weaponisation** phase of NotPetya, **Sandworm** engineered a single payload binary, which included already existing exploitation and encryption techniques. This binary included a modified version of **Mimikatz** (Benjamin Delpy; built it for research in Windows security, showcasing its vulnerabilities, later to be maliciously altered and used by **Sandworm**), for credential harvesting, embedded exploit code of EternalBlue (CVE-2017-0144) and EternalRomance (CVE-2017-0145) for later network propagation, and a **'triple threat'** encryption as CrowdStrike calls it, in which AES-128 encryption is used for normal files, MFT (Master File Table) encryption, making the operating system not know where any file is located, and MBR (Master Boot Record) overwrite, where the first sector of the hard drive, telling the computer where to find the OS, was replaced with **Sandoworm's** own version, which would show the popular black/red ransomware message screen. The payload also include calls to Windows administration tools such as PsExec and WMIC (Windows Management Instrumentation Command-line).

**Tools/Techniques used**

**Detection Opportunity (What could have been done)**

## 3. Delivery - How did the payload reach the target ? 

**What is this phase**
Delivery is the phase where the attacker delivers the weaponised malware via different ways. Some include; **Phishing Emails** with malicious attachments which trick the company employee into downloading it or providing their user credentials; **Malicious Links**, which are URLs designed to lead the victim onto compromised websites and/or drive-by downloads of malware; and lastly, **Removeable Media**, such as USBs where the weaponised payload it planted onto these, and then plugged into the victim's system physically by either the attacker or more commonly an employee (either knowingly or unknowingly).

**What happened in the context of NotPetya**

**Tools/Techniques used**

**Detection Opportunity (What could have been done)**

## 4. Exploitation - What vulnerabilities and mechanisms were triggered ? 

**What is this phase**
The exploitation phase takes place when the malicious payload is successfully delivered, taking advantage of a potential vulnerability and allowing the attacker to gain access to the system, officially making it compromised. It is the entry point of the attacker, and not much can be done after this phase, but to mitigate further damage.

**What happened in the context of NotPetya**

**Tools/Techniques used**

**Detection Opportunity (What could have been done)**

## 5. Installation - How did the malware establish itself on the system ? 

**What is this phase**
This attacker's aim in this phase is to gain **Persistence**. They have already penetrated the system and now they have to make their presence persistence via different ways so that they do not lose this access. This can be done via **Trojan Malware**, which would allow the attacker remote access to the system, while disguising itself as legitimate software. Another way would be to use a **Rootkit**, a piece of malware that would give the attacker administrative access, while hiding malicious activities from detection.

**What happened in the context of NotPetya**

**Tools/Techniques used**

**Detection Opportunity (What could have been done)**

## 6. Command and Control - How did the attacker communicate with the infected machines ? 

**What is this phase**
By this phase, the attacker would already have persistence over multiple systems within the compromised company, and now they will attempt to build a channel, between their C2 server, to the systems, as a way of communicating with them; sending commands instructing the malware what to do and at the same time, receiving data, such as compromised user credentials and other sensitive information. This is the second phase in which further **Persistence** is built up, making sure that even after reboots and updates, the attacker will still have a way of accessing the target.

**What happened in the context of NotPetya**

**Tools/Techniques used**

**Detection Opportunity (What could have been done)**

## 7. Actions on Objectives - What was the end goal ? What have they achieved in the end ?

**What is this phase**
This is the final phase of the cyber kill chain. This is where the attacker would make their final move, executing their malicious plan to the end. The final objective(s) could be varied and include things such as data exfiltration, permanent destruction of data or even further later movement to other systems. The actual reason for these actions include: financial gain, espionage or simply sabotage.

**What happened in the context of NotPetya**

**Tools/Techniques used**

**Detection Opportunity (What could have been done)**
