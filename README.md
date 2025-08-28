\# SSH Remote Server Setup



This project demonstrates how to set up a remote Linux server and configure it to allow SSH access using \*\*two separate key pairs\*\*.  

The goal is to practice the basics of Linux server setup and secure authentication.



Project URL : " https://roadmap.sh/projects/ssh-remote-server-setup "



---



\## 🖥️ Server Details

\- \*\*Provider:\*\* DigitalOcean  

\- \*\*Droplet Specs:\*\* 1 vCPU, 1 GB RAM, 35 GB Disk  

\- \*\*OS:\*\* Ubuntu 25.04 x64  

\- \*\*Public IP:\*\* 129.212.177.127  



---



\## 🔑 Steps Completed



\### 1. Droplet Creation

\- Created a new DigitalOcean droplet with Ubuntu 25.04.

\- Chose \*\*password authentication\*\* for initial login.



\### 2. SSH Key Generation (on local machine)

On my \*\*Windows laptop (PowerShell)\*\*, generated two SSH key pairs:



```powershell

ssh-keygen -t rsa -b 4096 -f $HOME\\.ssh\\mykey1

ssh-keygen -t rsa -b 4096 -f $HOME\\.ssh\\mykey2



\### 3. Copy Public Keys to Server



Appended both .pub keys to the server’s authorized\_keys file:



type $HOME\\.ssh\\mykey1.pub | ssh root@129.212.177.127 "umask 077; mkdir -p ~/.ssh; cat >> ~/.ssh/authorized\_keys"

type $HOME\\.ssh\\mykey2.pub | ssh root@129.212.177.127 "cat >> ~/.ssh/authorized\_keys"

ssh root@129.212.177.127 "chmod 700 ~/.ssh \&\& chmod 600 ~/.ssh/authorized\_keys"



\### 4. Test Key-Based Authentication



Verified login with both keys:



ssh -i $HOME\\.ssh\\mykey1 root@129.212.177.127

ssh -i $HOME\\.ssh\\mykey2 root@129.212.177.127





Both worked successfully ✅.



\### 5. SSH Config Alias



Configured an alias for easy access:



File: C:/Users/bhavy/.ssh/config



Host myserver

&nbsp;   HostName 129.212.177.127

&nbsp;   User root

&nbsp;   IdentityFile C:/Users/bhavy/.ssh/mykey1





\### Now I can connect with:



ssh myserver





✅ Outcome



Two SSH key pairs generated and configured.



Server accepts both keys.



Alias ssh myserver works.



