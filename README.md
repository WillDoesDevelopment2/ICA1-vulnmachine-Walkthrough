## ICA 1 VulnHub Vulnerable Machine Walk-through 

Platform: VulnHub Status: Completed Difficulty: Easy Medium <br/>
Completed: September 2026<br/>
A vulnerable machine practice focusing on web application security, credential harvesting, and Linux privilege escalation via PATH hijacking.

## Machine Information

Machine Name: ICA 1 <br/>
Author: onurturali Release <br/>
Date: September 25, 2021 <br/>
Download Link: https://www.vulnhub.com/entry/ica-1,748/ <br/>
Target IP In my Documentation: 10.0.2.14 <br/>
Completion Date: September 17, 2026 Time to <br/>
Complete: Approximately 6 hours <br/>
Difficulty Rating: Easy Medium

## Tools Used

Nmap: Port scanning and service enumeration<br/> 
Dirsearch: Web directory brute-forcing <br/>
Nikto: Web vulnerability scanning <br/>
SQLMap: SQL injection automation Metasploit Framework: Exploit searching<br/> 
Hydra: Credential brute-forcing <br/>
MySQL Client: Database interrogation <br/>
Base64: Password decoding <br/>
Strings: Binary inspection <br/>
Vim: PATH hijacking payload creation

## Vulnerabilities Exploited

Open MySQL Ports: Database accessible via network (3306, 33060) <br/>
Exposed Configuration File: databases.yml publicly readable <br/>
Hardcoded Credentials: DB username and password in plaintext YAML <br/>
Weak Password Hashing: Base64 encoding instead of proper encryption <br/>
SUID Binary Misconfiguration: /opt/get_access without absolute paths <br/>
PATH Hijacking: Exploitable non-absolute path in SUID binary for root escalation

## Attack Path Summary

Initial reconnaissance with Nmap identified open ports (22, 80, 3306, 33060) <br/>
Web enumeration via Dirsearch located /install/, /core/, /uploads/ directories <br/>
Nikto flagged outdated Apache 2.4.48 version Sensitive file /core/config/databases.yml exposed database credentials<br/> 
MySQL login achieved with harvested credentials Database query extracted user credentials encoded in Base64 <br/>
Decoded passwords matched to usernames in staff table SSH access gained using Travis credentials <br/>
Privilege escalation via SUID binary and PATH hijacking <br/>
Both user.txt and root.txt flags captured

## Repository Contents

walkthrough.md: Step-by-step methodology with commands <br/>
lessons-learned.md: Where I got stuck and recovery strategies<br/> 
screenshots/: Proof of access with sensitive data redacted<br/>

## Skills Demonstrated

Network reconnaissance and service fingerprinting <br/>
Web application security assessment Sensitive file discovery and exposure analysis<br/> 
Database interrogation and credential extraction <br/>
Password decoding and credential matching SSH access with harvested credentials<br/> 
Linux post-exploitation with SUID binaries <br/>
Privilege escalation via PATH hijacking <br/>
Technical documentation and reporting

## Disclaimer

This machine is from VulnHub and intended for educational purposes only. All techniques were performed in a locally controlled authorized environment using a VirtualBox VM at 10.0.2.14. Unauthorized testing on production systems is illegal and unethical.
This walkthrough respects the VulnHub community by intentionally omitting full flags and sensitive credentials in linked files to preserve learning value for other learners.

## Contact

GitHub: @willdoesdevelopment2 <br/>
Email: JulianDelphinki01@pm.me<br/>
Last Updated: September 25, 2026
