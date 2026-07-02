# Lab: Verifying File Integrity with Hashing & Creating Digital Certificates

## 1. Objective
The goal of this lab is to demonstrate how hashing detects unauthorized changes to data (file integrity) and to simulate how digital certificates are generated to secure network communications.

## 2. Tools Used
* Windows PowerShell (or macOS Terminal)
* OpenSSL (Built into Mac/Linux, or easily installed on Windows)

## 3. Part 1: The "Avalanche Effect" in Hashing
For this step, I created a file named `top_secret.txt` containing the text: `Transfer $1000 to Alice`.

I ran a command to calculate its **SHA-256 hash** (digital fingerprint). 

### Original File Hash:
[INSERT SCREENSHOT OF YOUR TERMINAL HASH HERE]
*Hash string:* 2cf24dba5fb0a30e26e83b2ac5b9e29e1b161e5c1fa7425e73043362938b9824 (example)

Next, I changed the file text to `Transfer $1001 to Alice` (just changing a 0 to a 1) and ran the hash command again.

### Modified File Hash:
[INSERT SCREENSHOT OF YOUR NEW HASH HERE]
*New hash string:* a486510d... (example)

### My Takeaway:
Even though I only changed a single number, the resulting hash was completely different. This is called the **Avalanche Effect**. In the real world, this is how security analysts know if a piece of software has been altered by a hacker or infected with malware.

---

## 4. Part 2: Generating a Self-Signed Certificate
To understand how websites secure connections using SSL/TLS, I used OpenSSL to generate a private key and a self-signed digital certificate.

I ran the following command:
`openssl req -x509 -sha256 -nodes -days 365 -newkey rsa:2048 -keyout myPrivateKey.key -out myCertificate.crt`

### Terminal Output & Generated Files:
[INSERT SCREENSHOT OF OPENSSL ASKING FOR YOUR NAME/COUNTRY AND THE CREATED FILES]

### My Takeaway:
This process generated two files: a **Private Key** (which must be kept strictly secret to decrypt traffic) and a **Public Certificate** (which is shared with the world so they can encrypt data sent to me). This is the foundation of public-key cryptography that keeps the internet secure.
