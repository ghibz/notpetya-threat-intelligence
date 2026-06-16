# notpetya-threat-intelligence
Threat Intelligence Analysis - NotPetya (2017) - Cyber Kill Chain / Diamond Model / MITRE ATT&amp;CK

1. Executive Summary      

NotPetya is a cyber-weapong used by the Russian government in 2017 which was launched against multiple companies with sites in Ukraine. The payload was injected into M.E.DOC, a software application used by every company in Ukraine for taxes. Once the application was updated, it starts to encrypt files on devices, as well as the master boot record (MBR), making the OS unusable. It gave the user a ransomware screen, demanding $300 in return, however this was in vain as the purpose of the attack was not financial gain, but rather destruction. NotPetya uses some popular exploits such as MimiKatz, EternalBlue and EternalRomance, which I will go in depth below to further understand them.

2. Attribution           

NotPetya was created and deployed by Sandworm, a.k.a APT44, Telebots, Voodoo Bear etc., an APT (Advanced Persistent Threat) and cyberwarfare unit of the GRU (Russia's military intelligence service). They are known not only for the NotPetya attack, but also for others such as the Ukraine Power Grid Hacks in 2015, 2016 and 2022, the 2018 Winter Olympics disruption and others.

3. Impact & Scope          ← $10B, affected companies, Ukraine + global



4. Repository Contents     ← what files are in this repo and what each does



5. Frameworks Used         ← brief explanation of Kill Chain, Diamond, ATT&CK



6. Sources & References    

https://www.youtube.com/watch?v=3-MSlNVqzYY
https://cyber-peace.org/wp-content/uploads/2018/10/The-Untold-Story-of-NotPetya-the-Most-Devastating-Cyberattack-in-History-_-WIRED.pdf
https://www.crowdstrike.com/en-us/blog/petrwrap-ransomware-technical-analysis-triple-threat-file-encryption-mft-encryption-credential-theft/
https://medium.com/@RocketMeUpCybersecurity/the-cyber-kill-chain-analyzing-and-disrupting-attack-phases-87f045e774b4
https://www.youtube.com/watch?v=LFo2PtQlL1Y
https://socprime.com/blog/petya-a-notpetya-is-an-ai-powered-cyber-weapon-ttps-lead-to-sandworm-apt-group/
https://en.wikipedia.org/wiki/Sandworm_(hacker_group)
https://www.cisa.gov/news-events/alerts/2017/07/01/petya-ransomware
