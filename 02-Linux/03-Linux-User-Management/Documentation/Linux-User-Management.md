# Linux User Management

## Lab Information

**Lab Name:** Linux User Management  
**Project:** Enterprise IT Support Lab  
**Date:** 05 August 2026  
**Operating System:** Ubuntu Server  

### Objective

Learn how to create a new Linux user, assign a password, verify the account, and validate the user's home directory using enterprise administration practices.

---

## Ticket Information

**Ticket ID:** INC-0001  
**Department:** IT Operations  
**Priority:** Medium  
**Status:** Completed  

---

## Scenario

A new employee joined the company.

The IT Operations team received a request from Human Resources (HR) to create a new Linux account for the employee.

The account must be created securely, assigned a password, and verified before handing it over to the employee.

---

## Environment

- Ubuntu Server
- Terminal
- Sudo Privileges
- Local User Management

---

## Lab Duration

**Estimated Time:** 20–30 Minutes

---

## Commands Used

### Check Current Logged-in User

```bash
whoami
```

**Purpose:**  
Verify the currently logged-in user before performing administrative tasks.

---

### Display User Information

```bash
id
```

**Purpose:**  
Display information about the current user, including:

- User ID (UID)
- Group ID (GID)
- User Groups

---

### Check Hostname

```bash
hostname
```

**Purpose:**  
Identify the current Linux server.

---

### Create New User

```bash
sudo useradd -m john
```

**Purpose:**  
Create a new Linux user named `john`.

The `-m` option automatically creates the user's home directory.

---

### Set Password

```bash
sudo passwd john
```

**Purpose:**  
Assign a password to the newly created user.

---

### Verify User

```bash
id john
```

**Purpose:**  
Verify that the new user account has been created successfully and display its UID, GID, and group membership.

---

### Verify Home Directory

```bash
ls /home
```

**Purpose:**  
Confirm that the user's home directory was created successfully.

---

## Verification Results

The following checks confirmed successful user creation:

- User `john` exists.
- Password was assigned successfully.
- User information was verified.
- Home directory was created successfully.

---

## Troubleshooting

### Issue

While assigning the password, an incorrect username was entered:

```bash
sudo passwd joh
```

The system returned:

```text
passwd: user 'joh' does not exist
```

### Resolution

The username was corrected and the command was executed again:

```bash
sudo passwd john
```

The password was then updated successfully.

This demonstrated the importance of verifying usernames when performing user-administration tasks.

---

## Evidence

The following screenshots were captured during the lab:

1. `01-whoami.png` — Verified the currently logged-in user.
2. `02-id-command.png` — Displayed UID, GID, and group information.
3. `03-password-updated.png` — Confirmed successful password assignment.
4. `04-id-john.png` — Verified the newly created `john` account.
5. `05-home-directories.png` — Confirmed creation of the user's home directory.

---

## Lessons Learned

During this lab, I learned how to:

- Verify the currently logged-in Linux user.
- Understand basic UID and GID information.
- Identify the Linux server using the hostname.
- Create a new Linux user account.
- Automatically create a home directory using the `-m` option.
- Assign a password to a user account.
- Verify a newly created account.
- Confirm creation of the user's home directory.
- Troubleshoot an incorrect username during password configuration.

---

## Skills Demonstrated

- Linux User Administration
- User Account Management
- Password Management
- Linux Verification Commands
- Basic Troubleshooting
- System Administration
- Technical Documentation

---

## Outcome

Successfully completed the Linux User Management lab by creating, configuring, and verifying a new Linux user account using standard Linux administration commands.

The account was successfully created with its own home directory, assigned a password, and verified using Linux user-management commands.

---

## Repository Information

**Repository:** Enterprise-IT-Support-Lab  
**Lab:** `02-Linux/03-Linux-User-Management/`  
**Documentation:** `02-Linux/03-Linux-User-Management/Documentation/Linux-User-Management.md`  
**Screenshots:** `02-Linux/03-Linux-User-Management/Screenshots/`  
**Status:** Completed  
**Version:** 1.0
