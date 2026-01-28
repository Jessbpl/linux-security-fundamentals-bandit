# Block-3 – SSH, Processes & Privilege Boundaries 


## Overview
This block introduces advanced SSH usage and interaction with remote services.
It focuses on understanding how credentials, ports, and services are exposed
and accessed in real systems.

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

### Explanation
1. nmap is used to scan a specific range of ports on localhost to discover which services are running and which ports are open.
The scan reveals a service that allows SSH connections.
SSH is then used with:
     -i to specify the private key file
     -p to connect to the correct non-standard port
Once authenticated, access to the system is granted and the password for the next level is displayed.

## Security Concepts
Port scanning and service discovery
SSH key-based authentication
Non-standard SSH ports
Access control via cryptographic keys

## Relevance to Cybersecurity
Understanding how to identify exposed services and authenticate securely is
fundamental in cybersecurity. This level mirrors real-world scenarios such as:

Discovering misconfigured or exposed services
Using SSH keys instead of passwords for secure access
Assessing attack surfaces during reconnaissance
Investigating systems during incident response


## Level 17 → Level 18

## Objective
Retrieve the password for the next level by identifying the difference between two nearly identical files.

## Context
Two files are provided, passwords.old and passwords.new, which contain multiple lines of text. Only one line differs between them, and that difference contains the password for the next level.

## Commands Used
```bash
#compare both files line by line
diff passwords.old passwords.new

##Explanation
The comparison revealed a single modified line. The updatd value in passwords.new contained the password required to access the next level.

## Relevance to Cybersecurity
File comparison is a fundamental technique in security for detecting unauthorized changes, auditing configuration files, and analyzing log differences during incident investigations.


Level 18 → Level 19

## Objective
Obtain the password by connecting to a service running on a local network port.

## Context
The password for the next level is exposed through a service listening on local.host. The challenge is to connect directly to the service and read its output.

## Commands Used
```bash
#Connect to the local host service on the specific port
nc localhost <PORT>

## Explanation
Upon connecting to the service, the password for the next level was displayed directly in the service output.

## Relevance to Cybersecurity
This level demonstrates how sensitive information can be leaked through misconfigured or unsecured services. Exposed services should always be reviewed and protected with propper authentication and access controls.


Level 19 → Level 20

## Objective
Use a privileged executable to access a protected password file.

## Context
A binary file is provided with elevated prmissions (SetUID). when executed, it runs with the privileges of its owner and is capable of accessing restricted files.

## Commands Used
```bash
#Execute the privileged binary
./bandit20-do

## Explanation
The executable accessed a protected file and revelaed the password for the next level.

## Relevance to Cybersecurity
SetUID binaries are powerful and potentialy dangerous. If misconfigured, they can lead to privilege escalation vulnerabilities. This level highlights the importance of controlling and auditing privileged executables.
