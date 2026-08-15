# Linux File Permissions

## Overview

This lab demonstrates practical Linux file permission and ownership management in an Ubuntu Server environment.

The scenario simulates an IT Operations requirement to secure an internal support report, restrict access using Linux permissions, transfer ownership to an authorized user, and verify access from different user contexts.

This lab is part of the **Enterprise IT Support Lab** portfolio.

---

## Ticket Information

**Ticket ID:** INC-0003  
**Department:** IT Operations  
**Priority:** Medium  
**Status:** Completed  

---

## Scenario

The IT Operations team needed to secure a support report containing internal incident information.

A test file named `support-report.txt` was created and its default permissions were reviewed.

The permissions were configured so that:

- The file owner could read and modify the file.
- Members of the assigned group could read the file.
- Other users had no access.

Ownership was transferred to the existing user `john`, and access was tested from different user contexts.

Temporary lab resources were removed after completing the testing.

---

## Environment

- Ubuntu Server
- Linux Terminal
- Sudo Privileges
- Local User Management
- Existing Administrative User: `ankit`
- Existing Test User: `john`
- Test File: `support-report.txt`
- Test Directory: `permissions-lab`

---

## Tasks Completed

During this lab, I performed the following tasks:

1. Verified the current user and environment.
2. Created a temporary permissions lab directory.
3. Created the `support-report.txt` test file.
4. Reviewed the file's default permissions.
5. Changed file permissions to `640` using `chmod`.
6. Verified the updated permissions.
7. Changed file ownership using `chown`.
8. Changed both the file owner and group.
9. Tested access from the `ankit` user account.
10. Verified owner access using the `john` account.
11. Tested owner write permission.
12. Verified owner read permission.
13. Confirmed that unauthorized access was denied.
14. Troubleshot an incorrect filename during an ownership change.
15. Restored ownership before cleanup.
16. Removed the temporary lab resources.
17. Documented the implementation and captured supporting evidence.

---

## Key Commands

```bash
whoami
```

```bash
pwd
```

```bash
id
```

```bash
mkdir permissions-lab
```

```bash
touch support-report.txt
```

```bash
ls -l
```

```bash
chmod 640 support-report.txt
```

```bash
sudo chown john support-report.txt
```

```bash
sudo chown john:john support-report.txt
```

```bash
sudo -u john cat support-report.txt
```

```bash
sudo -u john sh -c 'echo "IT Support Incident Report" > support-report.txt'
```

```bash
sudo chown ankit:ankit support-report.txt
```

```bash
rm -r permissions-lab
```

---

## Verification

The following checks confirmed successful completion of the practical task:

- Default file permissions were inspected.
- Permissions were successfully changed to `640`.
- File ownership was successfully transferred to `john`.
- Both owner and group were successfully changed to `john:john`.
- Unauthorized access from the `ankit` context was denied.
- The `john` user could access the protected file.
- Owner write access was successfully tested.
- Owner read access was successfully verified.
- Permission restrictions remained effective after content was added.
- Temporary lab resources were removed after testing.

---

## Troubleshooting

During the ownership change, an incorrect filename was entered:

```bash
sudo chown john suport-report.txt
```

Linux returned:

```text
No such file or directory
```

The filename was reviewed and corrected:

```bash
sudo chown john support-report.txt
```

The command then completed successfully.

This demonstrated a basic troubleshooting process of reviewing the error, identifying the incorrect filename, correcting the command, and verifying the result.

---

## Evidence

Screenshots captured during the practical lab include:

- `01-current-user-environment.png`
- `02-create-file-default-permissions.png`
- `03-change-file-permissions-chmod.png`
- `04-change-file-ownership-chown.png`
- `05-change-owner-and-group.png`
- `06-test-file-access-permissions.png`
- `07-verify-owner-read-write-access.png`
- `08-restore-ownership-and-cleanup.png`

Supporting screenshots are available in the [`Screenshots`](./Screenshots/) directory.

---

## Detailed Documentation

Complete technical documentation, including command explanations, permission calculations, access testing, troubleshooting, verification results, and lessons learned, is available here:

[`Linux-File-Permissions.md`](./Documentation/Linux-File-Permissions.md)

---

## Skills Demonstrated

- Linux File Permission Management
- Linux Access Control
- `chmod` Numeric Permissions
- Linux File Ownership
- `chown` Administration
- Owner, Group, and Others Permissions
- Access Verification
- User Context Testing
- Principle of Least Privilege
- Linux Troubleshooting
- System Administration
- Incident/Ticket Documentation
- Technical Documentation

---

## Interview Relevance

This lab provides practical examples that can be discussed during IT Support, Application Support, System Administration, and junior cybersecurity interviews.

Examples include:

- How Linux file permissions work.
- How owner, group, and others permissions are represented.
- How numeric permission `640` is calculated.
- How to modify permissions using `chmod`.
- How to change file ownership using `chown`.
- How to test access from different user contexts.
- How Linux prevents unauthorized file access.
- How to troubleshoot an incorrect filename in an administrative command.
- How the principle of least privilege can be applied using Linux permissions.

---

## Outcome

The test file was successfully secured using Linux file permissions and ownership controls.

The designated owner could read and modify the protected file while unauthorized access was denied.

The practical task demonstrated Linux access control, ownership management, verification, troubleshooting, and cleanup using standard system administration practices.

---

## Repository Information

**Project:** Enterprise IT Support Lab  
**Section:** Linux Administration  
**Lab:** 05 - Linux File Permissions  
**Status:** Completed
