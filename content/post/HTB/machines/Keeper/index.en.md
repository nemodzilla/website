---
title: Keeper [Unlocked]
description: HTB Machines
slug: KeeperHTB
date: 2024-01-28 00:00:00+0000
image : assets/Keeper.png
categories:
    - HackTheBox
tags:
    - HackTheBox
---

[Link to the machine](https://app.hackthebox.com/machines/Keeper)

![Login.html](assets/proxy.png)

Burpsuite -> Send to intruder -> Intruder -> Positions -> Attack type (Cluster bomb)

In the request, highlight the username value and click Add § to mark it as a payload position. Same for the password.

The Payload tab -> Load username txt -> Payload set (2) -> Load pass.txt

![Status code 302](assets/results.png)
<<<<<<< HEAD
=======

![lnorgaard password](assets/lnorgaard.png)

```bash
 ssh lnorgaard@10.10.11.227
```

![user flag](assets/userFlag.png)

Unzip

![Unzip](assets/zip.png)

Launch python server on ssh session to dl files

![Unzip](assets/pythonServer.png)

Dl the keepassXC dmp.

Download this repository :

https://github.com/vdohney/keepass-password-dumper

Put the dmp file in it.

Install dotnet (7.0), on Debian kernel :

https://learn.microsoft.com/en-us/dotnet/core/install/linux-debian

```bash
 dotnet run KeePassDumpFull.dmp
```

![DB password](assets/dotnet.png)

Seems to be a dessert : Rødgrød med fløde

try unlock passcodes.kdbx with **rødgrød med fløde**

![PPK key](assets/keepass.png)

Copy the key in txt file.

```bash
 puttygen key.txt -O private-openssh -o id_rsa
```

Connect :

```bash
 ssh -i id_rsa root@10.10.11.227
```

![root flag](assets/root.png)
