TEST


Recon

1. NMAP Scan
nmap -sV -sC -p- <ip>

This scan will return the ports 53, 1337.
It shows that port 1337 is running an Apache server, a popular attack surface. 
Visting the page, we get exposed. 

Running gobuster on the site was the next step so that we can map out any other pages. 
Running 
gobuster dir -u http://<ip>:1337/ -w /usr/share/wordlists/dirbuster/<regular> returned 

admin.
admin_101. 
phpmyadmin.

admin_101 had a filled in username: thm@thm.com which would make it much easier brtue force. 
phpymyadmin was exposed which uses mysql on the backend and the description of the challenge hints at using mysql. 

We need to provide mysql with some information so that it can dump the database; intercepting the request traffic in burupsuite, saving as a file and running
sqlmap req --dump revealed additional pages and two passwords. 

<What does sqlmap do?>


2. 
3. Found Ports
4. Gobuster
5. SQL MAP

SQL MAP returned two passwords.
1. easytohack
2. hard password
3. one user in the database thm.


User access to Z with reverse shell, SSH creds 
Escalate Privs to root using SUID bit on nano 
modify the /etc/passwd file to remove the X.

https://unix.stackexchange.com/questions/76313/change-password-of-a-user-in-etc-shadow
https://www.redhat.com/sysadmin/suid-sgid-sticky-bit
https://gtfobins.github.io/gtfobins/nano/#limited-suid
https://www.kali.org/tools/peass-ng/

Blue Team Perspective
