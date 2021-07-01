# Res - Tryhackme Writeup

Res is a vulnerable machine on TryHackMe. Though this machine, I was introduced to Redis (Remote Dictionary Server). It is the most popular key:value store for use as database, cache or queue. Redis is totally insecure to let it be exposed over network. Redis does not have access control implementation and also it does not support encryption.

# Walkthourgh  - Table of Contents

- [Reconnaissance](#Reconnaissance)
- [Vulnerability Identification](#Vulnerability-Identification)
- [Exploitation](#Exploitation)
- [Post-Exploitation](#Post-Exploitation)

*P.S. In my walkthrough, I have two different IP's for Res vulnerable machine. When I was working through this activity, the time on the vulnerable machine expired and I had to restart it. Hence two IPs (10.10.131.41 and 10.10.47.158).*

## Reconnaissance

Nmap scan to find out the open ports and services

```nmap -sV  -sC -p- 10.10.131.41```

