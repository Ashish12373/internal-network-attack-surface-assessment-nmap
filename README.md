# Internal Network Attack Surface Assessment using Nmap (SOC Case Study)

## Overview
This project documents a SOC-style internal network attack surface assessment performed in a controlled lab environment. The objective was to identify exposed services, analyze operating system characteristics, validate port behavior, and assess security risk from a defensive (blue-team) perspective.

The investigation follows realistic SOC workflows focused on visibility, validation, and risk-based analysis rather than exploitation. All findings are supported by raw scan evidence generated during the assessment.

---

## Environment Details

| Attribute | Value |
|---------|------|
| Target IP | 192.168.56.10 |
| Network Type | Internal / Host-only |
| Host Role | Linux server hosting SIEM components |
| Virtualization | Oracle VirtualBox |
| Tool Used | Nmap 7.98 |
| Scope | Authorized internal testing |

---

## Objectives

- Identify exposed TCP and UDP services on an internal host  
- Perform OS fingerprinting and analyze ambiguity in detection  
- Validate service exposure using multiple scan techniques  
- Analyze port states and firewall behavior  
- Reduce false positives through cross-validation  
- Translate technical findings into SOC-relevant risk insights  

---

## Methodology

The following Nmap techniques were used to reflect real-world SOC investigation workflows:

- OS Fingerprinting (`-O`)
- Service and Version Enumeration (`-sV`)
- TCP SYN (Stealth) Scanning (`-sS`)
- UDP Scanning (`-sU`)
- Full Port Scan with Reason Analysis (`--reason -p-`)
- Vulnerability Scanning using NSE (`--script vuln`)

Multiple scan types were intentionally used to validate findings and reduce false positives.

---

## Phase 1: Host Availability & OS Detection

**Command**

**Findings**
- Host was reachable with minimal latency
- OS fingerprinting returned multiple candidates:
  - Linux kernel 4.x–5.x
  - MikroTik RouterOS (lower confidence)
- Network distance: 1 hop

**Analysis**
OS fingerprinting produced ambiguous results, which is common in virtualized or hardened environments. Instead of forcing a conclusion, OS identification was validated later using service fingerprinting, banner analysis, and TCP/IP behavior.

---

## Phase 2: Service & Version Enumeration

**Command**

**Discovered Services**

| Port | Protocol | Service | Description |
|----|--------|--------|------------|
| 22 | TCP | SSH | Remote administration |
| 5432 | TCP | PostgreSQL | Database service |
| 8000 | TCP | HTTP | Splunk web interface |
| 8089 | TCP | HTTPS | Splunk management API |
| 9997 | TCP | TCP | Splunk ingestion |
| 9998 | TCP | TCP | Splunk ingestion |
| 8191 | TCP | TCP | Auxiliary service |

**Analysis**
The presence of multiple Splunk management and ingestion ports classified this host as **high-value SIEM infrastructure**, making it a critical internal asset from a SOC perspective.

---

## Phase 3: TCP SYN (Stealth) Scan

**Command**

**Findings**
- Open ports matched service enumeration results
- Scan completed in under one second
- No discrepancies observed

**Analysis**
Matching results across scan types increased confidence in service exposure and reduced the likelihood of false positives.

---

## Phase 4: UDP Scan

**Command**

**Findings**

| Port | Protocol | State | Service |
|----|--------|------|--------|
| 5353 | UDP | open|filtered | Zeroconf |

**Analysis**
UDP scanning required extended time (~18 minutes) and returned limited results. The `open|filtered` state reflects real-world firewall behavior and does not conclusively indicate service exposure. No critical UDP services were identified.

---

## Phase 5: Full Port Scan & Port-State Reasoning

**Command**

**Findings**

| Port | Protocol | State | Service |
|----|--------|------|--------|
| 5353 | UDP | open|filtered | Zeroconf |

**Analysis**
UDP scanning required extended time (~18 minutes) and returned limited results. The `open|filtered` state reflects real-world firewall behavior and does not conclusively indicate service exposure. No critical UDP services were identified.

---

## Phase 5: Full Port Scan & Port-State Reasoning

**Command**

**Findings**
- No critical vulnerabilities detected
- Informational results only
- HTTP enumeration revealed `/robots.txt`

**Analysis**
Automated vulnerability scan results were manually reviewed to eliminate false positives. No actionable vulnerabilities were identified.

---

## Risk Analysis (SOC Perspective)

### High-Value Exposed Services
- SSH (remote access)
- PostgreSQL (database service)
- Splunk web, management, and ingestion interfaces

### Risk Interpretation
While these services are expected in enterprise environments, they represent elevated risk if credentials are compromised. Exposure of SIEM infrastructure is particularly sensitive due to its impact on monitoring, detection, and incident response capabilities.

---

## Recommendations

- Restrict Splunk management interfaces to administrative IP ranges
- Enforce strong authentication and logging for SSH access
- Monitor database access patterns for anomalies
- Correlate service access events within SIEM for detection engineering

---

## Key Takeaways

- OS fingerprinting ambiguity is common and must be validated
- Multiple scan techniques significantly reduce false positives
- Raw scan data requires analyst interpretation
- Internal reconnaissance is critical for SOC visibility and risk assessment

---

## Conclusion

This project demonstrates a realistic SOC analyst workflow involving internal reconnaissance, validation, and risk-based decision making. The assessment improved asset visibility, reduced uncertainty in service exposure, and translated technical findings into actionable security insights.

---

## Ethical Notice

All scans were performed in a controlled lab environment on systems owned by the author. No unauthorized scanning or testing was conducted.

---

## Author Notes

This case study is intended to demonstrate defensive security skills relevant to SOC Analyst and Security Analyst roles, emphasizing validation, accuracy, and risk awareness over tool-driven assumptions.
