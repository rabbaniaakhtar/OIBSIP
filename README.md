# OASIS INFOBYTE – Security Analyst
## Task 1: Basic Network Scanning with Nmap

### Objective

The objective of this task is to use Nmap to scan a local machine and identify open ports, running services, and operating system information.

The scan was performed on the local machine using the loopback address:

```text
127.0.0.1

Only the local machine was scanned for this educational task.

Tools Used
Nmap 7.991
Windows PowerShell
Windows 10
Localhost (127.0.0.1)
Nmap Installation

Nmap was installed on the Windows machine.

The installation was verified using:

nmap --version

The installed version was:

Nmap version 7.991
1. Basic Nmap Scan

Command used:

nmap 127.0.0.1

The scan identified the following open TCP ports:

Port	State	Service
135/tcp	open	msrpc
445/tcp	open	microsoft-ds
1433/tcp	open	ms-sql-s
1434/tcp	open	ms-sql-m
2179/tcp	open	vmrdp

The scan also showed 995 closed TCP ports.

2. Service Version Detection

Command used:

nmap -sV 127.0.0.1

The detected services included:

Port	    Service	            Version / Information
135/tcp 	msrpc	        Microsoft Windows RPC
445/tcp	    microsoft-ds	Version not identified
1433/tcp	ms-sql-s	    Microsoft SQL Server
1434/tcp	ms-sql-m	    Version not identified
2179/tcp	vmrdp	        Version not identified

Nmap identified the operating system as Windows.

Some services were marked with ? because Nmap could not confidently identify their exact service version.

3. Operating System Detection

Command used:

nmap -O 127.0.0.1

Nmap detected:

Device type: general purpose
Running: Microsoft Windows 10
OS CPE: cpe:/o:microsoft:windows_10
OS details: Microsoft Windows 10 1809 - 21H2
Network Distance: 0 hops
Security Analysis

Open ports represent network services that are accepting connections. If unnecessary services are exposed, they can increase the attack surface of a system.

Port 135 – Microsoft RPC

Microsoft RPC is used by Windows for communication between applications and system components.

Security consideration:
RPC services should be protected by the Windows Firewall and should not be unnecessarily exposed to untrusted networks.

Port 445 – Microsoft-DS

Port 445 is commonly associated with Windows file and printer sharing through SMB.

Security consideration:
SMB should be restricted to trusted networks because exposed SMB services can become a security risk if vulnerable or improperly configured.

Port 1433 – Microsoft SQL Server

Port 1433 is commonly used by Microsoft SQL Server.

Security consideration:
Database services should only be accessible to authorized systems and users. Strong authentication and firewall restrictions should be used.

Port 1434 – Microsoft SQL Server Browser

Port 1434 is associated with Microsoft SQL Server Browser services.

Security consideration:
The service should only be accessible where required and should be protected by appropriate firewall rules.

Port 2179 – VM Remote Desktop

Port 2179 can be associated with Microsoft virtualization-related remote access services.

Security consideration:
Remote access services should be restricted to trusted systems and should not be unnecessarily exposed.

Scan Results

The complete command outputs are available in:

nmap_scan_results.txt

The screenshots of the scans are available in:

screenshots/

The screenshots included are:

01-nmap-installation.png
02-basic-scan.png
03-service-scan.png
04-os-detection.png
Ethical Consideration

Network scanning should only be performed on systems that you own or have explicit permission to test.

For this task, Nmap was used only against:

127.0.0.1

which refers to the local machine.

Scanning external systems or networks without authorization is not permitted.

Conclusion

Nmap was successfully used to scan the local Windows machine.

The scan identified five open TCP ports and provided information about the services running on those ports. Service detection and operating system detection were also performed.

This task demonstrates how Nmap can be used for basic network discovery and security analysis.