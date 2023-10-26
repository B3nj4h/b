---
layout: post
title: Nmap Scanning Techniques
date: '2023-10-26 12:35:11 +0300'
image: /assets/img/cover_images/37.png
categories: [Pentesting, Nmap]
tags: [Nmap]
---
## Nmap

## Services and their versions
```
nmap -sV [ip]
```
## List of targets
```
nmap -iL targets.txt
```
## Service with Os detection
```
nmap -sV -O [ip]
```
## Fast mode
```
nmap -sV -F -O [ip]
```
## Aggressive scan
```
nmap -A [ip]
```
## Scripting engine
```
nmap -sC [ip]
nmap --script=default vuln [ip]
nmap --script vuln [ip]
```
## Service detection with script engine
```
nmap -sV -sC [ip]
```
## Tcp scan on all ports
```
nmap -sT -p- [ip]
```
## UDP aggressive scan
```
nmap -sU -T4 [ip]
```
## Most common ports in fast mode
```
nmap --top-ports 100 -F [ip]
```
## Firewall and IDS evasion
```
nmap -sS -T1 -F [ip]
nmap -sS -T1 [ip]
nmap -FN -T1 [ip]
nmap -D ip1,ip2,RND,RND,yourip [target_ip]
nmap -sV --scripts-args https.useragent="" [ip]
```
## Spoofed scan
```
nmap -e eth0 -Pn -S spoofed_ip [target_ip]
```
## Scanning speed
```T1``` is the slowest but the best to avoid IDS alerts, also ```T2```. ```T3``` is the normal one for Nmap.```T4``` is used for ctf's or when learning to scan with nmap.```T5``` is fast but has low accuracy due to packet loss.
```
--min-rate [number]
--max-rate [number]
```
can also be used as an alternative to specify the number of packets to be send per second
## Detecting Firewalls
If we get filtered fron the Null, FIN, XMAS scan it means firewalls are present. In Null scan 0 flags are set to 1. FIN Scan 1 flag is set to 1 and Xmas scan 3 are set to 1.
```
nmap -sN [ip]
nmap -sF [ip]
nmap -sX [ip]
```