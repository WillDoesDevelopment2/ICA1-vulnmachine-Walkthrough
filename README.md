## ICA 1 VulnHub Vulnerable Machine Walk-through 

Platform: VulnHub Status: Completed Difficulty: Easy Medium Completed: September 2026
A vulnerable machine practice focusing on web application security, credential harvesting, and Linux privilege escalation via PATH hijacking.

## Machine Information

Machine Name: ICA 1 
Author: onurturali Release 
Date: September 25, 2021 
Download Link: https://www.vulnhub.com/entry/ica-1,748/ 
Target IP In my Documentation: 10.0.2.14 
Completion Date: September 17, 2026 Time to 
Complete: Approximately 6 hours 
Difficulty Rating: Easy Medium

## Tools Used

Nmap: Port scanning and service enumeration 
Dirsearch: Web directory brute-forcing 
Nikto: Web vulnerability scanning 
SQLMap: SQL injection automation Metasploit Framework: Exploit searching 
Hydra: Credential brute-forcing 
MySQL Client: Database interrogation 
Base64: Password decoding 
Strings: Binary inspection 
Vim: PATH hijacking payload creation

## Vulnerabilities Exploited

Open MySQL Ports: Database accessible via network (3306, 33060) 
Exposed Configuration File: databases.yml publicly readable 
Hardcoded Credentials: DB username and password in plaintext YAML 
Weak Password Hashing: Base64 encoding instead of proper encryption 
SUID Binary Misconfiguration: /opt/get_access without absolute paths 
PATH Hijacking: Exploitable non-absolute path in SUID binary for root escalation

## Attack Path Summary

Initial reconnaissance with Nmap identified open ports (22, 80, 3306, 33060) 
Web enumeration via Dirsearch located /install/, /core/, /uploads/ directories 
Nikto flagged outdated Apache 2.4.48 version Sensitive file /core/config/databases.yml exposed database credentials 
MySQL login achieved with harvested credentials Database query extracted user credentials encoded in Base64 
Decoded passwords matched to usernames in staff table SSH access gained using Travis credentials 
Privilege escalation via SUID binary and PATH hijacking 
Both user.txt and root.txt flags captured

## Repository Contents

walkthrough.md: Step-by-step methodology with commands 
lessons-learned.md: Where I got stuck and recovery strategies 
screenshots/: Proof of access with sensitive data redacted

## Skills Demonstrated

Network reconnaissance and service fingerprinting 
Web application security assessment Sensitive file discovery and exposure analysis 
Database interrogation and credential extraction 
Password decoding and credential matching SSH access with harvested credentials 
Linux post-exploitation with SUID binaries 
Privilege escalation via PATH hijacking 
Technical documentation and reporting

## Disclaimer

This machine is from VulnHub and intended for educational purposes only. All techniques were performed in a locally controlled authorized environment using a VirtualBox VM at 10.0.2.14. Unauthorized testing on production systems is illegal and unethical.
This walkthrough respects the VulnHub community by intentionally omitting full flags and sensitive credentials in linked files to preserve learning value for other learners.

## Contact
GitHub: @yourusername LinkedIn: Your Profile Email: your.email@example.com
Last Updated: September 25, 2026
