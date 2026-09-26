# ICA: 1 Full Walk-Through

I designed this walk through to document my full process including dead ends and where i got stuck

## Recon of the Target Machine
### From indirect reconnaissance i found the following information
- sudo arp-scan -l exposed the target machine IP (10.0.2.14)
- at http://10.0.2.14 a publicly exposed website that was running a database service called qdPM
- looking for typical files such as /Readmme.txt or Robots.txt i found a read me file with the following information</br>
![Alt text](/Images/ICA1_Readme.png?raw=true "Readme.txt")
