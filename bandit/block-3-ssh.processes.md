# Block-3 – SSH, Processes & Privilege Boundaries 
Levels: 16–24

## Overview
This block focuses on advanced SSH usage, process inspection, and accessing privilege boundaries.
It teaches techniques to enumerate services, inspect processes, use key-based authentication, and escalate privileges within Linux systems.

---

## Level 16 → Level 17

### Objective
Retrieve the password for the next level by identifying the correct service
listening on localhost and authenticating using an SSH private key.

### Context
At this level, multiple services are running on different ports on `localhost`. Only one of them accepts SSH connections using the provided private key. The challenge is to identify the correct port and use SSH key-based authentication to obtain the password.

### Commands Used
```bash
#Scan for open ports in the target range
nmap -p 31000-32000 localhost
# Connect to the correct port using the private key
ssh -i sshkey16.private bandit17@localhost -p <PORT>
```

### Explanation
1. nmap is used to scan a specific range of ports on localhost to discover which services are running and which ports are open.
2. The scan reveals a service that allows SSH connections.
SSH is then used with:
     -i to specify the private key file
     -p to connect to the correct non-standard port
3. Once authenticated, access to the system is granted and the password for the next level is displayed.

### Security Concepts
Port scanning and service discovery
SSH key-based authentication
Non-standard SSH ports
Access control via cryptographic keys

### Relevance to Cybersecurity
Understanding how to identify exposed services and authenticate securely is
fundamental in cybersecurity. This level mirrors real-world scenarios such as:

Discovering misconfigured or exposed services
Using SSH keys instead of passwords for secure access
Assessing attack surfaces during reconnaissance
Investigating systems during incident response



## Level 17 → Level 18

### Objective
Retrieve the password for the next level by identifying the difference between two nearly identical files.

### Context
Two files are provided, passwords.old and passwords.new, which contain multiple lines of text. Only one line differs between them, and that difference contains the password for the next level.

### Commands Used
```bash
#compare both files line by line
diff passwords.old passwords.new
```

### Explanation
The comparison revealed a single modified line. The updatd value in passwords.new contained the password required to access the next level.

## Relevance to Cybersecurity
File comparison is a fundamental technique in security for detecting unauthorized changes, auditing configuration files, and analyzing log differences during incident investigations.



## Level 18 → Level 19

### Objective
Obtain the password by connecting to a service running on a local network port.

## Context
The password for the next level is exposed through a service listening on local.host. The challenge is to connect directly to the service and read its output.

### Commands Used
```bash
#Connect to the local host service on the specific port
nc localhost <PORT>
```

### Explanation
Upon connecting to the service, the password for the next level was displayed directly in the service output.

### Relevance to Cybersecurity
This level demonstrates how sensitive information can be leaked through misconfigured or unsecured services. Exposed services should always be reviewed and protected with propper authentication and access controls.



## Level 19 → Level 20

### Objective
Use a privileged executable to access a protected password file.

### Context
A binary file is provided with elevated prmissions (SetUID). when executed, it runs with the privileges of its owner and is capable of accessing restricted files.

### Commands Used
```bash
#Execute the privileged binary
./bandit20-do
```

### Explanation
The executable accessed a protected file and revelaed the password for the next level.

### Relevance to Cybersecurity
SetUID binaries are powerful and potentialy dangerous. If misconfigured, they can lead to privilege escalation vulnerabilities. This level highlights the importance of controlling and auditing privileged executables.



## Level 20 → Level 21

### Objective:
Retrieve the password by interacting with a service running on a specific port.

### Context:
A service is listening on a local port and expects the current password as input in order to return the password for the next level.

### Commands Used:
```bash
cat /etc/bandit_pass/bandit20 | nc localhost 30000
```

### Explanation:
The current password is read from the system file and piped into nc (netcat), which sends the data to the service listening on port 30000 and returns the next password.

### Security Concepts:
Service interaction
Local network communication

### Relevance to Cybersecurity:
Understanding how services accept input over network ports is essential for penetration testing and incident response.



## Level 21 → Level 22

### Objective:
Retrieve the password stored in a scheduled task configuration.

### Context:
A cron job runs periodically under a different user account. The password is embedded in a script executed by the scheduler.

### Commands Used:
```bash
ls -l /etc/cron.d
cat /etc/cron.d/cronjob_bandit22
cat /usr/bin/cronjob_bandit22.sh
```

### Explanation:
The cron configuration file reveals which script is executed automatically. Inspecting the script exposes the password being written or referenced.

### Security Concepts:
Scheduled tasks (cron jobs)
Script inspection

### Relevance to Cybersecurity:
Cron jobs are common persistence mechanisms. Inspecting them is a key step in system audits and malware analysis.



## Level 22 → Level 23

### Objective:
Retrieve a password that is dynamically generated and written to a file.

### Context:
A scheduled script creates a temporary file containing the password, which must be located and read.

### Commands Used:
```bash
ls -l /etc/cron.d
cat /etc/cron.d/cronjob_bandit23
cat /usr/bin/cronjob_bandit23.sh
ls /tmp
cat /tmp/<generated_file>
```

### Explanation:
By inspecting the cron job script, the location and naming pattern of the generated file can be identified. Reading the file reveals the password.

### Security Concepts:
Temporary files
Automated credential handling

### Relevance to Cybersecurity:
Insecure handling of temporary files can lead to credential leakage and privilege escalation.



## Level 23 → Level 24

### Objective:
Exploit a scheduled script to execute arbitrary commands and retrieve the password.

### Context:
A cron job executes a script from a writable directory. By modifying or injecting commands, it is possible to execute code with elevated privileges.

### Commands Used:
```bash
ls -l /etc/cron.d
cat /etc/cron.d/cronjob_bandit24
cat /usr/bin/cronjob_bandit24.sh
ls -l /var/spool/bandit24
```

### Explanation:
The cron job executes scripts placed in a specific directory. By understanding the execution flow, it is possible to inject a script that outputs the password.

### Security Concepts:
Privilege escalation
Insecure scheduled tasks
Writable execution paths

### Relevance to Cybersecurity:
Misconfigured cron jobs are a real-world privilege escalation vector and are frequently exploited during post-exploitation.
