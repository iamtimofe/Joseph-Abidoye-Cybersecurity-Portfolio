# 🔐 Encryption & Traffic Security Demonstration

> Practical demonstration of symmetric encryption, asymmetric encryption, and traffic analysis using OpenSSL and Wireshark.

---

## 🎯 Objective

To understand:

- How symmetric encryption works
- How asymmetric encryption works
- Why HTTP traffic is readable
- Why HTTPS traffic is encrypted and secure

---

# 1️⃣ Symmetric Encryption (AES-256-CBC)

## 🛠️ Tool Used
- OpenSSL (Kali Linux)

## 🔑 Key Generation

```bash
openssl rand -base64 32 > secret.key
```

Generated a 256-bit key stored in `secret.key`.

## 🔒 Encrypt File

```bash
openssl enc -aes-256-cbc -salt -in ssl.txt -out encrypted.bin -pass file:secret.key
```

## 🔓 Decrypt File

```bash
openssl enc -d -aes-256-cbc -salt -in encrypted.bin -out decrypted.txt -pass file:secret.key
```

## 📚 Observation

- Same key used for encryption and decryption.
- If key is compromised, data can be decrypted.
- Suitable for fast data encryption.

---

# 2️⃣ Asymmetric Encryption (RSA)

## 🛠️ Tool Used
- OpenSSL

## 🔑 Generate Public Key from Private Key

```bash
openssl rsa -in private.pem -pubout -out public.pem
```

## 🔒 Encrypt Using Public Key

```bash
openssl pkeyutl -encrypt -inkey public.pem -pubin -in Message.txt -out encrypted_Message.bin
```

## 🔓 Decrypt Using Private Key

```bash
openssl pkeyutl -decrypt -inkey private.pem -in encrypted_Message.bin
```

## 📚 Observation

- Public key encrypts.
- Private key decrypts.
- More secure for key exchange.
- Used in HTTPS (TLS).

---

# 3️⃣ Wireshark – HTTP Traffic Monitoring

## 📡 Captured Traffic

Filtered HTTP traffic:

```
http
```

Observed:

- GET requests
- Host headers
- User-Agent
- Response status (200 OK)
- Visible content

## 🚨 Security Observation

HTTP traffic is:

- Plaintext
- Fully readable
- Credentials and data visible
- Vulnerable to interception

---

# 4️⃣ Wireshark – HTTPS Traffic Monitoring

Filtered TCP stream:

```
tcp.stream eq X
```

Observed:

- TLS handshake
- Client Hello
- Server Hello
- Encrypted Application Data
- Unreadable payload

## 🔐 Security Observation

HTTPS traffic:

- Encrypted
- Content unreadable
- Uses asymmetric encryption for handshake
- Uses symmetric encryption for session data

---

# 🛡️ Key Security Takeaways

- Symmetric encryption is fast but requires secure key sharing.
- Asymmetric encryption secures key exchange.
- HTTP is insecure and readable.
- HTTPS protects confidentiality and integrity.
- Wireshark can inspect metadata but not decrypt HTTPS without keys.

---

# 🎓 Learning Outcome

This lab strengthened understanding of:

- Cryptographic fundamentals
- Encryption mechanisms
- Secure communication protocols
- Traffic visibility and monitoring
- Why TLS is essential in modern networks
