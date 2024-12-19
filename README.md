# Security Fundamentals

## SSL/TLS 

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






## Networking Basics
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

