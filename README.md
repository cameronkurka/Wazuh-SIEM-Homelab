
# Wazuh SIEM Home Lab

### Security Monitoring | Threat Detection | Log Analysis | MITRE ATT&CK

## Project Overview

This repository documents the deployment and ongoing development of a Security Information and Event Management (SIEM) home lab using Wazuh, Ubuntu Server, Kali Linux, and UTM virtualization on an Apple Silicon MacBook Air.

The project was created to develop hands-on Security Operations Center (SOC) analyst skills through centralized security monitoring, endpoint log collection, threat detection, and security event investigation.

After deploying the Wazuh environment and connecting a Kali Linux endpoint, I conducted two security monitoring investigations: SSH authentication failure detection and File Integrity Monitoring (FIM).

The SSH investigation involved generating controlled authentication failures, analyzing Wazuh alerts, and mapping the observed activity to MITRE ATT&CK.

The FIM investigation involved configuring real-time directory monitoring and successfully detecting file creation, modification, and deletion events. Both investigations include documented methodologies, detection results, and supporting evidence.

The project will continue expanding as additional monitoring scenarios and investigations are completed.

---

## Lab Architecture

| Component | Technology | Purpose |
|---|---|---|
| Host Machine | Apple Silicon MacBook Air | Physical host |
| Virtualization | UTM | Runs the virtual machines |
| SIEM Server | Ubuntu Server 22.04 LTS (ARM64) | Hosts Wazuh components |
| Monitored Endpoint | Kali Linux (ARM64) | Generates security events |
| SIEM Platform | Wazuh | Centralized security monitoring |
| Endpoint Agent | Wazuh Agent | Collects endpoint telemetry |
| Authentication Service | OpenSSH | Provides authentication events |
| File Integrity Monitoring | Wazuh FIM | Detects file creation, modification, and deletion |

### Architecture Diagram

```text
               Apple Silicon MacBook Air
                          |
                   UTM Virtualization
                          |
            +-------------+-------------+
            |                           |
            v                           v
     Ubuntu Server 22.04             Kali Linux
     -------------------             ----------
     Wazuh Manager                   Wazuh Agent
     Wazuh Indexer                   OpenSSH
     Wazuh Dashboard                 Auth Logs
            ^                        FIM Monitoring
            |                           |
            +------ Security Events ----+
```

The Kali Linux endpoint communicates with the Wazuh manager, allowing authentication events and file integrity monitoring alerts to be collected and analyzed through the dashboard.

---

## Completed Project Milestones

### 1. Wazuh Deployment and Configuration

- Deployed an Ubuntu Server virtual machine using UTM.
- Installed and configured Wazuh components.
- Established access to the Wazuh web dashboard.
- Configured a Kali Linux endpoint with the Wazuh agent.
- Verified successful agent enrollment and connectivity.
- Troubleshot ARM64 compatibility, HTTPS certificate access, and virtual machine networking.

**Documentation:** [Wazuh Installation and Configuration](docs/01-wazuh-installation.md)

### 2. SSH Authentication Failure Investigation

Conducted a controlled security monitoring investigation to evaluate Wazuh's ability to detect repeated failed SSH authentication attempts.

**Investigation activities:**

- Generated failed SSH authentication events on the Kali Linux endpoint.
- Reviewed the resulting alerts through Wazuh Threat Hunting.
- Examined alert metadata, including source address, username, and affected endpoint.
- Identified Wazuh detection rule 5712 with severity level 10.
- Analyzed the MITRE ATT&CK mapping to T1110 (Brute Force) under the Credential Access tactic.
- Documented findings and supporting evidence.

The test originated from the local loopback address (`::1`) within the controlled lab environment. The investigation demonstrated detection and analysis of authentication failures, not a successful account compromise.

**Documentation:** [SSH Authentication Failure Investigation](docs/02-ssh-bruteforce-investigation.md)

### 3. File Integrity Monitoring Investigation

Configured real-time File Integrity Monitoring (FIM) on the Kali Linux endpoint to detect changes within a dedicated test directory.

**Investigation activities:**

- Configured Wazuh FIM through the agent's `ossec.conf` file.
- Enabled real-time monitoring for `/home/kali/fim-lab`.
- Generated controlled file creation, modification, and deletion events.
- Verified successful detection of all three file operations.
- Identified Wazuh rules 554, 550, and 553 with severity levels 5 and 7.
- Reviewed MITRE ATT&CK mappings associated with file manipulation and deletion.
- Documented detection results and supporting screenshots.

**Detection results:**

| Event | Wazuh Rule ID | Alert Level | Result |
|---|---|---|---|
| File Created | 554 | 5 | Detected |
| File Modified | 550 | 7 | Detected |
| File Deleted | 553 | 7 | Detected |

The investigation demonstrated how file integrity monitoring can help SOC analysts identify unexpected endpoint changes and investigate potentially suspicious activity.

The tests involved harmless file operations in a controlled environment, not actual malicious activity.

**Documentation:** [File Integrity Monitoring Investigation](docs/03-file-integrity-monitoring.md)

---

## Lab Screenshots

### Wazuh Dashboard

![Wazuh Dashboard Overview](images/dashboard-overview.png)

*Wazuh dashboard providing centralized visibility into the monitoring environment.*

### Kali Linux Agent

![Kali Linux Agent Connected](images/kali-agent-connected.png)

*Kali Linux endpoint successfully enrolled and monitored through Wazuh.*

### SSH Authentication Detection

![SSH Brute Force Alert](images/ssh-bruteforce-alert.png)

*Wazuh security alert generated during the controlled SSH authentication investigation.*

### File Integrity Monitoring Dashboard

![FIM Events Overview](images/fim-events-overview.png)

*Wazuh dashboard showing successful detection of file creation, modification, and deletion.*

### File Integrity Monitoring Alerts

![FIM Alert Details](images/fim-alert-details.png)

*Individual Wazuh alerts displaying monitored file paths, detection rules, and severity levels.*

---

## Technical Skills Demonstrated

| Category | Skills and Technologies |
|---|---|
| SIEM & Monitoring | Wazuh, centralized log collection, endpoint monitoring, File Integrity Monitoring |
| Security Operations | Alert investigation, log analysis, threat detection |
| Threat Analysis | MITRE ATT&CK, T1110, T1485, T1070.004, T1565.001 |
| Endpoint Security | Real-time FIM, file change detection, Wazuh agent configuration |
| Operating Systems | Ubuntu Server, Kali Linux, Linux administration |
| Infrastructure | UTM virtualization, ARM64, virtual machine networking, DNS troubleshooting |
| Documentation | Technical reporting, investigation documentation, Git, GitHub |

---

## Challenges and Lessons Learned

### ARM64 Compatibility

Deploying the environment on Apple Silicon required attention to processor architecture and compatible Linux installations.

### Virtual Machine Configuration

Resolved installation and boot issues, including removing the installation ISO after Ubuntu was installed and troubleshooting Kali Linux display issues.

### Dashboard Connectivity

Troubleshot Wazuh service availability, HTTPS access, and browser certificate warnings within the local lab.

### Endpoint Monitoring

Configured the Wazuh agent and verified communication between the monitored Kali Linux endpoint and the SIEM server.

### Network Troubleshooting

Diagnosed and resolved Kali Linux connectivity issues involving a disabled network interface, inactive NetworkManager service, and disabled IPv4 configuration.

Restored connectivity by activating the network interface, starting NetworkManager, enabling automatic IPv4 configuration, and verifying network access and DNS resolution.

### File Integrity Monitoring

Configured real-time directory monitoring through the Wazuh agent and validated detection of file creation, modification, and deletion.

### Security Investigation

Practiced interpreting detection rules, reviewing authentication and file integrity events, and mapping observed activity to MITRE ATT&CK.

---

## Future Investigations

The following activities are planned unless marked as completed:

- [x] File integrity monitoring
- [ ] Linux account creation and modification monitoring
- [ ] Privilege-related event detection
- [ ] Vulnerability monitoring
- [ ] Windows endpoint monitoring
- [ ] Sysmon integration
- [ ] Custom Wazuh detection rules
- [ ] Additional SOC-style investigation reports

---

## Project Documentation

| Document | Description |
|---|---|
| [Wazuh Installation](docs/01-wazuh-installation.md) | Deployment, architecture, configuration, and troubleshooting |
| [SSH Authentication Investigation](docs/02-ssh-bruteforce-investigation.md) | Detection methodology, alert analysis, MITRE ATT&CK mapping, and evidence |
| [File Integrity Monitoring Investigation](docs/03-file-integrity-monitoring.md) | Real-time FIM configuration, file change detection, alert analysis, and supporting evidence |

---

## Project Status

**Ongoing development**

The Wazuh SIEM environment has been successfully deployed, and two security monitoring investigations have been completed and documented:

1. SSH Authentication Failure Detection
2. File Integrity Monitoring

Future work will expand the lab's detection capabilities through additional endpoint monitoring scenarios, security investigations, and custom detection rules.
