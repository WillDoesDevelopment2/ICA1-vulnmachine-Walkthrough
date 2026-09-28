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

