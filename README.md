# Community Bank Incident Remediation and Security Architecture Redesign

## Project Overview
In early 2025, a community bank employing approximately 200 staff suffered a prolonged and undetected cyberattack. The attackers gained initial access through a phishing email and successfully moved laterally across the organization's flat network, compromising ATM systems, teller workstations, Linux servers, and cloud hosted services. The breach remained hidden until a third party audit discovered the suspicious activity, triggering mandatory GLBA disclosure. 

This repository documents the comprehensive root cause analysis and the subsequent $400,000 proposed security architecture overhaul designed to rebuild a resilient, segmented, and heavily monitored environment.

## Root Cause and Vulnerability Analysis
The attackers, suspected to be a nation state Advanced Persistent Threat (APT), exploited several systemic technical and operational vulnerabilities. 

**Key findings from the post incident analysis include:**
* A completely flat network architecture existed with no separation between highly critical ATM systems, teller terminals, and internal computer networks.
* The organization lacked any Endpoint Detection and Response (EDR) or Security Information and Event Management (SIEM) solutions, resulting in total blindness to malicious lateral movement.
* Remote access was conducted through personally owned laptops connected via unsecured VPNs.
* Remote devices lacked encryption, Mobile Device Management (MDM) enrollment, and Multi Factor Authentication (MFA) enforcement.
* Backup systems were neither frequently tested nor encrypted, drastically increasing the risk associated with potential ransomware attacks.

## The Remediation Architecture
To address these critical vulnerabilities, I proposed a phased security overhaul prioritizing network segmentation, device hardening, and centralized monitoring. The selected technologies balance robust functionality with budget efficiency.

### Core Architectural Enhancements:
* **Network Segmentation:** Deployed Cisco Catalyst switches and Fortinet FortiGate 60F firewalls to create strict VLANs isolating Admins, Tellers, ATMs, and Remote devices.
* **Public Services DMZ:** Engineered a DMZ utilizing an NGINX reverse proxy, ModSecurity Web Application Firewall (WAF), and Snort IDS to securely filter traffic for web and mobile banking applications.
* **Endpoint Hardening:** Rolled out Microsoft Defender for Endpoint P2 paired with native AppLocker controls and Wazuh agents across all 200 endpoints.
* **SIEM and Logging:** Implemented an open source ELK Stack integrated with Wazuh Manager to provide real time alerting and behavior based threat detection.
* **Identity and Access Management (IAM):** Centralized identity management through Azure Active Directory P1, strictly enforcing Microsoft Entra MFA and Role Based Access Control (RBAC).
* **Secure Backups:** Automated encrypted database backups utilizing Wasabi cloud storage and Veeam orchestration to ensure business continuity.

## Regulatory Compliance and Success Metrics
This architecture was specifically engineered to align with the regulatory mandates governing financial institutions, including the Gramm Leach Bliley Act (GLBA), the FFIEC Cybersecurity Framework, and PCI DSS. 

**To validate the effectiveness of these security controls, the following Key Performance Indicators will be tracked:**
* Maintaining phishing simulation click rates below 5 percent.
* Achieving over 95 percent device enrollment in both EDR and MDM platforms.
* Demonstrating the ability to restore critical systems from encrypted cloud backups within a two hour window during quarterly tests.
* Eliminating critical unpatched systems within seven days of vendor release.
* Measurable reductions in Mean Time to Detect (MTTD) and Mean Time to Respond (MTTR) driven by the new SIEM integration.

## Conclusion
This project illustrates a critical transition from a reactive, vulnerable flat network to a highly segmented, proactive, and policy driven infrastructure. By directly addressing the root causes of the initial breach, this architecture minimizes the attack surface, hardens user access, and ensures the bank can maintain operational continuity and customer trust in a digital first era.
