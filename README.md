# internal-network-attack-surface-assessment-nmap
# Internal Network Attack Surface Assessment using Nmap (SOC Case Study)

## Overview
This repository documents a SOC-style internal network reconnaissance and attack surface assessment conducted in a controlled lab environment. The objective was to identify exposed services, validate operating system characteristics, analyze port behavior, and assess security risk from a defensive (blue-team) perspective.

## Objectives
- Improve internal asset and service visibility
- Identify exposed and high-value services
- Validate OS fingerprinting ambiguity
- Reduce false positives through multi-scan verification
- Translate scan data into SOC-relevant risk insights

## Tools Used
- Nmap 7.98
- Linux & Windows hosts (Virtualized)
- Internal host-only network

## Investigation Phases
1. Host discovery and availability confirmation
2. OS fingerprinting and validation
3. Service and version enumeration
4. TCP SYN (stealth) scanning
5. UDP exposure analysis
6. Port-state reasoning
7. Lightweight vulnerability assessment

## Key Findings
- Identified multiple exposed TCP services, including critical SIEM infrastructure
- OS fingerprinting produced ambiguous results, requiring validation via service correlation
- TCP and UDP scans confirmed expected internal exposure with minimal false positives
- No critical vulnerabilities detected after manual validation

## Repository Structure
- `/scans` → Raw Nmap scan outputs (evidence)
- `/case-study` → SOC analysis and risk interpretation
- `/methodology` → Techniques and rationale used

## Ethical Notice
All scans were performed in a controlled lab environment on systems owned by the author. No unauthorized testing was conducted.
