# Blue Team: Summary of Operations

## Table of Contents
- Network Topology
- Description of Targets
- Monitoring the Targets
- Patterns of Traffic & Behavior
- Suggestions for Going Further

### Network Topology

The following machines were identified on the network:
- Target 1
  - **Operating System**: Linux 3.2-4.9
  - **Purpose**: Web Server
  - **IP Address**: 192.168.1.110
- Target 2
  - **Operating System**: Linux 3.2-4.9
  - **Purpose**: Web Server
  - **IP Address**: 192.168.1.115
- ELK
  - **Operating System**: Ubuntu
  - **Purpose**: Kibana
  - **IP Address**: 192.168.1.100
- Capstone
  - **Operating System**: Linux
  - **Purpose**: Web Server
  - **IP Address**: 192.168.1.105
- Kali
  - **Operating System**: Kali Linux
  - **Purpose**: Attacking machine
  - **IP Address**: 192.168.1.90
- ML-RefVM-684427
  - **Operating System**: Windows
  - **Purpose**: Accessing Kibana and VMs
  - **IP Address**: 192.168.1.1


### Description of Targets

The target of this attack was: `Target 1` (192.168.1.110).

Target 1 is an Apache web server and has SSH enabled, so ports 80 and 22 are possible ports of entry for attackers. As such, the following alerts have been implemented:

HTTP Errors Alert is implemented as follows:
  - **Metric**: HTTP Status Errors
  - **Threshold**: Above 400 over last 1 minute
  - **Vulnerability Mitigated**: Brute Force Attacks
  - **Reliability**: high

SSH password failed attempts Alert is implemented as follows:
  - **Metric**: Password failed attempts
  - **Threshold**: Failed attempts above 10 over last 5 minutes.
  - **Vulnerability Mitigated**: SSH logins
  - **Reliability**: high

### Monitoring the Targets

Traffic to these services should be carefully monitored. To this end, we have implemented the alerts below:

Port Scans Alert is implemented as follows:
  - **Metric**: source port
  - **Threshold**: count above 2000 over last 5 minutes
  - **Vulnerability Mitigated**: network scans
  - **Reliability**: high

CPU Usage Monitor Alert is implemented as follows:
  - **Metric**: CPU usage
  - **Threshold**: When max CPU process total above .5 over last 5 minutes.
  - **Vulnerability Mitigated**: DDoS Attacks
  - **Reliability**: medium

HTTP Request Size Alert is implemented as follows:
  - **Metric**: HTTP request size
  - **Threshold**: Sum of HTTP request bytes is above 3500 over the last 1 minute.
  - **Vulnerability Mitigated**: Buffer Overflow Attacks
  - **Reliability**: low

HTTP Errors Alert is implemented as follows:
  - **Metric**: HTTP Status Errors
  - **Threshold**: Above 400 over last 1 minute
  - **Vulnerability Mitigated**: Brute Force Attacks
  - **Reliability**: high



### Suggestions for Going Further (Optional)
_TODO_:
- Each alert above pertains to a specific vulnerability/exploit. Recall that alerts only detect malicious behavior, but do not stop it. For each vulnerability/exploit identified by the alerts above, suggest a patch. E.g., implementing a blocklist is an effective tactic against brute-force attacks. It is not necessary to explain _how_ to implement each patch.

The logs and alerts generated during the assessment suggest that this network is susceptible to several active threats, identified by the alerts above. In addition to watching for occurrences of such threats, the network should be hardened against them. The Blue Team suggests that IT implement the fixes below to protect the network:
- Vulnerability 1
  - **Patch**: TODO: E.g., _install `special-security-package` with `apt-get`_
  - **Why It Works**: TODO: E.g., _`special-security-package` scans the system for viruses every day_
- Vulnerability 2
  - **Patch**: TODO: E.g., _install `special-security-package` with `apt-get`_
  - **Why It Works**: TODO: E.g., _`special-security-package` scans the system for viruses every day_
- Vulnerability 3
  - **Patch**: TODO: E.g., _install `special-security-package` with `apt-get`_
  - **Why It Works**: TODO: E.g., _`special-security-package` scans the system for viruses every day_
