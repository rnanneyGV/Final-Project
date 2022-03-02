# Network Forensic Analysis Report

## Time Thieves

You must inspect your traffic capture to answer the following questions:

- What is the domain name of the users' custom site? **Frank-n-Ted.com**

![Frank-n-Ted](https://user-images.githubusercontent.com/88005785/156288018-d2e75263-bab3-4082-87d8-0d726860f29c.png)

- What is the IP address of the Domain Controller (DC) of the AD network? **10.6.12.12 (Frank-n_Ted-DC)**

![Domain Controller](https://user-images.githubusercontent.com/88005785/156288040-e54a6915-f5e1-4df2-8e75-4871ae791f43.png)

- What is the name of the malware downloaded to the 10.6.12.203 machine? **june11.dll**

![June download](https://user-images.githubusercontent.com/88005785/156288145-db5593fb-21c5-4811-8285-335d03b7a8af.png)

Once you have found the file, export it to your Kali machine's desktop.
Upload the file to VirusTotal.com.

- What kind of malware is this classified as? **A Trojan Horse**

![VirusTotal](https://user-images.githubusercontent.com/88005785/156288060-cec94bc7-f40d-4210-92ea-64a2e48f060a.png)

## Vulnerable Windows Machine

Find the following information about the infected Windows machine:

- Host name: **Rotterdam-PC**
- IP address: **172.16.4.205**
- MAC address: **00:59:07:b0:63:a4**

![Rotter](https://user-images.githubusercontent.com/88005785/156290420-886983ed-22c0-4b33-b02e-3020bdfe5775.png)

- What is the username of the Windows user whose computer is infected? **matthijs.devries**

![matthijs](https://user-images.githubusercontent.com/88005785/156289435-b65a0a97-4728-47b2-9980-33a535649650.png)

- What are the IP addresses used in the actual infection traffic? **Source: 172.16.4.205 Dest: 205.185.216.10**

(infection traffic)

## Illegal Downloads
Find the following information about the machine with IP address 10.0.0.201:

- MAC address: **00:16:17:18:66:c8**

![Illegal MAC](https://user-images.githubusercontent.com/88005785/156288490-fd36276e-77e4-486e-b8ef-aabeae135ca4.png)

- Windows username: **elmer.blanco**

![elmer](https://user-images.githubusercontent.com/88005785/156289665-ba1cc145-a6ff-423c-9f39-5be4ffd7910c.png)

- OS version: **Windows 10.0; win 64**

- Which torrent file did the user download? **Betty Boop Rhythm on the Reservation** 

![Betty](https://user-images.githubusercontent.com/88005785/156288639-98e9a969-0fef-4360-8766-64c4a77527b5.png)
