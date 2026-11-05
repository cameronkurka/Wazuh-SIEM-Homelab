
# Wazuh SIEM Installation & Configuration

## 1. Project Overview

This document describes the deployment and configuration of a Wazuh Security Information and Event Management (SIEM) home lab using UTM virtualization on an Apple Silicon MacBook Air.

The objective was to establish a centralized security monitoring environment, connect a Linux endpoint, and prepare the lab for security event detection and investigation.

## 2. Lab Environment

| Component | Technology | Purpose |
|---|---|---|
| Host Machine | Apple Silicon MacBook Air | Physical host |
| Virtualization | UTM | Virtual machine management |
| SIEM Server | Ubuntu Server 22.04 LTS (ARM64) | Hosts Wazuh components |
| Monitored Endpoint | Kali Linux (ARM64) | Generates and forwards security events |
| SIEM Platform | Wazuh | Centralized monitoring and alert analysis |
| Endpoint Agent | Wazuh Agent | Collects endpoint security telemetry |
| Web Browser | Safari | Accesses the Wazuh dashboard |

## 3. Lab Architecture

The lab uses two virtual machines running on the same MacBook.

- **Ubuntu Server:** Hosts the Wazuh manager, indexer, and dashboard.
- **Kali Linux:** Runs the Wazuh agent and serves as the monitored endpoint.
- **UTM:** Provides virtualization and networking between the two machines.
- **Wazuh Dashboard:** Provides a web interface for reviewing security alerts and monitored endpoints.

### Data Flow

```text
Apple Silicon MacBook Air
        |
        v
    UTM Virtualization
        |
        +----------------------+
        |                      |
        v                      v
  Ubuntu Server            Kali Linux
  Wazuh Manager            Wazuh Agent
  Wazuh Indexer            OpenSSH Logs
  Wazuh Dashboard               |
        ^                       |
        |_______________________|
           Security Telemetry
```

## 4. Deployment Process

### 4.1 Ubuntu Server Installation

1. Created an ARM64-compatible Ubuntu Server virtual machine using UTM.
2. Installed Ubuntu Server 22.04 LTS.
3. Configured the virtual disk and removed the installation ISO after setup to prevent the installation process from repeating.
4. Configured networking to allow communication between the host and virtual machines.
5. Verified that Ubuntu booted successfully.

### 4.2 Wazuh Deployment

1. Installed the Wazuh components on the Ubuntu Server virtual machine.
2. Verified that the Wazuh services were running.
3. Accessed the Wazuh dashboard through a browser on the Mac host.
4. Resolved HTTPS certificate warnings associated with the local dashboard.
5. Confirmed that the dashboard was accessible.

### 4.3 Kali Linux Endpoint Configuration

1. Created a Kali Linux ARM64 virtual machine in UTM.
2. Installed and configured the Wazuh agent.
3. Registered the Kali endpoint with the Wazuh manager.
4. Verified that the agent appeared as active in the Wazuh dashboard.
5. Confirmed that the endpoint could generate security events for monitoring.

## 5. Troubleshooting

### ARM64 Compatibility

**Challenge:** Some installation methods and software packages expected a different processor architecture.

**Resolution:** Used ARM64-compatible Linux environments and adjusted the deployment approach to work with Apple Silicon virtualization.

### Virtual Machine Boot Configuration

**Challenge:** The Ubuntu installation process initially repeated after rebooting.

**Resolution:** Removed the installation ISO from the virtual machine configuration after Ubuntu was installed.

### HTTPS Dashboard Access

**Challenge:** The browser displayed certificate warnings when connecting to the local Wazuh dashboard.

**Resolution:** Verified dashboard connectivity and handled the locally generated HTTPS certificate warning in the controlled lab environment.

### Service and Network Connectivity

**Challenge:** Establishing reliable communication between the Wazuh server, dashboard, and monitored endpoint required troubleshooting.

**Resolution:** Checked service status, virtual machine networking, and connectivity until the Kali Linux agent appeared as active.

## 6. Deployment Results

The completed deployment established a working SIEM environment with:

- A Wazuh server running on Ubuntu Server
- An accessible Wazuh dashboard
- A connected Kali Linux endpoint
- Centralized collection of endpoint security events
- The ability to investigate SSH authentication-related alerts

The environment was subsequently used for a controlled SSH authentication failure investigation.

See [SSH Authentication Failure Investigation](02-ssh-bruteforce-investigation.md).

## 7. Evidence

Screenshots of the dashboard and connected endpoint will be added here as the repository documentation is organized.

## 8. Lessons Learned

This project provided practical experience with:

- Linux server deployment and configuration
- ARM64 virtualization on Apple Silicon
- SIEM installation and endpoint onboarding
- Service and network troubleshooting
- Centralized security monitoring
- Technical documentation and GitHub version control

## 9. Future Improvements

- Restore and verify the lab after the recent virtual machine shutdown
- Expand endpoint monitoring and detection scenarios
- Explore file integrity monitoring
- Document additional security investigations
- Continue improving the lab's architecture and documentation

