# Wazuh SIEM Home Lab

## Overview

This repository documents the design, deployment, and operation of a Security Information and Event Management (SIEM) home lab built using Wazuh.

The lab was created to develop practical Security Operations Center (SOC) analyst skills including endpoint monitoring, log analysis, incident investigation, and threat detection using real security events.

The environment consists of an Ubuntu Server running the Wazuh Manager and Dashboard with a Kali Linux endpoint configured as a monitored agent. Simulated attacks are performed to validate detection capabilities and investigate alerts using the Wazuh Dashboard and the MITRE ATT&CK framework.

---

## Project Objectives

- Build an enterprise-style SIEM lab
- Configure centralized log collection
- Monitor Linux endpoints
- Detect common attack techniques
- Investigate security alerts
- Map detections to the MITRE ATT&CK framework
- Document investigations like a SOC analyst

---

## Lab Environment

| Component | Technology |
|-----------|------------|
| Host Machine | Apple Silicon MacBook Air |
| Hypervisor | UTM |
| SIEM Platform | Wazuh |
| SIEM Server | Ubuntu Server 22.04 LTS |
| Endpoint | Kali Linux |
| Communication | Wazuh Agent |

---

## Skills Demonstrated

- Linux Administration
- SIEM Administration
- Endpoint Monitoring
- Log Analysis
- Threat Hunting
- Incident Response
- MITRE ATT&CK
- SSH Monitoring
- Security Event Investigation

---

## Current Investigations

- [x] Wazuh Installation
- [x] Kali Agent Enrollment
- [x] SSH Authentication Failure Detection
- [ ] User Creation Detection
- [ ] File Integrity Monitoring
- [ ] Privilege Escalation Detection
- [ ] Vulnerability Detection
- [ ] Windows Endpoint Monitoring
- [ ] Sysmon Integration
- [ ] Sigma Rule Detection

---

## Architecture

*(Architecture diagram coming soon.)*

---

## Future Improvements

- Add Windows endpoint monitoring
- Deploy Sysmon
- Integrate Sigma rules
- Build custom Wazuh detection rules
- Simulate ransomware activity
- Simulate privilege escalation attacks
- Add Suricata network monitoring
- Create SOC-style incident reports
