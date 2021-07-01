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

![Nmap screenshot](/images/nmap_scan)

From the results we see that we have an Apache web server running on port 80 and Redis 6.0.7  on port 6379.

## Vulnerability Identification

1. Port 80 running Apache web server

Visiting the web application on http://10.10.131.41:80, displayed a standard Apache landing page. Nothing was revealed by examining the source code

[Web Application on Port 80](/images/web_application)

Next I ran a directory scan using Dirbuster to look for any hidden directories or files. but no hidden directories was found.

[web directory enumeration screenshot](/images/dirbuster)

Moving on to next open port 6379 and enumerating the Redis service.

2. Port 6379 running Redis 6.0.7

After researching on Redis, I found out following issues that could be exploited.
* By default Redis can be accessed without credentials
* Using Redis we could write a webshell, if we know the directory path of the web application.

To access Redis on 10.10.131.41, I installed redis-tools on my kali machine

```sudo apt-get install redis-tools```

[redis_tools installation screenshot](/images/redis_tools)

[redis connect screenshot](/images/connect_redis)

[redis info screenshot](/images/info_redis)

Checking the webpage, I found that it works.

[Webshell execution screenshot](/images/webshell_execution)

Make a netcat connection to the attacker IP

```10.10.131.41/shell.php?c=nc -e /bin/bash -lnvp 8888```

[access screenshot](/images/user)

###Privilage Escalation
[suid screenshot](/images/xxd_0)
[xxd screenshot](/images/xxd)

local user password hash from /etc/shadow file
[password hash screenshot](/images/shadow)

John the ripper to crack the password
[password cracked screenshot](/images/john)

Root access
[sudo screenshot](/images/root_access)







