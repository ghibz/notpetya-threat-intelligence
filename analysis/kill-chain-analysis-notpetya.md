# Cyber Kill Chain *NotPetya*

## 1. Reconnaissance - What has the attacker researched beforehand ?

### **What is this phase**
The initial phase in which the attacker gathers intelligence on the victim/target. This is extremely important as it can lead to identifying key vulnerabilities which can later be exploited. There are mainly two types of reconnaissance; the first one being **Passive Reconnaissance** in which the attacker gathers data without directly interacting with the system, e.g publicly available data such as social media pages, websites, databases. The other type is **Active Reconnaissance** where the attacker tests the ground directly on the system, through Network Scanning (nmap) or Web Vulnerabilities (outdated software or SQL injection points).

### **What happened in the context of NotPetya**
The **Reconnaissance** phase in the context of NotPetya is probably the least descriptive phase in terms of available information that we have. This is because **Sandworm**, the group responsible for this is part of the GRU, a cyberwarfare unit of Russia's military intelligence service, making their tracks very hard to detect. What we know however, is that **Sandworm** had been very active in the hacking of Ukraine's power grids, making it obvious that they have had **Long-term Strategic Recon** over the landscape and infrastructure of Ukraine's institutions. 

There is however, more information regarding NotPetya which we can place in the Reconnaissance phase, and that is, the **Operational Recon in M.E.Doc**. Once **Sandworm** had infiltrated **Linkos Group** servers (the developers of M.E.Doc), they had several weeks of studying the victim's networks, mapping the systems and accounts they would target as well as identifying SCCM/AD (System Center Configuration Manager, now known as Microsoft Endpoint Configuration Manager, and Active Directory) credentials, which would later be used in the following phases.

### **Tools/Techniques used**
* Passive Reconnaissance (over the previous attacks in Ukraine)
* Identification of M.E.Doc as highly valuable target
* Network / Infrastructure mapping/reconnaissance of Linkos Group's update servers

### **Detection Opportunity (What could have been done)**

## 2. Weaponisation - What malicious weapon have they built ? 

### **What is this phase**
In this phase, the attackers start to develop the malicious payload, based on the vulnerabilities identified in the **Reconnaissance** phase. The most common sub-steps in this phase include the actual **Malware Development** in which the malware is tailored based on the victim environment, leveraging existing exploits. The next step is **Payload Delivery** in which the attackers decide the means in which the payload will be delivered into the target systems, which can be either email attachments, links or removable media (USB).

### **What happened in the context of NotPetya**
In the **Weaponisation** phase of NotPetya, **Sandworm** engineered a single payload binary, which included already existing exploitation and encryption techniques. This binary included a modified version of **Mimikatz** (Benjamin Delpy; built it for research in Windows security, showcasing its vulnerabilities, later to be maliciously altered and used by **Sandworm**), for credential harvesting, embedded exploit code of EternalBlue (CVE-2017-0144) and EternalRomance (CVE-2017-0145) for later network propagation, and a **'triple threat'** encryption as CrowdStrike calls it, in which AES-128 encryption is used for normal files, MFT (Master File Table) encryption, making the operating system not know where any file is located, and MBR (Master Boot Record) overwrite, where the first sector of the hard drive, telling the computer where to find the OS, was replaced with **Sandoworm's** own version, which would show the popular black/red ransomware message screen. The payload also include calls to Windows administration tools such as PsExec and WMIC (Windows Management Instrumentation Command-line).

### **Tools/Techniques used**
* Development of the *ZvitPublishedObjects.dll* backdoor module, into M.E.Doc's *IsNewUpdate* function
* Integration of EternalBlue and EternalRomance
* Integration of modified Mimikatz component
* Integration of AES-128 and MFT encryption
* Development of MBR-overwriting payload
* Development of fake ransomware screen for misdirection

### **Detection Opportunity (What could have been done)**

## 3. Delivery - How did the payload reach the target ? 

### **What is this phase**
Delivery is the phase where the attacker delivers the weaponised malware via different ways. Some include; **Phishing Emails** with malicious attachments which trick the company employee into downloading it or providing their user credentials; **Malicious Links**, which are URLs designed to lead the victim onto compromised websites and/or drive-by downloads of malware; and lastly, **Removeable Media**, such as USBs where the weaponised payload it planted onto these, and then plugged into the victim's system physically by either the attacker or more commonly an employee (either knowingly or unknowingly).

### **What happened in the context of NotPetya**
The **Delivery** of NotPetya was quite genius of **Sandworm**; with most delivery methods of payload being malicious links or emails, or removable media and Trojan horses, **Sandworm** thought of a better way of making sure the payload reached their targets, and that is the M.E.Doc software, the leading Ukrainian accounting and finances software, a must in every company on at least one device, used to report taxes and manage invoices. With months before deploying NotPetya (believed to be in April), the hacking organization gained unauthorized access into **Linkos Group's** update servers, the developers responsible for M.E.Doc. They have managed to do this with stolen credentials from one of their employees, via what is believed to be a phishing email. Once inside the update servers, they managed to install a **backdoor** in the software package, with multiple injection attempts in the M.E.Doc updates. On June 27, once the final update took place on these devices, the malware rapidly propagated itself onto each company's network in ways that will be explained in later phases.

### **Tools/Techniques used**
* Compromised Linkos Group update server (via stolen credentials)
* Trojanised M.E.Doc update package (*actual version 10.01.189*)
* Backdoor module

### **Detection Opportunity (What could have been done)**

## 4. Exploitation - What vulnerabilities and mechanisms were triggered ? 

### **What is this phase**
The exploitation phase takes place when the malicious payload is successfully delivered, taking advantage of a potential vulnerability and allowing the attacker to gain access to the system, officially making it compromised. It is the entry point of the attacker, and not much can be done after this phase, but to mitigate further damage.

### **What happened in the context of NotPetya**
While only two true exploits (with known CVEs) have been used in this attack, there are also some other techniques worth mentioning.

1. EternalBlue (CVE-2017-0144) - exploit developed by **U.S National Security Agency (NSA)**, leaked on the Internet by hacking group known as **Shadow Brokers**. It is based on a vulnerability in the SMBv1 (Server Message Block) protocol, where a buffer overflow exploit is used to control what is sitting at specific memory locations, so when the kernel calls a function pointer, instead of legitimate code, it runs an **attacker-supplied shellcode** (with kernel-level permissions) allowing **arbitrary code execution**.
2. EternalRomance (CVE-2017-0145) - exploit developed by the same **NSA** and also leaked by **Shadow Brokers**, at the same time as **EternalBlue**. Very similarly, it also an arbitrary code execution exploit aimed at a vulnerability in SMBv1, however different in deployment. **EternalRomance** uses an exploit called **DoublePulsar**, a persistent backdoor that takes advantage of the SMB flaw to download the malware from a remote location and then allocates an internal and a public IP address to connect to the target via port 445 and deliver the payload.

It is worth noting that **NotPetya** had both of these exploits in this code, each one acting as a backup in case the other one did not succeed. The main difference between these two is that **EternalBlue** is a buffer overflow exploit, whereas **EternalRomance** is a type confusing vulnerability which leads to arbitrary code execution.

Lastly, the **Mimikatz** exploit (discovered and showcased for research purposes) has been used for credential harvesting. It takes advantage of a vulnerability of LSASS (Local Security Authority Subsystem Service), a key component of Windows' authentication process. The vulnerability is that passwords are sometimes stored, even in plaintext in the LSASS memory, and Mimikatz is able to extract it, as well as other information, making it extremely powerful for credential harvesting.

### **Tools/Techniques used**
* EternalBlue (CVE-2017-0144)
* EternalRomance (CVE-2017-0145)
* Mimikatz

### **Detection Opportunity (What could have been done)**

## 5. Installation - How did the malware establish itself on the system ? 

### **What is this phase**
This attacker's aim in this phase is to gain **Persistence**. They have already penetrated the system and now they have to make their presence persistence via different ways so that they do not lose this access. This can be done via **Trojan Malware**, which would allow the attacker remote access to the system, while disguising itself as legitimate software. Another way would be to use a **Rootkit**, a piece of malware that would give the attacker administrative access, while hiding malicious activities from detection.

### **What happened in the context of NotPetya**
Onto the **Installation** phase for NotPetya, it uses multiple invasive techniques to propagate itself into other devices. First of all it takes advantages of **PsExe**, a legitimate Microsoft Sysinternal tool, usually used by system administrators to remotely access machines and copy small executables onto them. **PsExe** was used by **Sandworm** in a malicious manner, with the administrator credentials gathered by **Mimikatz** to further deploy **NotPetya** into other devices across the network. In the case of **PsExe** not functioning as a way for NotPetya to extend, **WMIC** was used as a second option for lateral movement. **WMIC** is also a legitimate Windows tool, which can also be used to remotely copy files to other systems, and the similarly to **PsExe**, it was used with stolen credentials from **Mimikatz**. What is genius about this propagation approach from **Sandworm** is that both of these tools are completely legitimate and they were not flagged by any anti-malware/virus.

### **Tools/Techniques used**
* PsExe
* WMIC
* Windows Task Scheduler (for reboot)
* MBR overwrite

### **Detection Opportunity (What could have been done)**

## 6. Command and Control - How did the attacker communicate with the infected machines ? 

### **What is this phase**
By this phase, the attacker would already have persistence over multiple systems within the compromised company, and now they will attempt to build a channel, between their C2 server, to the systems, as a way of communicating with them; sending commands instructing the malware what to do and at the same time, receiving data, such as compromised user credentials and other sensitive information. This is the second phase in which further **Persistence** is built up, making sure that even after reboots and updates, the attacker will still have a way of accessing the target.

### **What happened in the context of NotPetya**
At first glance, NotPetya appeared to be a ransomware, demanding a payment in return for the encrypted data, however the almost complete absence of C2 infrastructure is evidence for the argument that **'NotPetya is a wiper, not a ransomware'**. A normal ransomware author would require a reliable C2 payment infrastructure, to keep their ransomware profitable, in contrast to NotPetya, which had very minimal C2, allowing researchers to quickly discover its true nature.

### **Tools/Techniques used**
* Hardcoded email address for ransom payment (non-functional)

**Detection Opportunity (What could have been done)**

## 7. Actions on Objectives - What was the end goal ? What have they achieved in the end ?

### **What is this phase**
This is the final phase of the cyber kill chain. This is where the attacker would make their final move, executing their malicious plan to the end. The final objective(s) could be varied and include things such as data exfiltration, permanent destruction of data or even further later movement to other systems. The actual reason for these actions include: financial gain, espionage or simply sabotage.

### **What happened in the context of NotPetya**
As mentioned in previous phase, NotPetya initially pretended to be a ransomware, so therefore in the eyes of the victim, the reason was financial gain, however after some attempts across Ukraine to pay the ransom, it was quickly discovered that this was just a cover-up for the real motive. Most researchers can agree that the true motive was chaos and destruction, and that NotPetya was simply a cyber-weapon for the ongoing war between Russia and Ukraine, and in the end, NotPetya was extremely successful in this regard, causing damages equal to approximately 10 billion dollars.

### **Tools/Techniques used**
* MBR-based encryption

### **Detection Opportunity (What could have been done)**
