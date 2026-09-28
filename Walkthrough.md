# ICA: 1 Full Walk-Through

I designed this walk through to document my full process including dead ends and where i got stuck

## Recon of the Target Machine
### From indirect reconnaissance i found the following information
- sudo arp-scan -l exposed the target machine IP (10.0.2.14)
- at http://10.0.2.14 a publicly exposed website that was running a database service called qdPM with a login page and password recovery page
![Alt text](/Images/LoginPage.png?raw=true "loginpage")
- looking for typical files such as /Readmme.txt or Robots.txt i found a read me file with the following information with an email 'support@qdPM.net'. This mostly indicates that we may be looking for a known vulnerability related to qdPM. the robots.txt file was available but was disallowed </br>
![Alt text](/Images/ICA1_Readme.png?raw=true "Readme.txt")

### From More Direct Reconnaissance ###
- nmap displayed the following ports and versions
![Alt text](/Images/Nmap.png?raw=true "Readme.txt")

- Key Findings:
  - SSH on port 22 (OpenSSH 8.4p1)
  - HTTP on port 80 (Apache 2.4.48)
  - MySQL on port 3306 and 33060
  - Title on port 80: "qdPM | Login"
  - Page title indicates qdPM application
- next i used dirsearch as so 'dirsearch -u http://10.0.2.14' with the following results
![Alt text](/Images/InitialDirsearch.png?raw=true "Readme.txt")
- most notable to me was the directories /backups/, /install/ and ,/uploads/ however most of these were dead ends and i will include more details from here in ./lessons-learned.md
