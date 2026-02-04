# SahilCySA
This repository showcases my hands-on cybersecurity lab work focused on access control, authentication, authorization, and incident analysis. Each lab reflects real-world security scenarios, emphasizes analytical thinking, and follows industry best practices. 

# 🔐 Google Cybersecurity Professional Certificate - Hands-On Labs Portfolio


## 🧪 Lab 1: Access Control & Authorization Incident Analysis

### 🧭 Context of the Work
This lab simulates a real-world **access control failure** scenario where a former contractor retained system access after termination. The objective was to analyze authentication and authorization data, identify security gaps, and recommend preventive controls aligned with standard security governance practices.

This exercise reflects common issues faced by organizations related to **identity lifecycle management**, **least privilege enforcement**, and **access revocation failures**.

---

### 🎯 Lab Objective
- Identify indicators of unauthorized access
- Analyze authentication and authorization issues
- Assess risk caused by improper access control
- Recommend security controls to prevent recurrence

---

### 🛠️ Tools & Concepts Used
- Access Control Analysis
- Authentication & Authorization Review
- Identity and Access Management (IAM) Principles
- Security Documentation & Risk Assessment

---

### 📋 Incident Details

**User Role:** Legal / Administrator  
**System Name:** Up2-NoGud  
**IP Address:** 152.207.255.255  
**Date & Time of Event:** 10/03/2023 – 8:29 AM  

---

### 🔍 Threat Indicators Identified
- System access activity traced to an **administrator-level account**
- Account belonged to a **former contractor**
- Contractor’s last active employment date: **12/27/2019**
- Access event occurred nearly **four years after termination**

---

### 🚨 Authorization Issues Identified
- Access rights were **not revoked** after contractor offboarding
- Former contractor retained **administrator-level permissions**
- No apparent access review or account expiration enforcement

---

### 🧠 Security Analysis
The incident highlights a breakdown in **user access lifecycle management**. Retaining privileged access for inactive users significantly increases the risk of unauthorized access, insider threats, and regulatory non-compliance.

This scenario demonstrates how failures in **authorization controls** can undermine otherwise functional authentication mechanisms.

---

### 🛡️ Recommendations & Mitigations
- Implement formal **access revocation procedures** immediately upon employee or contractor termination
- Enforce **Multi-Factor Authentication (MFA / 2FA)** for all administrative accounts
- Conduct **periodic access reviews** to validate user privileges
- Apply the **Principle of Least Privilege (PoLP)** to all roles

---

### 📈 Skills Demonstrated
- Access control analysis
- Authorization vs authentication assessment
- Risk identification and mitigation planning
- Security documentation and reporting
- IAM fundamentals

---

### 📚 Related Frameworks & Best Practices
- NIST Access Control (AC) Family
- Identity Lifecycle Management
- Least Privilege Principle
- Zero Trust Concepts

---

### 🏁 Key Takeaway
This lab reinforced the importance of strong access governance and continuous access monitoring. Even a single overlooked account can lead to serious security exposure if proper access controls are not enforced.

---

## 🧪 Lab 2: Python Automation for Access Control List (ACL) Management

### 🧭 Context of the Work
This lab focuses on **automating access control maintenance** using Python. In real-world security operations, allow lists (such as IP allow lists or firewall rules) must be continuously updated to remove unauthorized or risky IP addresses.

The objective of this lab was to design an algorithm that programmatically reviews an allow list and removes IP addresses that appear in a predefined removal list. This reflects common **SOC and IAM automation tasks** used to reduce manual effort and prevent access control misconfigurations.

---

### 🎯 Lab Objective
- Automate the management of IP-based access controls
- Ensure unauthorized IP addresses are removed from allow lists
- Demonstrate secure file handling and list manipulation using Python
- Apply basic security automation principles

---

### 🛠️ Tools & Technologies Used
- Python
- File Handling (`open()`, `with`)
- List Operations
- Access Control Concepts
- Automation Logic

---

### 📋 Problem Description
An allow list file contains a list of IP addresses that are permitted access to a system. A separate list (`removed_list`) contains IP addresses that should no longer have access.

The task was to:
- Read the allow list from a file
- Compare it against the removal list
- Remove any matching IP addresses
- Update the file with the revised, secure list

---

### 🔍 Algorithm Overview
1. Open the file containing the IP allow list
2. Read the file contents
3. Convert the string data into a list of IP addresses
4. Iterate through the `removed_list`
5. Remove matching IP addresses from the allow list
6. Write the updated IP list back to the file

---

### 🧠 Security Analysis
Manually maintaining access control lists is error-prone and does not scale well in enterprise environments. This automation reduces the risk of:
- Retaining unauthorized IP access
- Configuration drift
- Human error during access updates

The algorithm supports **defense-in-depth** by ensuring access rules stay current and enforce security policies consistently.

---

### 🛡️ Security Use Case
- Removing decommissioned system IPs
- Revoking access after security incidents
- Maintaining firewall or application allow lists
- Supporting Zero Trust access enforcement

---

### 📈 Skills Demonstrated
- Python scripting for cybersecurity
- Secure file operations
- Automation of access control tasks
- Logical problem solving
- Security-focused algorithm design

---

### 📚 Related Frameworks & Concepts
- NIST Access Control (AC)
- Identity and Access Management (IAM)
- Least Privilege Principle
- Security Automation & Orchestration

---

### 🏁 Key Takeaway
This lab demonstrates how simple Python automation can significantly improve access control hygiene. Automating allow list updates helps security teams respond faster to changes and maintain stronger security postures with minimal manual effort.

---

## 🧪 Lab 3: Network Attack Analysis – Denial of Service (SYN Flood)

### 🧭 Context of the Work
This lab simulates a real-world **network availability incident** affecting a public-facing website. Users experienced connection timeout errors, prompting an investigation into potential malicious activity targeting the web server.

The objective was to analyze network behavior, interpret log data, and identify whether the outage was caused by a cyberattack. This exercise mirrors common **SOC analyst responsibilities**, including attack identification, protocol analysis, and incident reporting.

---

### 🎯 Lab Objective
- Identify the type of network attack causing service disruption
- Analyze how the attack impacts system availability
- Explain the attack using TCP/IP networking concepts
- Document findings in an incident report format

---

### 🛠️ Tools & Concepts Used
- Network Traffic Analysis
- TCP/IP Protocols
- Log Interpretation
- Denial of Service (DoS) Concepts
- Incident Documentation

---

### 🚨 Incident Overview
- **Issue Observed:** Website connection timeout errors
- **Affected Asset:** Web server
- **Impact:** Legitimate users unable to establish connections
- **Primary Concern:** Loss of availability

---

### 🔍 Attack Identification
Based on log analysis, the most likely cause of the network interruption is a **Denial of Service (DoS) attack**, specifically a **SYN flood attack**.

Indicators included:
- High volume of SYN packets
- Server becoming unresponsive
- Failure to complete TCP handshakes

---

### 🧠 Technical Analysis – How the Attack Works
The TCP three-way handshake is required to establish a connection:

1. A **SYN** packet is sent by the client to initiate a connection
2. The server responds with a **SYN-ACK** and reserves resources
3. The client completes the handshake with an **ACK**

In a SYN flood attack:
- An attacker sends a massive number of SYN packets
- The server allocates resources for each request
- The final ACK is never sent
- Server resources become exhausted

As a result, legitimate users cannot complete new connections and receive timeout errors.

---

### 📉 Impact Assessment
- Server resources fully consumed
- Legitimate traffic denied access
- Website availability disrupted
- Potential business and reputational impact

---

### 🛡️ Mitigation & Defensive Measures
- Enable SYN cookies on the web server
- Implement rate limiting and connection throttling
- Deploy intrusion detection/prevention systems (IDS/IPS)
- Use DDoS protection services or load balancers
- Monitor traffic for abnormal SYN packet patterns

---

### 📈 Skills Demonstrated
- Network attack identification
- TCP/IP protocol analysis
- DoS and SYN flood understanding
- Log-based incident investigation
- Security incident documentation

---

### 📚 Related Frameworks & Concepts
- NIST Incident Response Lifecycle
- CIA Triad (Availability)
- Network Security Fundamentals
- SOC Incident Analysis Workflow

---

### 🏁 Key Takeaway
This lab demonstrates how availability-focused attacks can disrupt critical services without compromising data. Understanding TCP behavior and attack patterns is essential for detecting and responding to network-based threats in a SOC environment.

---


---

