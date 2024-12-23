# Cyber Security Fundamentals

# SSL/TLS 

TLS 1.2 Flow Diagram And Explained - https://www.youtube.com/watch?v=j9QmMEWmcfo

![image](https://github.com/user-attachments/assets/0fbf8acc-0343-4445-8bed-01fbbda35c34)

## TLS Handshakes

TLS handshakes are a series of datagrams or messages exchanged between a client and a server. They involve multiple steps, allowing both parties to exchange the necessary information to complete the handshake and enable secure communication.

The exact steps within a TLS handshake depend on the key exchange algorithm and cipher suites supported. Below are descriptions of the TLS handshake processes for two common methods: RSA and Diffie-Hellman.

---

## **RSA TLS Handshake**
The RSA key exchange algorithm (deprecated in TLS 1.3) involves the following steps:

1. **Client Hello**:
   - The client sends a "hello" message to the server, initiating the handshake.
   - This message includes:
     - Supported TLS version.
     - Supported cipher suites.
     - A random string of bytes called the **"client random"**.

2. **Server Hello**:
   - The server responds with:
     - The server's SSL certificate.
     - The chosen cipher suite.
     - A random string of bytes called the **"server random"**.

3. **Authentication**:
   - The client verifies the server's SSL certificate with the certificate authority (CA) that issued it.
   - This confirms the server's identity.

4. **Premaster Secret**:
   - The client generates a random string of bytes called the **"premaster secret"**.
   - The premaster secret is encrypted using the server's **public key** (from its SSL certificate) and sent to the server.

5. **Private Key Decryption**:
   - The server decrypts the premaster secret using its **private key**.

6. **Session Key Generation**:
   - Both the client and server generate session keys using:
     - Client random.
     - Server random.
     - Premaster secret.
   - The resulting session keys should match on both sides.

7. **Client is Ready**:
   - The client sends a "finished" message encrypted with a session key.

8. **Server is Ready**:
   - The server responds with a "finished" message encrypted with a session key.

9. **Secure Communication**:
   - The handshake is completed, and further communication uses **symmetric encryption** via session keys.

---

## **Ephemeral Diffie-Hellman (DH) TLS Handshake**
The Diffie-Hellman key exchange uses exponential calculations for key generation and avoids transmitting a premaster secret. Steps include:

1. **Client Hello**:
   - The client sends a message with:
     - Supported protocol version.
     - **Client random**.
     - Supported cipher suites.

2. **Server Hello**:
   - The server responds with:
     - SSL certificate.
     - Selected cipher suite.
     - **Server random**.
     - A digital signature of all previous handshake messages.

3. **Server's Digital Signature**:
   - The server computes and includes a **digital signature** of all handshake messages so far.

4. **Digital Signature Verification**:
   - The client verifies the server's digital signature to confirm its authenticity.

5. **Client DH Parameter**:
   - The client sends its **DH parameter** to the server.

6. **Premaster Secret Calculation**:
   - Both client and server use their exchanged DH parameters to independently calculate a matching **premaster secret**.

7. **Session Key Generation**:
   - Both client and server generate session keys using:
     - Client random.
     - Server random.
     - Premaster secret.

8. **Client is Ready**:
   - The client sends a "finished" message encrypted with a session key.

9. **Server is Ready**:
   - The server responds with a "finished" message encrypted with a session key.

10. **Secure Communication**:
    - The handshake is completed, and communication continues using **symmetric encryption**.

---

## Key Terms
- **DH Parameter**: In Diffie-Hellman, each side provides a parameter used in exponential calculations to generate a shared premaster secret.
- **Premaster Secret**: A random value used to derive session keys.
- **Session Keys**: Symmetric encryption keys used after the handshake for secure communication.

TLS handshakes rely on **asymmetric cryptography** for key exchange and **symmetric encryption** for ongoing communication.






# Networking Basics
Understand the basics of networking : https://www.youtube.com/watch?v=_IOZ8_cPgu8

## Key Networking Components and Concepts

### 1. Local Area Network (LAN)
- A network setup within a limited area, such as a home or school.
- Devices like laptops, printers, and mobile phones communicate within this network.
- **Example:** In a school, students represent devices, each with a unique identifier (like an IP address).

### 2. Wide Area Network (WAN)
- Connects multiple LANs across broader areas, such as cities or countries.
- **Example:** Communicating with a different school or accessing the internet involves WAN.

### 3. Router
- Acts as a gateway connecting a local network to external networks like the internet.
- Manages data traffic between devices and external networks.

### 4. Gateway
- A node that serves as an entry or exit point to another network.
- Ensures secure communication and handles network translation.

### 5. Subnet
- Divides a larger network into smaller, manageable sections.
- Helps organize and isolate network traffic within a LAN.

How To Identify Subnet Ranges?

![image](https://github.com/user-attachments/assets/f9fee2b9-d195-4546-b59b-5ba049bec985)




### 6. Firewall
- Provides security by filtering traffic between internal and external networks.
- Prevents unauthorized access to internal systems.

### 7. DMZ (Demilitarized Zone)
- A separate subnetwork exposing services to an external network while keeping internal networks secure.
- **Example:** A school reception area that visitors must pass through before accessing inner sections.

### 8. Port Forwarding
- Allows specific traffic from external networks to reach designated devices in a LAN.
- **Example:** Forwarding traffic to a web server hosted within a home network.

### 9. Network Address Translation (NAT)
- Masks internal device IPs when accessing the internet by using the router’s external IP.
- Enhances security and conserves IP addresses.

### 10. IP Addressing
- Logical identifiers for devices in a network.
- **Example:** Devices in a LAN communicate using unique IP addresses within a defined range (e.g., 192.168.x.x).

---

## Key Analogies and Examples

- **LAN vs. WAN:**
  - LAN is like students interacting within the same class, while WAN is like students communicating with other schools.

- **DMZ:**
  - Acts as a reception desk in a school; visitors must clear it before entering secure areas.

- **Port Forwarding:**
  - Similar to granting specific permissions to visitors to meet someone in a secure section of a school.

---

## Advanced Features
- **Firewalls** and **Port Forwarding** enable controlled communication between internal and external networks.
- **Routers** and **NAT** ensure efficient and secure device communication across different network layers.

## Forward Proxy, Reverse Proxy and Load Balancing

Basics: https://www.youtube.com/watch?v=xo5V9g9joFs


# SOC / Threat Hunting

Good For Understanding The Terms And How The Dots Can Be Connected  - https://www.youtube.com/watch?v=VNp35Uw_bSM
Good For Understanding The Process - https://www.youtube.com/watch?v=NdwTeSi70SU

## Threat Hunting: Key Notes and Strategy

- **Threat hunting** involves proactively searching for anomalies or indicators of compromise in a system.
- It is a **technical process** requiring knowledge of attacker behavior and system baselines.
- **Common challenges** include:
  1. Complexity of the domain.
  2. Lack of actionable and pragmatic advice online.
  3. Vendor-driven resources that double as advertisements.
  4. Difficulty in choosing the right starting point.

---

## **Step 1: Learn Attacker TTPs**
- **TTPs**: Tactics, Techniques, and Procedures.
  - **Tactics**: High-level goals of attackers.
  - **Techniques**: General methods to achieve those goals.
  - **Procedures**: Step-by-step execution of an attack.
- Use resources like the **MITRE ATT&CK framework** to familiarize yourself with common TTPs.
  - **Focus on these key categories**:
    - **Execution**
    - **Persistence**
    - **Privilege Escalation**
    - **Lateral Movement**
  - These categories are easier to detect via telemetry and log analysis.

---

## **Step 2: Establish a Baseline**
- **Understand what is normal**:
  - Review logs regularly to identify typical patterns.
  - Know the behavior of admins and applications on your servers.
  - **Ask operational questions**:
    - How often are servers accessed?
    - Is **sudo** configured correctly?
    - Is there monitoring in place?
    - How often are patches applied?
  - This baseline helps in spotting anomalies.

---

## **Step 3: Start the Hunt**
- **Use security tools wisely**:
  - Examples: SIEM, SOAR, EDR, or XDR.
  - Tools are helpful but rely on human configuration and oversight.
- **Confirm your setup**:
  - Verify that logs are generated as expected.
  - Ensure that security tools are collecting and shipping logs for analysis.
- **Investigate directly**:
  - Access systems and explore manually or with scripts.
  - **Search logs for suspicious activity**, such as:
    - Powershell execution at odd hours.
    - Activity under unauthorized accounts.

---

## **Additional Resources**
- Use recent **attacker behavior reports** to guide your focus:
  - Examples:
    - **CrowdStrike OverWatch Report**
    - **Verizon Data Breach Report**
  - **Common indicators** include:
    - Abuse of valid accounts.
    - Unusual use of command and scripting interpreters.

---

## **Key Takeaways**
- **Three steps for threat hunting**:
  1. Learn attacker TTPs relevant to your environment.
  2. Establish a baseline of normal activity.
  3. Explore system telemetry, logs, and security tools to find anomalies.
- **Proactive mindset**:
  - Don’t rely solely on tools.
  - Always verify your assumptions and data collection methods.

---
## Log Analysis

## Quick Tips for EDR Analysis  

1. **Search Efficiently with IOCs**  
   Use Indicators of Compromise (IOCs) like file hashes, IP addresses, or process names to search across all endpoints. This can quickly identify affected devices and determine the scope of the attack.  

2. **Leverage Containment Features**  
   Isolate compromised devices immediately to prevent lateral movement. Ensure the device communicates only with the EDR center for ongoing analysis without further network risk.  

3. **Analyze Browser History**  
   Check browser history on the device to identify any suspicious activity or malicious downloads that could indicate the entry point of an attack.  

4. **Monitor Network Connections**  
   Review active and historical network connections to detect unauthorized access or command-and-control communication.  

5. **Investigate Process Lists**  
   Identify unusual processes or applications running on the device. Pay attention to processes that mimic legitimate ones but have unexpected behaviors.  

6. **Utilize Live Investigation**  
   Connect to the endpoint in real time to gather additional evidence, capture memory dumps, or run specific forensic tools for deeper analysis.  

7. **Automate Repetitive Tasks**  
   Use automated playbooks in your EDR tool for common tasks like hash lookups, file quarantines, and IOC scanning to save time.  

8. **Prioritize Alerts**  
   Focus on high-severity alerts and events flagged by your EDR solution. These often indicate critical threats requiring immediate action.  

9. **Document Everything**  
   Maintain a log of your EDR analysis steps, findings, and containment actions. This aids in incident reporting and knowledge sharing.  

10. **Practice Regularly**  
    Simulate incident scenarios to familiarize yourself with the EDR tool's interface and features, ensuring quick and efficient responses during actual events.  



## Common Mistakes Made by SOC Analysts  

## 1. **Over-reliance on VirusTotal Results**  
- VirusTotal is a **supporting tool** and should not be solely relied upon for analysis.  
- New malicious software using AV bypass techniques may not be detected by VirusTotal.  
- Always perform additional analysis beyond VirusTotal results.  

**Key Tip**: Treat VirusTotal as a starting point, not the final answer.  

---

## 2. **Hasty Analysis of Malware in a Sandbox**  
- Short analysis times (3-4 minutes) in sandboxes can lead to inaccurate results.  
  - Malware may detect the sandbox environment and remain inactive.  
  - Some malware takes 10-15 minutes (or longer) to activate.  
- **Recommendation**:  
  - Conduct extended analysis in sandboxes.  
  - Use real environments for better accuracy, if feasible.  

---

## 3. **Inadequate Log Analysis**  
- Failing to properly analyze logs can result in missed connections or threats.  
- Example:  
  - Malware detected on a device ("Jev") secretly sends data to "jev.io".  
  - SOC analysts must use log management tools to check if other devices are also connecting to this address.  

**Key Tip**: Always correlate logs across devices for a comprehensive view.  

---

## 4. **Overlooking VirusTotal Dates**  
- Cached results on VirusTotal may not reflect the current state of a URL or file.  
- Example:  
  - An attacker might query a clean URL, then replace it with malicious content later.  
- **Recommendation**:  
  - Do not rely solely on cached results.  
  - Perform a fresh search to ensure the latest data is analyzed.  

---


