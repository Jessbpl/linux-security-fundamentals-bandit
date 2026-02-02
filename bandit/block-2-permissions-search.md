# BLOCK 2 – Permissions, Redirections & File Searching
**Levels:** 7–15

## Overview
This block focuses on file permissions, ownership, and advanced file searching, and data extraction techniques. It develops skills required to locate sensitive information while handling permission boundaries and noisy system output.

---

## Level 7 → Level 8

### Objective:
Locate a file containing the password by filtering contents.

### Context:
The password is stored somewhere in the system but not directly visible. The task requires searching through files to find a specific pattern. 

### Commands Used:
```bash
sort data.txt | uniq -u
```
### Explanation
The file is sorted to bring duplicate lines together **uniq -u** then outputs only lines that occur once, helping to isolate the unique password in the file. 

### **Security Concepts:**
Data deduplication
Pattern filtering
Log analysis

### Relevance to Cybersecurity:
Filtering out repeated or redundant data is crucial when scanning logs, extracting IOCs, or finding hidden credentials.


## Level 8 → Level 9

### Objective:
Locate a file with specific ownership and size attributes. 

### Context:
The password file is not located in the home directory. It must be identified by filtering files across the system based on ownership, group, and file size while suppressing permission errors. 

### Command Used:
```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```
## Explanation:
The **find** command searches the entire filesystem for regular files owned by user **bandit7**, and exactly 33 bytes in size. Error messages are redirected to **/dev/null** to avoid permission-denied noise. 

### Security Concepts:
File ownership
Permission handling
Error redirection

### Relevance to Cybersecurity:
Filtering files by ownership and attributes is essential during forensic analysis and privilege misuse investigation.


## Level 9 → Level 10

### Objective:
Extract readable strings from a binary file.

## Context:
The password is stored inside a file containing non-printable or binary data that cannot be read directly using standard text commands.

### Commands Used:
```bash
strings data.txt
```

### Explanation:
The **strings** command scans the file and outputs sequences of printable characters, revealing embedded readable data.

### Security Concepts:
Binary inspection
Data leakage

## Relevance to Cybersecurity
Security analysis frequently extracts readable artifacts from binaries, memory dumps, or malware samples.


## Level 10 → Level 11

### Objective:
Decode base64-encoded data.

### Command Used:
```bash
base64 -d data.txt
```
### Explanation: 
The **base64 -d** command decodes Base64-encoded content back into its original readable form.

### Security Concepts:
Encoding vs encryption

### Relevance to Cybersecurity
Attackers often use encoding to obscure data. Analysts must recognize and reverse these transformations.


## Level 11 → Level 12

### Objective:
Decrypt ROT13-encoded text.

### Context:
The password is obfuscated using a simple substitution cypher rather than real encryption. 

### Commands Used:
```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

### Explanation:
The **tr** command replaces each character with its ROT13 counterpart, reversing the obfuscation. 

### Security Concepts:
Simple ciphers
Obfuscation

### Relevance to Cybersecurity
Understanding weak or legacy obfuscation techniques is important when analyzing malware or poorly secured systems. 


## Level 12 → Level 13

### Objective: 
Extract and decompress a file multiple times.

### Context:
The password is hidden inside a file that has undergone several transformations, starting as a hex dump.

### Commands Used:
```bash
xxd -r data.txt > data.bin
file data.bin
```

### Explanation:
The hex dump is reversed back into binary format. The **file** command is then used to identify the file type so the correct extraction method can be applied. 

### **Security Concepts:**
File extraction
Compression formats

### Relevance to Cybersecurity:
Layered compression and transformation are common techniques used to hide malicious payloads or exfiltrated data. 


## Level 13 → Level 14

### Objective:
Authenticate using a SSH private key.

### Context:
Password-based authentication is disabled, requiring key-based access. 

### Command Used:
```bash
ssh -i sshkey.private bandit14@localhost
```

### Explanation:
The SSH client uses the provided private key to authenticate securely without transmitting a password.

### Security Concepts:
SSH authentication
Key-based access

### Relevance to Cybersecurity:
Key-based authentication is a standard security practice in cloud and production. 


## Level 14 → Level 15

### Objective:
Communicate with a service using a specific port.

### Context:
The password must be sent to a service listening on a local port in order to receive the next credential. 

### Command Used:
```bash
nc localhost 30000
```

### Explanation: 
The **nc** (netcat) command establishes a connection to the service and sends input, receiving a response.

### Security Concepts:
Networking basics
Service interaction

### Relevance to Cybersecurity:
Understanding how services communicate over ports is fundamental for penetration testing and incident response. 

---

