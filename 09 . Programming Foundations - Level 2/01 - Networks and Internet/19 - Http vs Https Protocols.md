---
DATE: 2025-09-05T19:23:00
DONE: true
Name: Foundation 2
---

## HTTP vs HTTPS Protocols

### HTTP: Hypertext Transfer Protocol

**HTTP** stands for **H**yper**T**ext **T**ransfer **P**rotocol. It is the fundamental protocol used to transfer data across the World Wide Web (WWW).

**What it does:**
- Sends requests from your browser to web servers
- Retrieves and transfers webpages, images, audio, video, and other files
- Displays web content on your screen

**Important note:** HTTP sends data in **plaintext**, meaning anyone intercepting the connection can see exactly what information is being transmitted.

---

### HTTPS: Hypertext Transfer Protocol Secure

**HTTPS** stands for **H**yper **T**ext **T**ransfer **P**rotocol **S**ecure. It is the encrypted, secure version of HTTP.

**What it adds to HTTP:**
- Encryption using **TLS** (Transport Layer Security) or **SSL** (Secure Sockets Layer)
- Data verification and digital signatures
- Protection against hackers and eavesdropping
- Authentication to confirm you're communicating with the real website

**The key difference:** HTTPS encrypts all your data, making it unreadable to anyone trying to intercept it.

---

## Quick Comparison Table

| Feature | HTTP | HTTPS |
|---------|------|-------|
| **Security** | Unencrypted (plaintext) | Encrypted (TLS/SSL) |
| **Port** | 80 | 443 |
| **URL Format** | `http://www.google.com` | `https://www.google.com` |
| **Hacker Visibility** | Data is visible | Data is encrypted |
| **Browser Warning** | None | Trusted icon/lock |
| **Use Case** | Non-sensitive content | Sensitive data (passwords, payments) |
| **Current Status** | Declining in use | Standard for all websites |

---

## Understanding SSL/TLS

### What's the Difference?

**SSL (Secure Sockets Layer)** was the original security protocol created by Netscape in the mid-1990s. It's now considered outdated and deprecated.

**TLS (Transport Layer Security)** is the modern, improved replacement for SSL. It's more secure, faster, and is the current standard for web security.

TLS is an updated, more secure version of SSL. We still often refer to security certificates as "SSL" because it's a more familiar term, but modern implementations use TLS.

### How It Works

HTTPS uses TLS (or SSL) to encrypt normal HTTP requests and responses, and to digitally sign those requests and responses. This means:

1. Your browser and the server establish a secure connection
2. All data transmitted between them is encrypted
3. Each message is digitally signed so it can't be tampered with
4. Even if someone intercepts the connection, they can't read the data

---

## Ports: Where Data Travels

Every internet connection uses a "port" - think of it like a specific channel or pathway for data.

**Port 80 (HTTP):** The default port for unencrypted HTTP connections. When you access a webpage through HTTP, the browser sends a GET request through port 80 to the server.

**Port 443 (HTTPS):** The standard port for encrypted HTTPS connections. Port 443 allows data transmission over a secured network and encrypts network data packets before data transmission.

---

## Why HTTPS Matters Today

According to recent data, HTTPS (encrypted protocol) now provides the majority of online traffic, making it the standard for web security.

**When you should use HTTPS:**
- Entering passwords or usernames
- Making online purchases
- Submitting personal information (address, phone number, etc.)
- Banking and financial transactions
- Any sensitive or private data

**Browser warnings:** Modern browsers now show a warning if you try to access a non-HTTPS website, especially when entering sensitive information.

---

## Real-World Examples

**Website URLs:**
- Insecure: `http://www.example.com`
- Secure: `https://www.example.com`

**Identifying HTTPS:**
- Look for a **lock icon** 🔒 in your browser's address bar
- The URL starts with `https://` instead of `http://`
- You might see "Secure" or a green indicator

---

## Key Takeaways

1. **HTTP** = Basic protocol for transferring web data (unencrypted)
2. **HTTPS** = HTTP with encryption and security added
3. **SSL/TLS** = The encryption technology that makes HTTPS secure (TLS is the modern standard)
4. **Port 80** = HTTP uses this port
5. **Port 443** = HTTPS uses this port
6. **Modern web** = HTTPS is now the standard; HTTP is rarely used for sensitive data

**Bottom line:** Always use HTTPS for any website that handles personal or financial information. It keeps your data safe from hackers and eavesdroppers.

---

