# ICA: 1 Full Walk-Through

I designed this walk through to document my full process including dead ends and where i got stuck

## Recon of the Target Machine
### From indirect reconnaissance i found the following information
- sudo arp-scan -l exposed the target machine IP (10.0.2.14)
- at http://10.0.2.14 a publicly exposed website that was running a database service called qdPM with a login page and password recovery page. Note the qdPM version (9.2) is displayed publicly at the bottom
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
- most notable to me was the directories /backups/, /install/ and ,/uploads/ however most of these were dead ends and i will include more details from here in [./lessons-learned.md](https://github.com/WillDoesDevelopment2/ICA1-vulnmachine-Walkthrough/blob/main/lessons-learned.md)

## Searching Exploits Per Version
- I conducted many searches listed in [./lessons-learned.md](https://github.com/WillDoesDevelopment2/ICA1-vulnmachine-Walkthrough/blob/main/lessons-learned.md) however i will show the exploit that was crucial. As suspected earlier, qdPM version 9.2 with a brief search on exploit-db has 2 known exploits, one of which is an exposed plaintext username and password for the sql database
- link to exploit https://www.exploit-db.com/exploits/50176
- here we can simply write in the terminal curl http://10.0.2.14/core/config/databases.yml or the same web address in your chosen browser</br>
![Alt text](/Images/CurlYmlFile.png?raw=true "Curl Yml File")

## Initial Access to mySQL on port 3306 
- using a simple mySQL command i was able to authenticate with the stolen credentials and navigate through the SQL database as so.
![Alt text](/Images/MySqlLogIn.png?raw=true "Curl Yml File")
- looking into the password file we can see some encoded passwords, It looks like most likely these are in base64. After some decoding using the command 'echo "<encoded_password>" | base64 -d ' i was able to retrieve some password log in pairs to use on the ssh port.

## Initial Access to the Target Device
-I initially found dexter's login pair however there was no flag, but there was a clue indicating how to escalate privilege
![Alt text](/Images/DexterLogin.png?raw=true "Curl Yml File")
- after getting lost yet again looking into files such as the initrd.img as discussed in [./lessons-learned.md](https://github.com/WillDoesDevelopment2/ICA1-vulnmachine-Walkthrough/blob/main/lessons-learned.md), i found i had the working password for Travis who had the user.txt flag! Yey
![Alt text](/Images/TravisLogIn.png?raw=true "Curl Yml File")
- Now on to Escalating privilege for the root flag

## Privilege Escalation

-  for this machine it seems that path hijacking is the most common method of privilege escalation most likely because it is the most simple and effective method for gaining root privilege. Below is my method for checking files with set User ID bits set, checking if the file was created by a root user, and then using strings to find any human readable content that doesn't use an absolute path
![Alt text](/Images/PathHijackSearch.png?raw=true "Curl Yml File")
- as we can see cat/root/system.info looks promising! Seems that Dexter's note from earlier was helpful! We can now start looking into creating an identical path that will be checked first before the actual cat file.
- 
