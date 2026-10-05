# OASIS INFOBYTE – Security Analyst

## Task 1: Basic Network Scanning with Nmap

### Objective

The objective of this task is to use Nmap to scan a local machine and identify open ports, running services, and operating system information.

The scan was performed on the local machine using the loopback address:

```text
127.0.0.1
```

---

## Tools Used

- Nmap 7.991
- Windows PowerShell
- Microsoft Windows 10
- Localhost (127.0.0.1)

---

## What is Nmap?

Nmap (Network Mapper) is a network scanning and security auditing tool. It can be used to discover hosts, identify open ports, detect services, and gather operating system information.

Network scanning is useful for security analysis because it helps identify services that are accessible on a system and allows administrators to review whether those services are necessary and properly protected.

---

## Nmap Installation

Nmap was installed on the Windows machine.

The installation was verified using the following command:

```powershell
nmap --version
```

The installed version was:

```text
Nmap version 7.991
```

A screenshot of the installation and version verification is available in:

```text
Screenshots/01-nmap-installation.PNG
```

---

# 1. Basic Nmap Scan

### Command Used

```powershell
nmap 127.0.0.1
```

The scan was performed against `127.0.0.1`, which represents the local machine.

### Scan Results

The scan identified the following open TCP ports:

| Port | State | Service |
|------|-------|---------|
| 135/tcp | open | msrpc |
| 445/tcp | open | microsoft-ds |
| 1433/tcp | open | ms-sql-s |
| 1434/tcp | open | ms-sql-m |
| 2179/tcp | open | vmrdp |

The scan also showed **995 closed TCP ports**.

### Screenshot

```text
Screenshots/02-basic-scan.PNG
```

---

# 2. Service Version Detection

### Command Used

```powershell
nmap -sV 127.0.0.1
```

The `-sV` option is used to detect the services and their versions running on open ports.

### Service Detection Results

| Port | Service | Version / Information |
|------|---------|------------------------|
| 135/tcp | msrpc | Microsoft Windows RPC |
| 445/tcp | microsoft-ds | Version not identified |
| 1433/tcp | ms-sql-s | Microsoft SQL Server |
| 1434/tcp | ms-sql-m | Version not identified |
| 2179/tcp | vmrdp | Version not identified |

Nmap also identified the operating system as Windows.

Some services were marked with `?` in the original Nmap output because Nmap could not confidently identify their exact service version. These results have therefore not been guessed or replaced with unsupported version information.

### Screenshot

```text
Screenshots/03-service-scan.PNG
```

---

# 3. Operating System Detection

### Command Used

```powershell
nmap -O 127.0.0.1
```

The `-O` option is used by Nmap for operating system detection.

### Detection Results

```text
Device type: general purpose
Running: Microsoft Windows 10
OS CPE: cpe:/o:microsoft:windows_10
OS details: Microsoft Windows 10 1809 - 21H2
Network Distance: 0 hops
```

### Screenshot

```text
Screenshots/04-os-detection.PNG
```

---

# Security Analysis

Open ports indicate network services that are accepting connections. Unnecessary or improperly protected services can increase the attack surface of a system.

## Port 135 – Microsoft RPC

Port 135 is associated with Microsoft RPC (Remote Procedure Call), which is used by Windows for communication between applications and system components.

**Security consideration:**

RPC services should be protected by the Windows Firewall and should not be unnecessarily exposed to untrusted networks.

---

## Port 445 – Microsoft-DS

Port 445 is commonly associated with Windows file and printer sharing through SMB.

**Security consideration:**

SMB should be restricted to trusted networks because exposed SMB services can become a security risk if vulnerable or improperly configured.

---

## Port 1433 – Microsoft SQL Server

Port 1433 is commonly used by Microsoft SQL Server.

**Security consideration:**

Database services should only be accessible to authorized systems and users. Strong authentication and appropriate firewall restrictions should be used.

---

## Port 1434 – Microsoft SQL Server Browser

Port 1434 is associated with Microsoft SQL Server Browser services.

**Security consideration:**

The service should only be accessible where required and should be protected by appropriate firewall rules.

---

## Port 2179 – VM Remote Desktop

Port 2179 can be associated with Microsoft virtualization-related remote access services.

**Security consideration:**

Remote access services should be restricted to trusted systems and should not be unnecessarily exposed.

---

# Scan Summary

The following Nmap scans were successfully performed:

| Scan Type | Command | Purpose |
|-----------|---------|---------|
| Basic Scan | `nmap 127.0.0.1` | Identify open ports and services |
| Service Detection | `nmap -sV 127.0.0.1` | Detect services and available version information |
| OS Detection | `nmap -O 127.0.0.1` | Identify operating system information |

### Main Findings

- Target scanned: `127.0.0.1`
- Open TCP ports identified: **5**
- Closed TCP ports reported: **995**
- Operating system detected: **Microsoft Windows 10**
- Service detection was performed successfully.
- Some service versions could not be confidently identified by Nmap.

---

# Evidence and Screenshots

The complete Nmap command outputs are available in:

```text
nmap_scan_results.txt
```

Screenshots of the task execution are available in the `Screenshots` directory.

### Included Screenshots

1. `01-nmap-installation.PNG` – Nmap installation/version verification
2. `02-basic-scan.PNG` – Basic Nmap scan
3. `03-service-scan.PNG` – Service version detection
4. `04-os-detection.PNG` – Operating system detection

---

# Ethical Consideration

Network scanning should only be performed on systems that you own or have explicit permission to test.

For this task, Nmap was used only against:

```text
127.0.0.1
```

which refers to the local machine.

No external or production systems were scanned.

Scanning external systems or networks without authorization is not permitted.

---

# Conclusion

Nmap was successfully used to scan the local Windows machine.

The basic scan identified five open TCP ports and 995 closed TCP ports. Service detection was then performed to gather information about the services running on the open ports. Operating system detection identified the target as Microsoft Windows 10.

This task demonstrates how Nmap can be used for basic network discovery, service identification, operating system detection, and security analysis in an authorized local environment.

---

# Project Structure

```text
Security-Analyst-Task-1-Nmap/
│
├── README.md
├── nmap_scan_results.txt
│
└── Screenshots/
    ├── 01-nmap-installation.PNG
    ├── 02-basic-scan.PNG
    ├── 03-service-scan.PNG
    └── 04-os-detection.PNG
```

---

# Task Information

**Program:** OASIS INFOBYTE  
**Track:** Security Analyst  
**Task:** Task 1 – Basic Network Scanning with Nmap  
**Target:** 127.0.0.1 (Localhost)  
**Platform:** Microsoft Windows 10  
**Nmap Version:** 7.991