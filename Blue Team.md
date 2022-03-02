# Blue Team: Summary of Operations

## Table of Contents

- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

## Network Topology

The following machines were identified on the network:

- Capstone
  - Operating System: Ubuntu (Linux)
  - Purpose: Vulnerable Webserver
  - IP Address: 192.168.1.105

- ELK
  - Operating System: Ubuntu (Linux)
  - Purpose: Elasticsearch and Kibana stack
  - IP Address: 192.168.1.100

- Kali
  - Operating System: Ubuntu (Linux)
  - Purpose: Attacking Machine
  - IP Address: 192.168.1.90

- Target 1
  - Operating System: Debian
  - Purpose: Target Machine hosting Wordpress
  - IP Address: 192.168.1.110.

![Network Diagram](https://user-images.githubusercontent.com/88005785/156203320-b7c225a6-7ace-49cc-a7fb-e0e67d340c30.png)

## Description of Targets

The target of this attack was the Target 1 VM (192.168.1.110).

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts, described in detail below, have been implemented:

- Excessive HTTP Errors
- HTTP Request Size Monitor
- CPU Usage Monitor

## Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

_Excessive HTTP Errors_

“Excessive HTTP Errors” is implemented as follows:

- Metric: **WHEN count() GROUPED OVER top 5 'http.response.status_code'**
- Threshold: **IS ABOVE 400 FOR THE LAST 5 minutes**
- Vulnerability Mitigated: **Enumeration and Brute Force**
- Reliability: **The alert should have high reliability. Filtering out all response codes other than those than client and server errors should focus the scope of the alert to potential malicious activity.**

_HTTP Request Size Monitor_

“HTTP Request Size Monitor” is implemented as follows:

- Metric: **WHEN sum() of http.request.bytes OVER all documents** 
- Threshold: **IS ABOVE 3500 FOR THE LAST 1 minute**
- Vulnerability Mitigated: **Code injection and distributed denial of service (DDOS)**
- Reliability: **This alert may have medium reliability. HTTP request sizes in bytes typically average in the 700-800 byte size, so it's possible the threshold of this alert is properly configured, but additional monitoring may be necessary to review the nature of HTTP requests over 3500 bytes.**

_CPU Usage Monitor_

“CPU Usage Monitor” is implemented as follows:

- Metric: **WHEN max() OF system.process.cpu.total.pct OVER all documents** 
- Threshold: **IS ABOVE 0.5 FOR THE LAST 5 minutes**
- Vulnerability Mitigated: **Malicious software consuming system resources**
- Reliability: **This alert may have low reliability as it monitors the total CPU percantage used by the service since the service was launched. Many innocous applications consume substantial CPU resources, so this alert may trigger many false-positive flags.**
