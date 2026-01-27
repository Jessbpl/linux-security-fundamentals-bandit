# Block 3 – SSH, Processes & Privilege Boundaries


## Overview
This block introduces advanced SSH usage and interaction with remote services.
It focuses on understanding how credentials, ports, and services are exposed
and accessed in real systems.

---

## Level 16 → Level 17

### Objective
Retrieve the password for the next level by identifying the correct service
listening on localhost and authenticating using an SSH private key.

---

### Context
At this level, multiple services are running on different ports on `localhost`. Only one of them accepts SSH connections using the provided private key. The challenge is to identify the correct port and use SSH key-based authentication
to obtain the password.

---

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

### Security Concepts

Port scanning and service discovery
SSH key-based authentication
Non-standard SSH ports
Access control via cryptographic keys

###Relevance to Cybersecurity

Understanding how to identify exposed services and authenticate securely is
fundamental in cybersecurity. This level mirrors real-world scenarios such as:

Discovering misconfigured or exposed services
Using SSH keys instead of passwords for secure access
Assessing attack surfaces during reconnaissance
Investigating systems during incident response
