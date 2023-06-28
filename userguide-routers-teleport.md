---
layout: default
title: Changing Routers Passwords on Teleport
description: Interns and newcommers wondered if it was already Christmas
---

![intro](images-changingpasswords-info.png)

## On this Page:

- [Actions Required](#actions-required)
- [Prerequisites](#prerequisites)
- [Creating Passwords for Stores' Routers on LastPass](#creating-passwords-for-stores-routers-on-lastpass)
- [Accessing a Server](#accessing-a-server)
- [Setting SREs SSH RSA Keys](#setting-sres-ssh-rsa-keys)
- [Bonus: Setting Server’s Time](#bonus-setting-servers-time)

## Actions Required

- Create Passwords and Sections for Servers on LastPass
- Access Servers and Change Routers Passwords
- Add SREs SSH RSA Keys to the Routers Authorized Keys
- Set Server Time

## Prerequisites

- Having a LastPass user
- Having a Teleport User
- Having Teleport installed
- Having Necessary SSH RSA Keys
- Knowing which Servers to make changes on.

## Creating Passwords for Stores' Routers on LastPass

To create a section for each store’s router password on LastPass:

1. Access Agot’s LastPass Password Manager panel.
2. Create a New Item by clicking the plus sign located at the bottom right corner. This action will open a modal where you must fill in a few fields. <br> ![createnew](images-changingpasswords-createnew.png)
3. Fill in the Name field with the server’s name.
4. Fill in the Folder field with the “Shared-stores” value.
5. Fill in the Username with “root.”
6. Create a strong password (use the LastPass' Generate Secure Password tool).
7. Copy the password and paste it into the Site password field.
8. Save this configuration by clicking Save.
9. Repeat the whole process for each of the servers listed below.

![createnew2](images-changingpasswords-createnew2.png)

## Accessing a Server

To access a server:

1. List the existing servers by running: <br>
`tsh ls` <br>
   You will see all servers listed as shown next

![servers](images-changingpasswords-serverslist.png)

2. Select a server and access it:<br>
`tsh ssh doxhut@doxhut-2-xavier-0` (example)

3. Then, access the router:<br>
`ssh root@192.168.1.1`

4. Once in the router, change its password by running:<br>
`passwd`

5. You will get a confirmation message and that’s it!<br>

## Setting SREs SSH RSA Keys

To set an SREs SSH RSA key in the router:<br>

1. Run:<br>
`cd /root`

2. List all directories:<br>
`ls -hal`

3. Open .ssh<br>
`cd .ssh`

4. Then, edit the authorized keys<br>
`vim authorized_keys`

5. Once on the **Vim editor**, press **“i”** to activate the editor mode.<br>

6. Paste one of the SSH RSA keys.<br>

7. Press **“Esc”** to exit edit mode.<br>

8. Press **“o”** to jump into the next line.<br>

9. Press **“i”** to activate the editor mode and paste a second key.<br>

10. Repeat as many times as keys you must insert in the file.<br>

11. Finally, make sure you are not in the editor mode, and press **“:wq”** to save changes and quit. <br>

## Bonus: Setting Server’s Time

Since you are already on the server, use the chance to set the server’s time by running:

`uci set system.ntp.enable_server='1' ; uci commit system ; /etc/init.d/sysntpd restart`

> 💡 **Note**: You will not get any confirmation message for this last step.

