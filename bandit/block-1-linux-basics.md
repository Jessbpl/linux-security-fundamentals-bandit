# BLOCK 1 – Linux Basics & File Handling
**Levels:** 0–7

## Overview
This block focuses on foundational Linux navigation and file-handling skills. It builds essential command-line knowledge required to inspect files,  directories, and system structures safely in Linux.

---

## Level 0 → Level 1

### Objective: 
Read the content of a file located in the home directory.

### Context
The user starts in their home directory and is given a file containing the password for the next level.

### Commands Used:
```bash
cat readme
```

### Explanation:
The **cat** command outputs the content of a file directly to standard output, allowing the user to read its data.

### Security Concepts:
File reading
Basic command-line interaction

### Relevance to Cybersecurity:
Reading configuration files, logs, or sensitive text files is a common task during investigations and system audits.


## Level 2 → Level 3

### Objective:
Read a hidden file.

### Context
The target file is hidden and does not appear in a standard directory listing.

### Commands Used:
```bash
ls -a
cat .hidden
```

### Explanation:
Hidden files start with a dot (.) and are excluded from normal **ls** output unless the **-a** flag is used.

### Security Concepts:
Hidden files
System visibility

### Relevance:
Hidden files may store credentials, configuration data, or malicious artifacts intended to avoid detection.


## Level 3 → Level 4

### Objective: 
Locate a file inside a directory structure.

### Context:
The password file is stored inside a subdirectory rather than the current working directory.

### Command Used:
```bash
ls
cd inhere
ls
```
### Explanation
Directory listing and navigation commands are used to explore the filesystem and locate files.

### **Security Concepts:**
Directory traversal
File discovery

### Relevance to Cybersecurity
Understanding directory structures is essential when analyzing compromised systems or searching for suspicious files.


## Level 4 → Level 5

### Objective:
Identify a human-readable file among multiple files.

### Context:
The directory contains many files, but only one contains readable text.

### **Command Used:**
```bash
file ./*
```

### Explanation:
The **file** command identifies file types by analyzing their content rather than relying on filenames or extensions.

### Security Concepts:
File type identification

### Relevance:
Helps distinguish between binaries, scripts, and readable data during forensic analysis.


## Level 5 → Level 6

### Objective:
Locate a file based on size and readability.

### Context:
The password file has specific attributes that must be matched to identify it. 

### Command Used:
```bash
find. -type f -size 1033c
```

### Explanation:
The **find** command searches for files based on attributes such as type and size.

### Security Concepts:
File searching
Attribute-based filtering


## Level 6 → Level 7

### Objective:
Locate a file owned by a specific user.

### Command Used:
```bash
find / -user bandit7 2>/dev/null
```

### Explanation:
The **find** command searches the entire filesystem while redirecting permission errors to **/dev/null**.

### **Security Concepts:**
File ownership
Error redirection

### Relevance to Cybersecurity:
Ownership analysis helps detect privilege misuse, unauthorized file creation, and lateral movement.
