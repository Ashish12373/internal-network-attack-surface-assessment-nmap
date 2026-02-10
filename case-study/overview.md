# Case Study Overview

This case study documents a SOC-style internal network attack surface assessment conducted in a controlled lab environment. The objective was to identify exposed services, validate operating system characteristics, and understand potential security risks from a defensive perspective.

Rather than focusing on exploitation, the assessment emphasizes visibility, validation, and risk-aware analysis — core responsibilities of a SOC Analyst. Multiple Nmap scan techniques were used to confirm findings, reduce false positives, and ensure accuracy of results.

The target system represented a high-value internal server hosting critical services, including SIEM components. The investigation followed a structured workflow similar to enterprise SOC operations, beginning with host availability and progressing through OS fingerprinting, service enumeration, port-state analysis, and lightweight vulnerability assessment.

All raw scan outputs are preserved in this repository to provide transparency and allow independent verification of findings.
