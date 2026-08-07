Linux User Management
Lab Information
Lab Name: Linux User Management

Project: Enterprise IT Support Lab

Date: 05 August 2026

Operating System: Ubuntu Server

Objective:

Learn how to create a new Linux user, assign a password, verify the account, and validate the user's home directory using enterprise administration practices.

Ticket Information
Ticket ID: INC-0001

Department: IT Operations

Priority: Medium

Status: Completed

Scenario
A new employee joined the company.

The IT Operations team received a request from Human Resources (HR) to create a new Linux account for the employee.

The account must be created securely, assigned a password, and verified before handing it over to the employee.

Environment
Ubuntu Server
Terminal
Sudo Privileges
Local User Management
Lab Duration
Estimated Time: 20–30 Minutes

Commands Used
Check Current Logged-in User
whoami
Purpose:

Verify the currently logged-in user before performing administrative tasks.

Display User Information
id
Purpose:

Display:

User ID (UID)
Group ID (GID)
User Groups
Check Hostname
hostname
Purpose:

Identify the current Linux server.

Create New User
sudo useradd -m john
Purpose:

Create a new Linux user named john.

The -m option automatically creates the user's home directory.

Set Password
sudo passwd john
Purpose:

Assign a password to the newly created user.

Verify User
id john
Purpose:

Verify that the new user account has been created successfully.

Verify Home Directory
ls /home
Purpose:

Confirm that the user's home directory was created successfully.

Verification Results
The following checks confirmed successful user creation:

User "john" exists.
Password assigned successfully.
Home directory created.
User information verified.
Troubleshooting
Issue
Incorrect command entered:

sudo passwd joh
Result:

passwd: user 'joh' does not exist
Resolution:

Corrected the username:

sudo passwd john
Password updated successfully.

Evidence
Screenshots

01-whoami.png
02-id-command.png
03-password-updated.png
04-id-john.png
05-home-directories.png
Lessons Learned
Verified the currently logged-in user.
Understood UID and GID.
Learned the importance of the hostname.
Created a Linux user.
Assigned a password.
Verified the user account.
Verified the home directory.
Understood the purpose of the -m option.
Learned how to troubleshoot an incorrect username.
Skills Demonstrated
Linux User Administration
User Account Management
Password Management
Linux Verification Commands
Basic Troubleshooting
System Administration
Outcome
Successfully completed the Linux User Management lab by creating and verifying a new user account using enterprise administration practices.

## Repository Information

Repository: Enterprise-IT-Support-Lab

Documentation: 02-Linux/03-Linux-User-Management/Documentation/Linux-User-Management.md

Screenshots: 02-Linux/03-Linux-User-Management/Screenshots/

Status: Completed

Version: 1.0



