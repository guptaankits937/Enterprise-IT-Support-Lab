# Linux User Management

## Overview

This lab demonstrates practical Linux user administration in an Ubuntu Server environment.

The scenario simulates an IT Operations request to create a new Linux user account for an employee, assign a password, verify the account, and confirm that the user's home directory was created successfully.

This lab is part of the **Enterprise IT Support Lab** portfolio.

---

## Ticket Information

**Ticket ID:** INC-0001  
**Department:** IT Operations  
**Priority:** Medium  
**Status:** Completed  

---

## Scenario

A new employee joined the company and required access to the Linux environment.

The IT Operations team received a request from Human Resources (HR) to:

- Create a new Linux user account.
- Create the user's home directory.
- Assign a password.
- Verify the account.
- Confirm successful configuration.

---

## Environment

- Ubuntu Server
- Linux Terminal
- Sudo Privileges
- Local User Management

---

## Tasks Completed

During this lab, I performed the following tasks:

1. Verified the currently logged-in user.
2. Checked UID, GID, and group information.
3. Verified the server hostname.
4. Created a new Linux user named `john`.
5. Created the user's home directory using the `-m` option.
6. Assigned a password to the new account.
7. Verified the user account using the `id` command.
8. Confirmed creation of the user's home directory.
9. Troubleshot an incorrect username entered during password configuration.
10. Documented the implementation and captured supporting evidence.

---

## Key Commands

```bash
whoami
```

```bash
id
```

```bash
hostname
```

```bash
sudo useradd -m john
```

```bash
sudo passwd john
```

```bash
id john
```

```bash
ls /home
```

---

## Verification

The following checks confirmed that the task was completed successfully:

- The `john` user account was created.
- A password was successfully assigned.
- UID and GID information was verified.
- The user's home directory was created.
- The account was successfully validated using Linux administration commands.

---

## Troubleshooting

During password configuration, an incorrect username was entered:

```bash
sudo passwd joh
```

The system returned:

```text
passwd: user 'joh' does not exist
```

The username was corrected:

```bash
sudo passwd john
```

The password was then updated successfully.

This provided a simple example of identifying and correcting an administrative command error.

---

## Evidence

Screenshots captured during the practical lab include:

- `01-whoami.png`
- `02-id-command.png`
- `03-password-updated.png`
- `04-id-john.png`
- `05-home-directories.png`

Supporting screenshots are available in the [`Screenshots`](./Screenshots/) directory.

---

## Detailed Documentation

Complete technical documentation, including command explanations, verification results, troubleshooting, and lessons learned, is available here:

[`Linux-User-Management.md`](./Documentation/Linux-User-Management.md)

---

## Skills Demonstrated

- Linux User Administration
- User Account Management
- Password Management
- Linux Command-Line Administration
- User Verification
- Basic Troubleshooting
- System Administration
- Incident/Ticket Documentation
- Technical Documentation

---

## Interview Relevance

This lab provides practical examples that can be discussed during IT Support, Application Support, System Administration, and junior cybersecurity interviews.

Examples include:

- How to create and verify a Linux user.
- How UID and GID are used in Linux.
- How Linux home directories are created.
- How to verify account configuration.
- How to troubleshoot a simple user-administration error.
- How to document the resolution of an IT Operations request.

---

## Outcome

The Linux user account was successfully created, configured, and verified.

The practical task demonstrated a structured approach to Linux user administration, verification, troubleshooting, and technical documentation.

---

## Repository

**Project:** Enterprise IT Support Lab  
**Section:** Linux Administration  
**Lab:** 03 - Linux User Management  
**Status:** Completed
