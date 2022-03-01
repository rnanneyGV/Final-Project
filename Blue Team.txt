##Blue Team: Summary of Operations

Table of Contents

- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

Network Topology

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

!C:\Users\Nanneys\Final-Project\Images\Network_Diagram.png

Description of Targets

The target of this attack was the Target 1 VM (192.168.1.110).

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts, described in detail below, have been implemented:

- Excessive HTTP Errors
- HTTP Request Size Monitor
- CPU Usage Monitor

Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

Excessive HTTP Errors

“Excessive HTTP Errors” is implemented as follows:

- Metric: WHEN count() GROUPED OVER top 5 'http.response.status_code' 
- Threshold: IS ABOVE 400 FOR THE LAST 5 minutes
- Vulnerability Mitigated: Enumeration and Brute Force
- Reliability: TODO: Does this alert generate lots of false positives/false negatives? Rate as low, medium, or high reliability.

HTTP Request Size Monitor

“HTTP Request Size Monitor” is implemented as follows:

- Metric: WHEN sum() of http.request.bytes OVER all documents 
- Threshold: IS ABOVE 3500 FOR THE LAST 1 minute
- Vulnerability Mitigated: Code injection and distributed denial of service (DDOS)
- Reliability: TODO: Does this alert generate lots of false positives/false negatives? Rate as low, medium, or high reliability.

CPU Usage Monitor

“CPU Usage Monitor” is implemented as follows:

- Metric: WHEN max() OF system.process.cpu.total.pct OVER all documents 
- Threshold: IS ABOVE 0.5 FOR THE LAST 5 minutes
- Vulnerability Mitigated: Malicious software consuming system resources
- Reliability: TODO: Does this alert generate lots of false positives/false negatives? Rate as low, medium, or high reliability.

Suggestions for Going Further (Optional)

TODO:

Each alert above pertains to a specific vulnerability/exploit. Recall that alerts only detect malicious behavior, but do not stop it. For each vulnerability/exploit identified by the alerts above, suggest a patch. E.g., implementing a blocklist is an effective tactic against brute-force attacks. It is not necessary to explain how to implement each patch.

The logs and alerts generated during the assessment suggest that this network is susceptible to several active threats, identified by the alerts above. In addition to watching for occurrences of such threats, the network should be hardened against them. The Blue Team suggests that IT implement the fixes below to protect the network:
Vulnerability 1
Patch: TODO: E.g., install special-security-package with apt-get
Why It Works: TODO: E.g., special-security-package scans the system for viruses every day
Vulnerability 2
Patch: TODO: E.g., install special-security-package with apt-get
Why It Works: TODO: E.g., special-security-package scans the system for viruses every day
Vulnerability 3
Patch: TODO: E.g., install special-security-package with apt-get
Why It Works: TODO: E.g., special-security-package scans the system for viruses every day
