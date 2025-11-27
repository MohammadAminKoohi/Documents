
2024-09-18 18:52

Status:

Tags: #Network #Security #Layer4

# How TLS Works

### Overview
Transport Layer Security (TLS) is a cryptographic protocol that provides secure communication over a computer network. It is the successor to Secure Sockets Layer (SSL) and is widely used for securing web traffic (HTTPS), emails, and other communications. The primary goal of TLS is to ensure **privacy**, **data integrity**, and **authentication** between communicating applications.

---

### Key Concepts

#### Encryption
Encryption is a method of converting plaintext into ciphertext to prevent unauthorized access to the data. TLS employs two types of encryption:

1. **Symmetric Encryption**: Both the client and server use the same key for encryption and decryption.
   - Fast and efficient.
   - Example algorithms: AES, ChaCha20.

2. **Asymmetric Encryption**: The encryption and decryption are done using two different keys: a **public key** and a **private key**.
   - More secure but computationally expensive.
   - Example algorithms: RSA, ECDSA.

#### Public and Private Keys
TLS utilizes **asymmetric encryption** during the handshake process:
- **Public Key**: Can be distributed freely. Used to encrypt data that can only be decrypted by the corresponding private key.
- **Private Key**: Kept secret by the owner. Used to decrypt data encrypted with the public key and also to sign data, providing proof of identity.

---

### How TLS Works: Step-by-Step

#### 1. **TLS Handshake**

The TLS handshake is the initial process of establishing a secure connection between a client (e.g., web browser) and a server (e.g., web server). During this handshake, the client and server authenticate each other and agree on encryption algorithms and keys to secure the communication.

##### Steps:
1. **Client Hello**: The client sends a message to the server indicating:
   - The version of TLS it supports.
   - A list of supported cipher suites (encryption algorithms).
   - A random value (used later to generate keys).

2. **Server Hello**: The server responds with:
   - The TLS version and cipher suite it will use.
   - Its digital certificate containing its public key.
   - A random value from the server.

3. **Server Authentication and Pre-Master Secret**: The client verifies the server’s certificate using the Certificate Authority (CA). The client then:
   - Generates a **pre-master secret** (a random value) and encrypts it using the server’s public key.
   - Sends the encrypted pre-master secret to the server.

4. **Key Generation**: Both the client and server use the pre-master secret, along with the random values exchanged earlier, to generate the **session keys**. These keys are symmetric keys used for encrypting and decrypting the data during the session.

5. **Client Finished Message**: The client sends a "Finished" message encrypted with the session key, indicating that it is ready to start secure communication.

6. **Server Finished Message**: The server responds with its "Finished" message, encrypted with the session key.

At this point, the handshake is complete, and the client and server can begin secure communication.

---

#### 2. **Symmetric Encryption After the Handshake**

After the handshake, symmetric encryption is used for the rest of the session. Both parties now use the same **session key** for:
- **Encrypting** outgoing messages.
- **Decrypting** incoming messages.

Since symmetric encryption is computationally efficient, it allows fast secure communication once the keys are exchanged.

---

### Important Components of TLS

#### Digital Certificates
A digital certificate is used to prove the ownership of a public key. Certificates are issued by trusted Certificate Authorities (CA) and contain:
- The **public key** of the server.
- The **identity** of the certificate holder (e.g., a domain name).
- The **CA’s digital signature**, verifying the authenticity of the certificate.

#### Cipher Suites
A **cipher suite** is a combination of cryptographic algorithms that specify how TLS performs encryption, key exchange, message authentication, and integrity verification. A cipher suite typically consists of:
1. **Key Exchange Algorithm** (RSA, DH, ECDHE)
2. **Symmetric Encryption Algorithm** (AES, ChaCha20)
3. **Message Authentication Code (MAC) Algorithm** (HMAC with SHA-256, SHA-384)

Example: `ECDHE-RSA-AES256-GCM-SHA384`
- **ECDHE**: Elliptic Curve Diffie-Hellman Exchange (for key exchange).
- **RSA**: Used for server authentication and key exchange.
- **AES256-GCM**: AES encryption in Galois/Counter Mode with 256-bit key.
- **SHA384**: HMAC-SHA384 used for integrity verification.

#### Perfect Forward Secrecy (PFS)
PFS ensures that even if a long-term private key is compromised, past communications remain secure. This is done by generating **ephemeral session keys** for each session that are not derived from the private key directly.

- **Key Exchange Algorithms** like **ECDHE** and **DHE** provide forward secrecy because they generate new key pairs for each session.

---

### TLS Versions

TLS has undergone multiple revisions to address security vulnerabilities:

1. **TLS 1.0**: The first version, now deprecated due to vulnerabilities.
2. **TLS 1.1**: Improvements over 1.0 but still not widely recommended.
3. **TLS 1.2**: Introduced modern cipher suites like AES-GCM, and more secure hash algorithms.
4. **TLS 1.3**: The latest and most secure version. It removes outdated algorithms (like RSA key exchange) and simplifies the handshake process, improving security and performance.

---

### How TLS Ensures Security

1. **Confidentiality**: All messages exchanged between the client and server are encrypted, ensuring that no one can eavesdrop.
   
2. **Integrity**: Each message is hashed with a Message Authentication Code (MAC) to prevent tampering. If the message is altered, the MAC verification will fail.
   
3. **Authentication**: The server's identity is verified using its digital certificate. In mutual TLS, both client and server authenticate each other using certificates.

---

### Usage of TLS

#### 1. **HTTPS (Web Security)**:
   - TLS secures HTTP traffic between web browsers and servers. HTTPS (Hypertext Transfer Protocol Secure) is simply HTTP over TLS.
   - Common use case: protecting user credentials, financial information, and private data on the web.

#### 2. **Email (STARTTLS)**:
   - STARTTLS is a mechanism to secure email communication using TLS. It allows an email server to upgrade an existing insecure connection to a secure one.
   
#### 3. **VPN (Virtual Private Networks)**:
   - TLS can be used to secure VPN connections, protecting data traveling over public networks.
   
#### 4. **Secure File Transfer**:
   - Protocols like FTPS (File Transfer Protocol Secure) use TLS to secure file transfers.

---

### Common Attacks and TLS Mitigations

1. **Man-in-the-Middle (MITM) Attacks**:
   - TLS protects against MITM attacks by ensuring that the server’s identity is verified through certificates and that the communication is encrypted.

2. **Downgrade Attacks**:
   - In a downgrade attack, an attacker forces the client and server to use a lower, less secure version of TLS (e.g., TLS 1.0). Modern TLS versions implement mechanisms like **TLS_FALLBACK_SCSV** to prevent this.

3. **Certificate Spoofing**:
   - This happens when an attacker presents a fake certificate. TLS mitigates this with Certificate Authorities (CAs) and proper verification of the certificate chain.
