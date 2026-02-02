# BLOCK 2 – Permissions, Redirections & File Searching

**Levels:** 8–15

## Overview
This block focuses on permissions, redirections, and advanced file searching techniques.

---

## Level 7 → Level 8
###**Objective:** Extract data from a file with repeated lines.

### **Command Used:**
```bash
sort data.txt | uniq -u
```

### **Security Concepts:**
Data processing
Log analysis


## **Level 8 → Level 9**

### **Objective:** Find a file by owner, group, and size.

### **Command Used:**
```bash
find / -type f -user bandit7 -group bandit6 -size 33c 2>/dev/null
```

### **Security Concepts:**
File ownership
Permission handling
Error redirection


## **Level 9 → Level 10**

### **Objective:** Extract readable strings from a binary file.

### **Command Used:**
```bash
strings data.txt
```

### **Security Concepts:**
Binary inspection
Data leakage

## **Level 10 → Level 11**

### **Objective:** Decode base64-encoded data.

### **Command Used:**
```bash
base64 -d data.txt
```

### **Security Concepts:**
Encoding vs encryption


## **Level 11 → Level 12**

### **Objective:** Decrypt ROT13-encoded text.

### **Command Used:**
```bash
cat data.txt | tr 'A-Za-z' 'N-ZA-Mn-za-m'
```

### **Security Concepts:**
Simple ciphers
Obfuscation

## **Level 12 → Level 13**

### **Objective:** Extract and decompress a file multiple times.

### **Commands Used:**
```bash
xxd -r data.txt > data.bin
file data.bin
```

### **Security Concepts:**
File extraction
Compression formats


## **Level 13 → Level 14**

### **Objective:** Use SSH keys for authentication.

### **Command Used:**
``bash
ssh -i sshkey.private bandit14@localhost
``

### **Security Concepts:**
SSH authentication
Key-based access


## **Level 14 → Level 15**

### **Objective:** Communicate with a service using a specific port.

### **Command Used:**
```bash
nc localhost 30000
```

### **Security Concepts:**
Networking basics
Service interaction


---

