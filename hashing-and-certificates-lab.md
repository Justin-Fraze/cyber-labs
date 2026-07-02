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
<img width="1165" height="136" alt="Screenshot 2026-07-02 065539" src="https://github.com/user-attachments/assets/a784aad2-3cc5-4dc5-b3e3-0e0541f0da31" />
*Hash string:* 0C1D83B606657572FD66123D22FFAD0D0C914E9056ECEFA9B63D780B4A2A1671

Next, I changed the file text to `Transfer $1001 to Alice` (just changing a 0 to a 1) and ran the hash command again.

### Modified File Hash:
<img width="1165" height="135" alt="image" src="https://github.com/user-attachments/assets/22c3891a-619a-45ae-8db6-82c70c6d374d" />
*New hash string:* BEEB0D654B620CAB561A26E2DFF956A6FC296B6EF0EBD0FAC715C94566F0C13E

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
