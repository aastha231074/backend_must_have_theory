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

## Stateless vs Stateful

### Stateless
A **stateless** system does not store any information about previous interactions.  
Each request is independent and contains all the data needed to process it.

**Key Points:**
- No memory of past requests (at application/server level)
- Easier to scale horizontally
- Simpler architecture
- Example: HTTP requests, REST APIs

**Note:**
You *can* use a **shared external store** (like Redis, DB, cache) to keep data accessible across servers.  
In that case, the **application remains stateless**, while the **state is managed externally**.

---

### Stateful
A **stateful** system retains information about previous interactions within the system itself.  
It remembers context between requests.

**Key Points:**
- Maintains session or state in the server
- Harder to scale (needs session affinity / sticky sessions)
- More complex to manage
- Example: In-memory sessions on a server

---

### Stateless with Shared State (Best Practice)
Instead of storing state inside the server:
- Use **shared storage** (Redis, DB, distributed cache)
- Any server can handle any request
- Enables true horizontal scaling

**Example:**
- User logs in → session stored in Redis  
- Next request → any server fetches session from Redis  

---

### Quick Comparison

| Feature        | Stateless (Pure)     | Stateless + Shared Store | Stateful (Server-side) |
|---------------|--------------------|-------------------------|------------------------|
| Memory        | No                 | External                | Internal               |
| Scalability   | High               | Very High               | Moderate/Low           |
| Complexity    | Low                | Medium                  | High                   |
| Example       | REST API           | API + Redis session     | In-memory session      |

---
# JWT (JSON Web Token)

A **JWT (JSON Web Token)** is a **compact, URL-safe token** used to securely transmit information between a client and a server.

It is commonly used for **authentication and authorization**.

---

## Structure of JWT

A JWT consists of **3 parts** separated by dots:

```
xxxx.yyyy.zzzz
```

---

### 1. Header

Contains metadata about the token:

- Algorithm used for signing (e.g., HS256, RS256)
- Token type (JWT)

**Example:**
```json
{
  "alg": "HS256",
  "typ": "JWT"
}
```

---

### 2. Payload (Data)

Contains the actual data (called **claims**):

- `user_id`
- `email`
- `role`
- `exp` (expiry time)

⚠️ Note: Payload is **not encrypted**, only encoded → anyone can decode it.

**Example:**
```json
{
  "user_id": 123,
  "role": "admin",
  "exp": 1710000000
}
```

---

### 3. Signature

Used to **verify integrity** of the token.

**Formula:**
```
signature = HMACSHA256(
    base64urlencode(header) + "." +
    base64urlencode(payload),
    secret_key
)
```

---

## Important Clarifications

### URL-safe means:
- Uses Base64URL encoding
- Avoids characters like `+`, `/`, `=`
- Safe to send in URLs, headers, cookies

---

## How JWT Works (Flow)

1. User logs in → sends id/password  
2. Server verifies credentials  
3. Server creates JWT using **secret key**  
4. Client stores JWT (cookie/localStorage)  
5. Client sends JWT in every request  
6. Server verifies signature → allows access  

---

## Key Insights

- Server **does NOT store session**
- JWT is **stateless authentication**
- Signature ensures:
  - Data is not tampered
  - Token is valid

---

## Common Mistakes

- ❌ `"role": admin` → invalid JSON  
- ✅ `"role": "admin"`

- ❌ JWT is encrypted  
- ✅ JWT is **encoded + signed**, not encrypted

---

## Secret Key vs Public Key

- **HS256 (HMAC)** → same secret key for sign & verify  
- **RS256 (RSA)** → private key signs, public key verifies  


