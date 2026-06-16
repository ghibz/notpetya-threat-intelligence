# Cyber Kill Chain *NotPetya*

## 1. Reconaissance - What has the attacker researched beforehand ?

**What is this phase**
The initial phase in which the attacker gathers intelligence on the victim/target. This is extremely important as it can lead to identifying key vulnerabilities which can later be exploited. There are mainly two types of reconaissance; the first one being **Passive Reconaissance** in which the attacker gathers data without directly interacting with the system, e.g publicly available data such as social media pages, websites, databases. The other type is **Active Reconaissance** where the attacker tests the ground directly on the system, through Network Scanning (nmap) or Web Vulnerabilities (outdated software or SQL injection points).

**What happened in the context of NotPetya**

**Tools/Techniques used**

**Detection Opportunity (What could have been done)**


## 2. Weaponisation - What malicious weapon have they built ? 

**What is this phase**
In this phase, the attackers start to develop the malicious payload, based on the vulnerabilities identified in the **Reconaissance** phase. The most common sub-steps in this phase include the actual **Malware Development** in which the malware is tailored based on the victim environment, leveraging existing exploits. The next step is **Payload Delivery** in which the attackers decide the means in which the payload will be delivered into the target systems, which can be either email attachments, links or removeable media (USB).

**What happened in the context of NotPetya**

**Tools/Techniques used**

**Detection Opportunity (What could have been done)**

## 3. Delivery - How did the payload reach the target ? 

**What is this phase**
Delivery is the phase where the attacker delivers the weaponised malware via different ways. Some include; **Phishing Emails** with malicious attachments which trick the company employee into downloading it or providing their user credentials; **Malicious Links**, which are URLs designed to lead the victim onto compromised websites and/or drive-by downloads of malware; and lastly, **Removeable Media**, such as USBs where the weaponised payload it planted onto these, and then plugged into the victim's system physical by either the attacker or more commonly an employee (either knowingly or unknowingly).

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
