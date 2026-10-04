# SahilCySA
This repository showcases my hands-on cybersecurity lab work focused on access control, authentication, authorization, and incident analysis. Each lab reflects real-world security scenarios, emphasizes analytical thinking, and follows industry best practices. 

# Project 1: Static Analysis of a Simple Malware Sample

## Introduction
Static analysis is the process of analyzing malware without executing it. This method involves examining the file's code and structure to gain insights into its functionality and behavior. In this project, you will perform static analysis on a simple malware sample using various tools to extract information such as strings, PE headers, imports/exports, and embedded resources.

## Pre-requisites
- Basic understanding of malware and its types.
- Familiarity with Windows operating system internals.
- Knowledge of programming languages like C/C++ (optional but helpful).
- Familiarity with common malware analysis tools.

## Lab Set-up
- Operating System: A Windows virtual machine (VM) is recommended. You can use VirtualBox or VMware to create a VM.
- Malware Sample: Obtain a known and safe-to-analyze malware sample from a reputable source like MalwareBazaar.

## Tools:
- PEview: For examining PE headers.
- Strings: For extracting strings from the binary.
- Dependency Walker: For analyzing imports and exports.
- Resource Hacker: For viewing embedded resources.
- Hex Editor (HxD): For examining the binary at a low level.
- Ensure that your VM is isolated from your main network to prevent accidental infection.

## Exercises
### Exercise 1: Extracting Strings

Objective: Extract and analyze strings from the malware sample to gather initial clues about its functionality.


Step 1: Use Strings.exe from Sysinternals.
Step 2: Run Command
```shell
strings malware_sample.exe > strings_output.txt
```
Step 3: Analysis
Open strings_output.txt.
Look for URLs, IP addresses, file paths, registry keys, and other readable text.
Identify any suspicious or noteworthy strings.

Step 4: Retreive the output
After running the strings command, you might find URLs that could indicate command-and-control servers or file paths showing where the malware operates. 

Example findings:
```
Copy code
http://malicious-site.com
C:\Windows\System32\malicious.dll
HKEY_LOCAL_MACHINE\Software\Malware
```

### Exercise 2: Analyzing the PE Header

Objective: Examine the PE header to understand the structure and metadata of the malware sample.


Step 1: Open the malware sample in PEview.
Step 2: Analysis
- Review the sections (e.g., .text, .data, .rdata).
- Note the entry point, which is where the execution starts.
- Check the timestamp to see when the file was compiled.

Step 3: Retreive the output
In PEview, you might observe the following:
- sections
  ```
  kotlin
  Copy code
  .text (code section)
  .data (initialized data)
  .rdata (read-only data)
  ```
- Entry Point: Located in the .text section.
- Timestamp: Indicates the compile date, which can be compared with known malware activity timelines.

### Exercise 3: Inspecting Imports and Exports

Objective: Identify functions that the malware imports from system libraries and any exported functions.



Step 1: Use Dependency Walker.
Step 2: Analysis
- Load the malware sample in Dependency Walker.
- Examine imported functions and their corresponding libraries.
- Check for any exported functions.

Step 3: Solution
You might find the malware imports functions related to networking (e.g., WSAStartup, connect) and file operations (e.g., CreateFile, WriteFile). This indicates potential capabilities like network communication and file manipulation.

Exercise 4: Viewing Embedded Resources

Objective: Examine any resources embedded within the malware sample.



Step 1: Open the malware sample in Resource Hacker.
Step 2: Analysis
Browse through different resource types (e.g., icons, dialogs, strings).
Identify any suspicious or unusual resources.
Step 3: Solution
In Resource Hacker, you may find:

- Icons: Custom icons used by the malware.
- Dialogs: Fake error messages or GUI components.
- Strings: Hardcoded messages or paths.

### Exercise 5: Hex Analysis

Objective: Perform a low-level examination of the binary to uncover any hidden data or patterns.


Step 1:Open the malware sample in HxD (or any hex editor).
Step 2: Analysis
Browse through the binary data.
Look for any readable text or unusual patterns.
Step 3: Solution
In HxD, you might see obfuscated strings or encrypted data. Recognizable patterns could indicate embedded code or data structures.

By completing these exercises, you'll gain a solid foundation in static malware analysis, enabling you to extract valuable information without executing potentially harmful code.

# Project 2: Dynamic Analysis in a Controlled Environment

## Introduction
Dynamic analysis involves executing malware in a controlled and isolated environment to observe its behavior. This approach allows you to monitor how the malware interacts with the system, such as file modifications, network communications, and changes to the registry. In this project, you will perform dynamic analysis on a simple malware sample to understand its operational characteristics.

## Pre-requisites
- Basic understanding of malware and its types.
- Familiarity with Windows operating system internals.
- Understanding of virtual machines and their configuration.
- Knowledge of networking and system monitoring tools.

## Lab Set-up
1. Operating System: Use a Windows virtual machine (VM) created using VirtualBox or VMware.
2. Malware Sample: Obtain a known and safe-to-analyze malware sample from a reputable source like MalwareBazaar.
3. Tools:
- Procmon (Process Monitor): For monitoring file system, registry, and process/thread activity.
- Wireshark: For capturing and analyzing network traffic.
- RegShot: For comparing registry snapshots.
- FakeNet-NG: For simulating network services to capture malware communication.

Ensure your VM is isolated from your main network and has a snapshot taken before analysis to easily revert to a clean state.

## Exercise: Monitoring Malware Behavior with Process Monitor
Objective: Execute the malware sample in a controlled environment and use Process Monitor to observe its behavior, including file, registry, and process activity.

Step 1: Set Up the Environment

- Ensure the VM is isolated from your main network.
- Install and configure the necessary tools: Procmon, Wireshark, RegShot, and FakeNet-NG.
- Take a snapshot of the VM for easy restoration.

Step 2: Initial Snapshot

- Use RegShot to take an initial snapshot of the registry.
- Run FakeNet-NG to simulate network services.

Step 3: Execute the Malware Sample

- Start Procmon to begin monitoring.
- Execute the malware sample within the VM.
- Observe and record the behavior of the malware in real-time.

Step 4: Collect Data:

- Let the malware run for a few minutes, capturing all activities with Procmon.
- Stop Procmon and save the captured events log.
- Use Wireshark to capture network traffic during the execution.

Step 5: Analyze the Collected Data

- File System Activity: In Procmon, filter events to focus on file system activity. Identify files created, modified, or deleted by the malware.
- Registry Activity: Filter events to examine registry changes. Look for new keys, modified values, or deleted entries.
- Process and Thread Activity: Check for new processes or threads spawned by the malware.
- Network Activity: Analyze Wireshark captures to identify communication attempts, such as connecting to external IP addresses or domains.

Step 6: Post-execution Snapshot

- Use RegShot to take a second snapshot of the registry.
- Compare the two snapshots to identify changes made by the malware.

## Expected Output

- File System Activity: In Procmon, you might observe the malware creating or modifying files in the system directory or user profile folders. Example findings:

```
Created: C:\Users\Public\malicious_file.exe
Modified: C:\Windows\System32\drivers\etc\hosts

```
- Registry Activity: You may find the malware adding new registry entries to establish persistence or modify existing keys to alter system behavior. Example findings:
```
Added: HKCU\Software\Microsoft\Windows\CurrentVersion\Run\Malware
Modified: HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters
```
- Process and Thread Activity: The malware might spawn new processes or inject code into existing ones. Example findings:
```
Created: Process PID 1234 (malicious_process.exe)
Injected: Thread into explorer.exe
```

- Network Activity: In Wireshark, you could observe the malware attempting to communicate with external servers, which may include sending HTTP requests or establishing TCP connections. Example findings:
```
GET http://malicious-domain.com/command
TCP connection to 192.168.1.100:8080
```

By completing this exercise, you will gain practical experience in dynamic malware analysis, allowing you to identify and understand the behavior and impact of malicious software in a controlled and safe environment.


# Project 3: Analyzing a Ransomware Sample

## Introduction
Ransomware is a type of malware that encrypts a victim's files and demands payment for the decryption key. Understanding how ransomware operates can help in developing strategies to defend against it and respond to incidents. In this project, you will analyze a ransomware sample to understand its encryption mechanism, ransom note delivery, and other behaviors.

## Pre-requisites
- Basic understanding of malware and its types, particularly ransomware.
- Familiarity with Windows operating system internals.
- Knowledge of encryption basics.
- Familiarity with dynamic analysis tools.

## Lab Set-up
1. Operating System: Use a Windows virtual machine (VM) created using VirtualBox or VMware.
2. Ransomware Sample: Obtain a known and safe-to-analyze ransomware sample from a reputable source like MalwareBazaar.
3. Tools:
  - Procmon (Process Monitor): For monitoring file system, registry, and process/thread activity.
  - Wireshark: For capturing and analyzing network traffic.
  - RegShot: For comparing registry snapshots.
  - FakeNet-NG: For simulating network services to capture malware communication.
  - HxD (Hex Editor): For examining binary data.
  - AES Crypt: For testing encryption mechanisms.
Ensure your VM is isolated from your main network and has a snapshot taken before analysis to easily revert to a clean state.

## Exercise: Analyzing the Encryption Mechanism of the Ransomware
Objective: Execute the ransomware sample in a controlled environment to understand its encryption mechanism and analyze its behavior, including file encryption and ransom note delivery.

Step 1: Set Up the Environment:

- Ensure the VM is isolated from your main network.
- Install and configure the necessary tools: Procmon, Wireshark, RegShot, and FakeNet-NG.
- Take a snapshot of the VM for easy restoration.

Step 2: Initial Snapshot:

- Use RegShot to take an initial snapshot of the registry.
- Create some test files (e.g., text documents, images) to observe encryption.

Step 3: Execute the Ransomware Sample:

- Start Procmon to begin monitoring.
- Execute the ransomware sample within the VM.
- Observe and record the behavior of the ransomware in real-time.

Step 4: Collect Data:

- Let the ransomware run until it completes its encryption process and displays a ransom note.
- Stop Procmon and save the captured events log.
- Use Wireshark to capture network traffic during the execution.

Step 5: Analyze the Collected Data:

- File System Activity: In Procmon, filter events to focus on file system activity. Identify files that were encrypted by the ransomware.
- Registry Activity: Filter events to examine registry changes. Look for new keys, modified values, or deleted entries.
- Encryption Analysis: Identify the encryption algorithm used by examining encrypted files and comparing them to their original versions.

Step 6: Post-execution Snapshot:

- Use RegShot to take a second snapshot of the registry.
- Compare the two snapshots to identify changes made by the ransomware.

# Expected Output

- File System Activity: In Procmon, you might observe the ransomware encrypting files in user directories and appending a specific extension to them. Example findings:

```
Modified: C:\Users\Public\Documents\example.txt -> C:\Users\Public\Documents\example.txt.encrypted
Created: C:\Users\Public\Documents\READ_ME.txt (ransom note)
```

- Registry Activity: You may find the ransomware adding new registry entries to establish persistence or modifying existing keys to alter system behavior. Example findings:

```
Added: HKCU\Software\Ransomware\EncryptedFiles
Modified: HKLM\SYSTEM\CurrentControlSet\Services\Tcpip\Parameters
```

- Encryption Analysis:

- Compare the encrypted files with the original versions to identify the encryption algorithm. You might use tools like HxD to look for patterns in the encrypted data.
- If the ransomware uses a known encryption algorithm (e.g., AES), you may identify typical characteristics such as block size and structure. Example analysis:
```
Original file size: 1 KB
Encrypted file size: 1 KB (indicating block cipher)
Hex pattern analysis: Encrypted data does not show simple repeating patterns, indicating strong encryption.
```
- Ransom Note Analysis: Examine the ransom note file (READ_ME.txt) created by the ransomware. It typically contains instructions for payment and may include a contact email or a URL for payment.


By completing this exercise, you will gain practical experience in analyzing ransomware, understanding its encryption mechanisms, and identifying how it demands ransom from victims. This knowledge is crucial for developing effective defense and response strategies against ransomware attacks.


# Project 4: Behavioral Analysis of a Keylogger

## Introduction
Keyloggers are a type of malware that records keystrokes to capture sensitive information, such as passwords and personal messages. Understanding how keyloggers operate is crucial for detecting and mitigating their impact. In this project, you will analyze a keylogger sample to observe its behavior, including how it captures and stores keystrokes.

## Pre-requisites
- Basic understanding of malware and its types, particularly keyloggers.
- Familiarity with Windows operating system internals.
- Knowledge of system monitoring and analysis tools.
- Understanding of virtual machines and their configuration.

## Lab Set-up
1. Operating System: Use a Windows virtual machine (VM) created using VirtualBox or VMware.
2. Keylogger Sample: Obtain a known and safe-to-analyze keylogger sample from a reputable source like MalwareBazaar.
3. Tools:
  - Procmon (Process Monitor): For monitoring file system, registry, and process/thread activity.
  - Wireshark: For capturing and analyzing network traffic.
  - RegShot: For comparing registry snapshots.
  - Sysinternals Autoruns: For examining startup entries.
  - Text Editor: For examining log files created by the keylogger.
Ensure your VM is isolated from your main network and has a snapshot taken before analysis to easily revert to a clean state.

## Exercise: Monitoring Keystroke Logging Activity
Objective: Execute the keylogger sample in a controlled environment and use Process Monitor to observe its behavior, including how it captures keystrokes and where it stores the logged data.

Step 1: Set Up the Environment:
- Ensure the VM is isolated from your main network.
- Install and configure the necessary tools: Procmon, Wireshark, RegShot, and Sysinternals Autoruns.
- Take a snapshot of the VM for easy restoration.

Step 2: Initial Snapshot:

- Use RegShot to take an initial snapshot of the registry.

Step 3: Execute the Keylogger Sample:

- Start Procmon to begin monitoring.
- Execute the keylogger sample within the VM.
- Perform typical user activities (e.g., typing in a text editor) to generate keystroke data.
  
Step 4: Collect Data:

- Let the keylogger run for a few minutes, capturing keystrokes.
- Stop Procmon and save the captured events log.

Step 5: Analyze the Collected Data:

- File System Activity: In Procmon, filter events to focus on file system activity. Identify any files created or modified by the keylogger, particularly those that might store logged keystrokes.
- Registry Activity: Filter events to examine registry changes. Look for new keys or modified values associated with the keylogger.
- Process and Thread Activity: Check for any processes or threads spawned by the keylogger.
- Log File Analysis: Locate and examine any log files to understand the format and content of captured keystrokes.

Step 6: Post-execution Snapshot:

- Use RegShot to take a second snapshot of the registry.
- Compare the two snapshots to identify changes made by the keylogger.

## Expected Solution/Output

- File System Activity: In Procmon, you might observe the keylogger creating or modifying log files in user directories. Example findings:

```
Created: C:\Users\Public\Documents\keylog.txt
Modified: C:\Users\Public\Documents\keylog.txt
```

- Registry Activity: You may find the keylogger adding new registry entries to establish persistence. Example findings:

```
Added: HKCU\Software\Microsoft\Windows\CurrentVersion\Run\Keylogger
Modified: HKLM\SOFTWARE\Microsoft\Windows\CurrentVersion\Policies\System
```

- Process and Thread Activity: The keylogger might spawn new processes or inject code into existing ones to monitor keystrokes. Example findings:

```
Created: Process PID 5678 (keylogger.exe)
Injected: Thread into explorer.exe
```

- Log File Analysis: Locate the log file (e.g., keylog.txt) and examine its content. You may find captured keystrokes and possibly timestamps indicating when each keystroke was logged. Example findings:

```
[2024-05-17 10:15:00] Username: JohnDoe
[2024-05-17 10:15:05] Password: mypassword123
```
By completing this exercise, you will gain practical experience in analyzing keylogger behavior, understanding how they capture and store keystrokes, and identifying persistence mechanisms. This knowledge is crucial for detecting and mitigating keylogger infections effectively.


# Project 5: Network Traffic Analysis of a Trojan

## Introduction
A Trojan is a type of malware that often masquerades as legitimate software but performs malicious activities once executed. These activities frequently include communicating with a command-and-control (C2) server to receive instructions or exfiltrate data. Analyzing the network traffic generated by a Trojan can reveal its communication patterns and help identify malicious domains or IP addresses. In this project, you will analyze the network traffic of a Trojan to understand its communication mechanisms.

## Pre-requisites
- Basic understanding of malware and its types, particularly Trojans.
- Familiarity with networking concepts and protocols (e.g., TCP/IP, HTTP).
- Knowledge of network traffic analysis tools.

## Lab Set-up
1. Operating System: Use a Windows virtual machine (VM) created using VirtualBox or VMware.
2. Trojan Sample: Obtain a known and safe-to-analyze Trojan sample from a reputable source like MalwareBazaar.
3. Tools:
  - Wireshark: For capturing and analyzing network traffic.
  - Procmon (Process Monitor): For monitoring file system, registry, and process/thread activity.
  - FakeNet-NG: For simulating network services and capturing malware communication.
    
Ensure your VM is isolated from your main network and has a snapshot taken before analysis to easily revert to a clean state.

## Exercise: Capturing and Analyzing Network Traffic
Objective: Execute the Trojan sample in a controlled environment and use Wireshark to capture and analyze its network traffic to identify communication patterns, protocols used, and any malicious domains or IP addresses.

Step 1: Set Up the Environment:

- Ensure the VM is isolated from your main network.
- Install and configure the necessary tools: Wireshark, Procmon, and FakeNet-NG.
- Take a snapshot of the VM for easy restoration.
- Start FakeNet-NG to simulate network services and capture the Trojan's communication.

Step 2: Initial Preparation:

- Start Wireshark to begin capturing network traffic on the VM.
- Start Procmon to monitor system activity (optional for additional context).

Step 3: Execute the Trojan Sample:

- Execute the Trojan sample within the VM.
- Allow the Trojan to run for a sufficient period to observe its network activity.

Step 4: Stop Capturing:

- Stop Wireshark after capturing enough traffic.
- Save the captured traffic data for analysis.

Step 5: Analyze the Network Traffic:

- Filter and Inspect Traffic: Use Wireshark to filter the traffic related to the Trojan. Common filters include ip.addr == <Trojan IP> or tcp.port == <specific port>.
- Identify Protocols: Determine the protocols used by the Trojan (e.g., HTTP, HTTPS, DNS).
- Examine Communication Patterns: Look for repetitive patterns, such as regular pings to a C2 server or data exfiltration attempts.
- Identify Malicious Domains/IPs: Note any suspicious domains or IP addresses the Trojan tries to contact.

## Expected Solution/Output:

- Filtering Traffic: Apply a filter in Wireshark to isolate the Trojan's traffic. For example:

```
ip.addr == 192.168.56.101
```
This filter isolates traffic to and from the IP address of the VM running the Trojan.

- Identifying Protocols: Analyze the traffic and identify the protocols used by the Trojan. For example:

```
Protocol: HTTP
Destination: malicious-domain.com
URL: http://malicious-domain.com/command
```
This indicates the Trojan is using HTTP to communicate with a malicious domain.

- Examining Communication Patterns: Observe the communication patterns. You might see the Trojan regularly checking in with the C2 server. Example findings:

```
GET /status HTTP/1.1
Host: malicious-domain.com
```
This indicates the Trojan is sending periodic HTTP GET requests to check in with the C2 server.

- Identifying Malicious Domains/IPs: Note the domains or IPs contacted by the Trojan. Example findings:

```
IP Address: 203.0.113.45
Domain: c2.malicious-domain.com
```
This information can be used to block these domains/IPs and understand the extent of the Trojan's network activity.

By completing this exercise, you will gain practical experience in capturing and analyzing network traffic generated by a Trojan. This knowledge is essential for identifying and mitigating malicious communication channels used by malware.



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

