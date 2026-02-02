# BLOCK 1 – Linux Basics & File Handling
**Levels:** 0–7

## Overview
This block focuses on basic Linux navigation and file handling.  
It builds foundational command-line skills required to inspect files and directories in Linux systems safely.

---

## Level 0 → Level 1
### **Objective:** Read the content of a file located in the home directory.

### **Command Used:**
```bash
cat readme
```

### **Explanation:**
The cat command outputs the content of a file to standard output.

### **Security Concepts:**
File reading
Basic command-line interaction

### **Relevance to Cybersecurity:**
Reading configuration or log files is a common task during investigations.


## Level 2 → Level 3

### **Objective:** Read a hidden file.

### **Command Used:**
```bash
ls -a
cat .hidden
```

### **Explanation:**
Hidden files start with a dot (.) and are often excluded from default listings.

### **Security Concepts:**
Hidden files
System visibility

### **Relevance:**
Hidden files may store credentials or configuration data.


## Level 3 → Level 4

### Objective: Locate a file inside a directory structure.

### **Command Used:**
```bash
ls
cd inhere
ls
```

### **Security Concepts:**
Directory traversal
File discovery


## Level 4 → Level 5

### **Objective:** Identify a human-readable file among multiple files.

### **Command Used:**
```bash
file ./*
```

### **Explanation:**
The file command identifies file types based on content.

### **Security Concepts:**
File type identification

### **Relevance:**
Helps identify binaries, scripts, or readable data during forensic analysis.


## Level 5 → Level 6

### **Objective:** Locate a file based on size and readability.

### **Command Used:**
```bash
find. -type f -size 1033c
```

### **Security Concepts:**
File searching
Attribute-based filtering


## Level 6 → Level 7

### **Objective:** Locate a file owned by a specific user.

### **Command Used:**
```bash
find / -user bandit7 2>/dev/null
```

### **Security Concepts:**
File ownership
Error redirection

**Relevance:**
Ownership analysis is critical for detecting privilege misuse.
