# Linux File Permissions

## Overview

This lab demonstrates Linux file permission and ownership management in an Ubuntu Server environment.

The objective was to create a test file, inspect its default permissions, modify permissions using `chmod`, change file ownership using `chown`, and verify how Linux permissions control access for different users.

The lab also demonstrates practical access testing and basic troubleshooting during Linux system administration.

This lab is part of the **Enterprise IT Support Lab** project.

---

## Ticket Information

**Ticket ID:** INC-0003  
**Department:** IT Operations  
**Priority:** Medium  
**Status:** Completed

---

## Scenario

The IT Operations team needed to secure a support report containing internal incident information.

A test file named `support-report.txt` was created and its permissions were reviewed.

The file permissions were changed to restrict access, ownership was transferred to the user `john`, and access was tested from different user contexts.

The temporary lab resources were removed after completing the verification process.

---

## Tasks Completed

- Verified the current logged-in user and environment.
- Created a temporary permissions lab directory.
- Created the `support-report.txt` test file.
- Reviewed the file's default permissions.
- Changed file permissions to `640` using `chmod`.
- Changed file ownership using `chown`.
- Changed both the file owner and group.
- Tested access from the `ankit` user account.
- Verified owner access using the `john` account.
- Added test content as the file owner.
- Verified successful owner read/write access.
- Verified that unauthorized access was denied.
- Restored file ownership before cleanup.
- Removed the temporary lab directory and test file.

---

## Commands Used

```bash
whoami
pwd
id

mkdir permissions-lab
cd permissions-lab
touch support-report.txt
ls -l

chmod 640 support-report.txt
ls -l support-report.txt

id john
sudo chown john support-report.txt
ls -l support-report.txt

sudo chown john:john support-report.txt
ls -l support-report.txt

cat support-report.txt
sudo -u john cat support-report.txt

sudo -u john sh -c 'echo "IT Support Incident Report" > support-report.txt'
sudo -u john cat support-report.txt
cat support-report.txt

sudo chown ankit:ankit support-report.txt
cd ..
rm -r permissions-lab
```

---

## Understanding Permission 640

The permission value `640` represents:

- **6 — Owner:** Read + Write (`rw-`)
- **4 — Group:** Read only (`r--`)
- **0 — Others:** No permissions (`---`)

This results in:

```text
-rw-r-----
```

This configuration allows the file owner to read and modify the file, allows members of the assigned group to read it, and prevents all other users from accessing it.

---

## Ownership and Access Verification

The file ownership was changed from:

```text
ankit ankit
```

to:

```text
john ankit
```

and then to:

```text
john john
```

using the `chown` command.

With permissions set to `640` and ownership assigned to `john:john`, the `ankit` user received:

```text
Permission denied
```

when attempting to read the file.

The `john` user was able to write:

```text
IT Support Incident Report
```

and successfully read the same content.

This demonstrated that the configured Linux permissions were actively controlling access to the file.

---

## Troubleshooting

During the ownership change, an incorrect filename was initially entered:

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

This demonstrates a basic troubleshooting process:

1. Review the error message.
2. Verify the command and target filename.
3. Correct the input.
4. Re-run the command.
5. Verify the result.

---

## Cleanup Note

Before cleanup, the following ownership restoration command was executed:

```bash
sudo chown ankit:ankit support-report.txt
```

The temporary `permissions-lab` directory was then removed.

A separate `ls -l` ownership verification was not captured before the directory was deleted, so the documentation does not claim a post-restoration verification result.

---

## Skills Demonstrated

- Linux File Permission Management
- `chmod` Numeric Permissions
- Linux File Ownership
- `chown` Administration
- Owner, Group, and Others Permissions
- Read and Write Access Control
- User Context Testing
- Access Verification
- Basic Linux Troubleshooting
- Principle of Least Privilege
- System Administration
- Technical Documentation

---

## Evidence

Eight screenshots were captured during the lab:

1. `01-current-user-environment.png`
2. `02-create-file-default-permissions.png`
3. `03-change-file-permissions-chmod.png`
4. `04-change-file-ownership-chown.png`
5. `05-change-owner-and-group.png`
6. `06-test-file-access-permissions.png`
7. `07-verify-owner-read-write-access.png`
8. `08-restore-ownership-and-cleanup.png`

Detailed commands, verification results, troubleshooting notes, and screenshots are maintained within the lab documentation and evidence folders.

---

## Outcome

Successfully demonstrated Linux file permission and ownership management using `chmod` and `chown`.

The lab verified that file permissions can restrict unauthorized access while allowing the designated owner to read and modify protected files.

The temporary lab resources were removed after testing.

---

## Repository Information

**Repository:** Enterprise-IT-Support-Lab  
**Section:** 02-Linux  
**Lab:** 05-Linux-File-Permissions  
**Documentation:** Documentation/Linux-File-Permissions.md  
**Screenshots:** Screenshots/  
**Status:** Completed  
**Version:** 1.0
