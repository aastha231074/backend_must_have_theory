# 🔐 Asymmetric vs Symmetric Encryption

## 🔑 1. Asymmetric Key Pair (Public + Private Key)

### 📌 Used for Encryption
- Jim wants to send a secret message to Pam  
- Jim encrypts the message using **Pam’s Public Key**  
- Only **Pam’s Private Key** can decrypt it  

👉 Ensures: **Confidentiality**

---

### ✍️ Used for Digital Signatures
- Pam wants to prove she sent the message  
- Pam creates signature using her **Private Key**  
- Jim verifies using **Pam’s Public Key**

👉 If verification succeeds:
- ✔️ **Authentication** → Message came from Pam  
- ✔️ **Integrity** → Message not altered  

---

## ⚠️ Limitations of Asymmetric Encryption
- ❌ Slow  
- ❌ High CPU usage  
- ❌ Not suitable for large/bulk data  

---

## 🔐 2. Symmetric Encryption

- Same key used for:
  - Encryption  
  - Decryption  

👉 Best for:
- ✅ Large data transfer  
- ✅ High performance  

---

## 🤔 Problem: How to share symmetric key securely?

- Pam generates a **random symmetric key**  
- Pam encrypts this key using **Jim’s Public Key**  
- Jim decrypts it using **his Private Key**  

---

## 🔀 3. Hybrid Encryption

👉 Real-world systems (HTTPS, APIs, etc.)

- Use **Asymmetric Encryption** → for **Key Exchange**  
- Use **Symmetric Encryption** → for **Bulk Data Transfer**  

✔️ Combines:
- Security + Speed  

---

## 🔐 4. Hashing (For Signatures)

- Converts message → fixed-size **digest (fingerprint)**  
- Properties:
  - Same input → same hash  
  - Small change → completely different hash  

---

## ✍️ Digital Signature Process

### 🔹 Sender (Pam)
1. Create **hash of message**  
2. Encrypt hash using **Private Key** → Signature  
3. Send:
   - Message + Signature  

---

### 🔹 Receiver (Jim)
1. Decrypt signature using **Pam’s Public Key** → Get hash1  
2. Hash the received message → Get hash2  
3. Compare:

👉 If `hash1 == hash2`:
- ✔️ Integrity verified  
- ✔️ Authentication verified  

---

## 🧠 Key Insight

- ❌ Private key does NOT encrypt entire message in signatures  
- ✔️ Only the **hash is signed** (efficient + secure)

---

## ⚡ Quick Summary Table

| Feature        | Asymmetric                | Symmetric              |
|---------------|--------------------------|------------------------|
| Keys          | Public + Private         | Single key             |
| Speed         | Slow                     | Fast                   |
| Use Case      | Key exchange, signatures | Bulk data encryption   |
| Security      | High                     | High (if key secure)   |

---

## 🚀 One-Liner

👉 **Asymmetric is used to securely exchange keys, symmetric is used to encrypt actual data.**

