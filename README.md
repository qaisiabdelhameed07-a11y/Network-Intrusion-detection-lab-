# Network-Intrusion-detection-lab-
Cybersecurity lab using Suricata, Wireshark, Nmap, Ubuntu, and VMware to detect and analyze network traffic.

Project Overview

This project demonstrates the deployment and testing of a network intrusion detection system (IDS) in an isolated virtual environment using VMware Workstation and Ubuntu Linux.

The lab consists of two virtual machines: IDS-Monitor, which runs Suricata and Wireshark, and IDS-Attacker, which generates controlled network traffic using Nmap and ICMP testing.

The objective was to gain hands-on experience in network security monitoring, packet analysis, intrusion detection, and security alert investigation.

Throughout this project, I configured an isolated Host-only network, analyzed ICMP traffic using Wireshark, performed controlled TCP port scans with Nmap, and developed custom Suricata detection rules to identify ICMP Echo Requests and TCP SYN traffic.

Technologies Used: VMware Workstation, Ubuntu Linux, Suricata IDS, Wireshark, Nmap, and Linux CLI.

Skills Demonstrated: Network configuration, packet inspection, TCP/IP analysis, intrusion detection, custom rule development, security monitoring, and troubleshooting.


## Lab Architecture

Environment Overview
This lab uses two Ubuntu Linux virtual machines hosted in VMware Workstation. Both machines communicate through a private Host-only network (VMnet1), providing an isolated environment for controlled security testing.

### Virtual Machine Configuration

IDS-Monitor (Ubuntu Linux)

IP Address: 192.168.11.128

Network: VMware Host-only (VMnet1)

Role: Intrusion Detection and Network Traffic Analysis

Tools: Suricata IDS and Wireshark

IDS-Attacker (Ubuntu Linux)

IP Address: 192.168.11.129

Network: VMware Host-only (VMnet1)

Role: Simulated Network Attacks and Traffic Generation

Tools: Nmap and Linux networking utilities

### Security Tools
IDS-Monitor
- Suricata: Network intrusion detection, traffic inspection, and custom alert generation.
- Wireshark: Packet capture and analysis of network protocols.
IDS-Attacker
- Nmap: TCP port scanning and network reconnaissance.
- Ping: ICMP traffic generation and connectivity testing.
  
### Network Design
IDS-Attacker (192.168.11.129)
↓
VMware Host-Only Network (VMnet1)
↓
IDS-Monitor (192.168.11.128)
How the Lab Works
The IDS-Attacker generates controlled ICMP and TCP traffic directed toward IDS-Monitor. Wireshark captures packets for analysis, while Suricata evaluates the traffic against its configured detection rules.

Custom Suricata signatures were created to identify ICMP Echo Requests and TCP SYN packets, demonstrating fundamental intrusion detection techniques.

The isolated network allows security testing without directing scans toward external systems.

## Lab Setup & Screenshots

### 1. IDS-Monitor — VMware Configuration

![IDS-Monitor VMware Configuration](Screenshots/Screenshot%202026-11-09%20191749.png)

Description: Configured the IDS-Monitor virtual machine in VMware Workstation with Ubuntu Linux and Host-only networking. This machine serves as the monitoring system for Suricata IDS and Wireshark packet analysis.

#### IDS-Attacker Configuration

![IDS-Attacker VMware Configuration](Screenshots/Host%20only%20attacker.png)

**Description:** Configured the IDS-Attacker virtual machine with Ubuntu Linux and VMware Host-only networking. This machine generates controlled ICMP traffic and TCP port scans to test the intrusion detection capabilities of IDS-Monitor.

### Network Configuration

#### IDS-Monitor — System and IP Configuration

![IDS-Monitor System Configuration](Screenshots/IP%20address%20and%20archheticture%20.png)

**Description:** Verified the Ubuntu operating system, system architecture, and network interface configuration on IDS-Monitor. This system was configured to use the private IP address `192.168.11.128` for communication with IDS-Attacker over the VMware Host-only network.

#### IDS-Attacker — System and IP Configuration

![IDS-Attacker System Configuration](Screenshots/ip%20address%20and%20archeticture%20for%20attacker.png)

**Description:** Verified the Ubuntu operating system, system architecture, and network configuration of IDS-Attacker. The machine uses the private IP address `192.168.11.129` on the VMware Host-only network and serves as the traffic generation system for controlled ICMP testing and Nmap scans.

### Nmap Port Scanning

#### Nmap Installation and Version Verification

![Nmap Installation and Version](Screenshots/NMap%20installion%20and%20version.png)

**Description:** Installed Nmap on the IDS-Attacker Ubuntu virtual machine and verified the installed version. Nmap was used to perform authorized TCP port scans against IDS-Monitor, generating controlled network traffic for intrusion detection testing.

#### Nmap TCP Port Scan Results

![Nmap TCP Port Scan](Screenshots/ports%20check%20nmap.png)

**Description:** Performed a controlled TCP connect scan from IDS-Attacker against IDS-Monitor using Nmap. The scan examined ports 21 (FTP), 22 (SSH), 80 (HTTP), 443 (HTTPS), and 8080 (HTTP Proxy), which were reported as closed. This test generated TCP connection attempts for network monitoring and intrusion detection analysis.

**Command Used:** `nmap -sT -Pn -p 21,22,80,443,8080 192.168.11.128`

### Suricata Intrusion Detection

#### Suricata IDS Service Verification

![Suricata Active Service](Screenshots/suricata%20active.png)

**Description:** Verified that the Suricata intrusion detection service was active on IDS-Monitor. Suricata monitors network traffic on the configured interface and evaluates packets against detection signatures to identify activity matching security rules.

**Command Used:** `systemctl is-active suricata`
#### Custom ICMP Detection Alerts

![Suricata ICMP Detection](Screenshots/suricata%20detection.png)

**Description:** Developed and tested a custom Suricata detection rule to identify ICMP Echo Requests sent from IDS-Attacker (`192.168.11.129`) to IDS-Monitor (`192.168.11.128`). The rule successfully generated alerts in Suricata's `fast.log`, demonstrating signature-based network traffic detection.

**Signature ID:** `1000001`

**Command Used:** `sudo grep 'LAB ALERT - ICMP Traffic From Attacker' /var/log/suricata/fast.log | tail -n 15`

**Finding:** Suricata successfully detected controlled ICMP traffic originating from the attacker VM. These alerts represent authorized lab activity, not a confirmed malicious intrusion.

#### Suricata Detection Rule Validation

![Suricata Rule Validation](Screenshots/suricata%20tcp%20detection%20.png)

**Description:** Validated the Suricata configuration after adding custom ICMP and TCP SYN detection rules. The configuration test confirmed that 53,380 detection rules loaded successfully with zero failures.

**Command Used:** `sudo suricata -T -c /etc/suricata/suricata.yaml -v`

**Finding:** The configuration passed validation, confirming that Suricata could load the configured detection rules. This test verifies rule loading, not whether TCP SYN alerts were generated.

### Wireshark Packet Analysis

#### Wireshark Installation

![Wireshark Installation](Screenshots/Wireshark%20installation.png)

**Description:** Installed Wireshark on the IDS-Monitor Ubuntu virtual machine to capture and analyze network traffic. Wireshark provides visibility into individual packets, allowing inspection of source and destination IP addresses, network protocols, and packet header information.

**Tool:** Wireshark

**Purpose:** Network packet capture and protocol analysis.

#### Wireshark Version Verification

![Wireshark Version](Screenshots/Wireshark%20version.png)

**Description:** Verified the successful installation of Wireshark on IDS-Monitor and confirmed the installed version (4.6.4). This ensured the packet analysis tool was available for capturing and examining network traffic within the isolated VMware lab.

**Tool:** Wireshark 4.6.4

**Purpose:** Verify that the packet analysis environment was ready for network traffic inspection.

#### Wireshark Source, Destination, and Protocol Analysis

![Wireshark Network Traffic Analysis](Screenshots/Wireshark%20src%20and%20dst%20and%20protocol.png)

**Description:** Captured and analyzed ICMP network traffic using Wireshark on IDS-Monitor. Identified the source IP address (`192.168.11.129`), destination IP address (`192.168.11.128`), and ICMP protocol to verify communication between the two virtual machines.

**Display Filter:** `icmp`

**Finding:** Successfully identified ICMP Echo Request and Echo Reply packets exchanged between IDS-Attacker and IDS-Monitor.

#### Detailed Wireshark ICMP Packet Analysis

![Detailed Wireshark ICMP Analysis](Screenshots/wireshark%20full%20analysis.png)

**Description:** Inspected captured ICMP packets using Wireshark to examine IPv4 header information and ICMP message fields. Analyzed source and destination addresses, protocol identification, Time to Live (TTL), ICMP message type, and checksum information.

**Packet Analysis:**
- **Source IP:** `192.168.11.129` (IDS-Attacker)
- **Destination IP:** `192.168.11.128` (IDS-Monitor)
- **Protocol:** ICMP
- **ICMP Type:** 8 (Echo Request)
- **ICMP Code:** 0

**Finding:** Verified that ICMP Echo Requests originated from IDS-Attacker and were transmitted to IDS-Monitor through the isolated VMware Host-only network.

### System Maintenance

#### Ubuntu System Updates

![Ubuntu System Updates](Screenshots/update%20for%20monitor.png)

**Description:** Updated the Ubuntu package information on IDS-Monitor as part of preparing and maintaining the cybersecurity lab environment. Keeping system packages updated helps reduce exposure to known vulnerabilities and improves system stability.

**Purpose:** Maintain a secure and reliable operating environment for Suricata intrusion detection and Wireshark network traffic analysis.

**Security Practice:** Regularly check for available operating system and security updates.

#### Live Network Packet Capture

![Live Network Packet Capture](Screenshots/capturing%20packets.png)

**Description:** Used Wireshark on IDS-Monitor to capture live network traffic generated within the isolated VMware Host-only environment. The capture provided visibility into communication between IDS-Attacker (`192.168.11.129`) and IDS-Monitor (`192.168.11.128`).

**Tool Used:** Wireshark

**Network Interface:** `ens33`

**Purpose:** Capture and inspect network packets to understand communication between virtual machines and support intrusion detection analysis.

**Finding:** Successfully captured network traffic for inspection and protocol analysis, complementing the alerts generated by Suricata IDS.

## Project Results

This project successfully demonstrated network traffic monitoring, packet analysis, and signature-based intrusion detection within an isolated VMware environment.

### Key Achievements

- **Virtual Network Configuration:** Configured two Ubuntu virtual machines using VMware Host-only networking to create an isolated cybersecurity testing environment.
- **Network Connectivity:** Verified communication between IDS-Attacker (`192.168.11.129`) and IDS-Monitor (`192.168.11.128`).
- **Nmap Port Scanning:** Performed a controlled TCP connect scan against ports 21, 22, 80, 443, and 8080. All five ports were reported as closed.
- **Suricata IDS Deployment:** Installed and configured Suricata to monitor network traffic on interface `ens33`.
- **Custom Detection Rules:** Created custom Suricata signatures for ICMP Echo Requests and TCP SYN traffic.
- **Intrusion Detection Validation:** Confirmed that the custom ICMP detection rule generated alerts with signature ID `1000001`.
- **Rule Configuration Testing:** Successfully validated the Suricata configuration, loading 53,380 rules with zero failures.
- **Wireshark Packet Analysis:** Captured and inspected ICMP packets, including source and destination IP addresses, protocol fields, and ICMP message types.

### Overall Outcome

The lab demonstrated how network traffic generated by a simulated attacker can be captured, analyzed, and detected using open-source security tools. The project provided hands-on experience with defensive security monitoring and foundational Security Operations Center (SOC) workflows.

**Note:** All testing was performed in an isolated, authorized virtual lab environment.

## Skills Demonstrated

Through this project, I gained hands-on experience with the following cybersecurity and networking skills:

### Network Security
- Network traffic monitoring and analysis
- TCP/IP and ICMP protocol analysis
- TCP port scanning using Nmap
- Source and destination IP address identification
- Network isolation using VMware Host-only networking

### Intrusion Detection
- Suricata IDS installation and configuration
- Custom intrusion detection rule creation
- Signature-based detection of ICMP traffic
- TCP SYN detection rule configuration
- Security alert log analysis
- Suricata rule validation and troubleshooting

### Packet Analysis
- Wireshark packet capture
- ICMP Echo Request and Echo Reply analysis
- Network packet header inspection
- Wireshark display filtering
- Basic network traffic investigation

### Linux and Virtualization
- Ubuntu Linux system administration
- Linux command-line operations
- VMware Workstation virtual machine configuration
- Network interface configuration
- Security tool installation and verification

### SOC Analyst Fundamentals
- Security event monitoring
- Detection rule testing
- Network traffic investigation
- Distinguishing authorized test traffic from potential security threats
- Documenting security findings and investigation evidence

  ## Project Conclusion

This project provided hands-on experience in network security monitoring, intrusion detection, and packet analysis using Suricata, Wireshark, Nmap, Ubuntu Linux, and VMware Workstation.

By building an isolated virtual network with two Ubuntu machines, I was able to generate controlled network traffic, perform TCP port scans, capture packets, and investigate network activity. I also configured custom Suricata detection rules and successfully verified ICMP security alerts.

The project strengthened my understanding of TCP/IP networking, ICMP communication, signature-based intrusion detection, Linux administration, and security event analysis.

Most importantly, this lab helped me develop practical skills relevant to Security Operations Center (SOC) environments, including monitoring network activity, examining alerts, analyzing packets, and documenting technical findings.

### Future Improvements

- Expand Suricata detection rules to identify additional network activity.
- Capture and document confirmed TCP SYN detection alerts.
- Explore centralized security monitoring using a SIEM platform.
- Practice investigating suspicious network activity and documenting incident findings.
- Develop more advanced detection and alert analysis workflows.

**Project Status:** Completed initial lab implementation and testing. Future enhancements are planned.
