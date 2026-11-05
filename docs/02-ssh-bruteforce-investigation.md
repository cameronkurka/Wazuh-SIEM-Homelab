
# SSH Authentication Failure Investigation

## 1. Investigation Overview

This investigation demonstrates how a Security Information and Event Management (SIEM) platform can detect and analyze repeated failed SSH authentication attempts.

Using a Wazuh SIEM home lab, I generated controlled authentication failures on a Kali Linux endpoint and examined the resulting security alerts through the Wazuh dashboard.

**Objective:** Practice security event detection, log analysis, alert investigation, and MITRE ATT&CK mapping.

## 2. Lab Environment

| Component | Technology | Purpose |
|---|---|---|
| Host | Apple Silicon MacBook Air | Physical host system |
| Virtualization | UTM | Runs virtual machines |
| SIEM Server | Ubuntu Server 22.04 LTS | Hosts Wazuh |
| Monitored Endpoint | Kali Linux | Generates authentication events |
| Monitoring Agent | Wazuh Agent | Collects endpoint security events |
| Monitored Service | OpenSSH | Provides authentication logs |

The Kali Linux endpoint was enrolled in Wazuh and confirmed as an active monitored agent.

## 3. Investigation Methodology

1. Verified that the Kali Linux endpoint was connected to the Wazuh manager.
2. Confirmed that OpenSSH was available on the monitored endpoint.
3. Generated repeated failed SSH authentication attempts against a nonexistent user account in the controlled local lab.
4. Opened Wazuh Threat Hunting to review the resulting security alerts.
5. Examined alert metadata, including the affected endpoint, detection rule, severity, and MITRE ATT&CK mapping.

All activity was performed within an isolated, authorized home lab.

## 4. Detection Results

Wazuh detected the repeated authentication failures and generated security alerts.

| Alert Field | Observed Value |
|---|---|
| Agent Name | kali |
| Agent ID | 001 |
| Event Source | sshd |
| Detection Rule | 5712 |
| Rule Level | 10 |
| MITRE ATT&CK ID | T1110 |
| MITRE Tactic | Credential Access |
| MITRE Technique | Brute Force |
| Source Address | ::1 |
| Username | fakeuser |

The source address `::1` represents the local IPv6 loopback address, confirming that the test originated locally rather than from an external attacker.

The detection demonstrated that Wazuh could identify and classify repeated SSH authentication failures on the monitored endpoint.

## 5. Security Analysis

The Wazuh alert identified activity consistent with a brute-force authentication pattern.

The investigation provided experience with:

- Reviewing security alerts and authentication logs
- Identifying the affected endpoint and account
- Interpreting rule severity and detection metadata
- Mapping observed activity to MITRE ATT&CK
- Distinguishing controlled test activity from a real external attack

The alert alone does not establish that an account was compromised. This investigation focused on detecting and analyzing failed authentication attempts.

## 6. Evidence

Screenshots captured during the investigation document the Wazuh dashboard, monitored endpoint connection, and authentication-related security alerts.

Additional evidence will be linked here as the repository documentation is organized.

## 7. Lessons Learned

This investigation reinforced the importance of centralized security monitoring, endpoint visibility, and authentication log analysis.

It also demonstrated how MITRE ATT&CK can provide context for detected activity and help analysts interpret security alerts.

## 8. Future Improvements

- Expand authentication monitoring scenarios
- Practice investigating additional Linux security events
- Document alert triage and response recommendations
- Explore file integrity monitoring and account-change detection
- Develop structured incident investigation reports
