# Enterprise IT Support Lab --- Master Practical Roadmap

## Purpose

This roadmap defines the practical hands-on plan for the **Enterprise IT
Support Lab** portfolio.

The goal is not to collect a large number of labs. The goal is to build
practical troubleshooting experience that can be demonstrated in GitHub
and discussed confidently during IT Support, Application Support,
Technical Operations, System Administration, and junior Cybersecurity
interviews.

Each practical activity should follow an incident/ticket-based approach:

**Ticket → Problem → Investigation → Troubleshooting → Resolution →
Verification → Evidence → Documentation**

------------------------------------------------------------------------

## Standard GitHub Lab Format

Each individual lab follows the same structure:

    XX-Lab-Name/
    ├── README.md
    ├── Documentation/
    │   └── Detailed-Lab-Documentation.md
    └── Screenshots/
        ├── README.md
        └── Evidence-Screenshots

### README.md

Recruiter-friendly overview:

-   Overview
-   Ticket Information
-   Scenario
-   Environment
-   Tasks Completed
-   Key Commands
-   Verification
-   Troubleshooting
-   Evidence
-   Detailed Documentation
-   Skills Demonstrated
-   Interview Relevance
-   Outcome
-   Repository

### Documentation

Detailed technical record including objective, scenario, environment,
commands, command purpose, observed results, troubleshooting,
verification, lessons learned, skills demonstrated, outcome, and
repository information.

### Screenshots

Practical evidence captured during the lab. Only useful evidence should
be retained. Screenshots must not expose passwords, credentials, tokens,
public IP addresses, private keys, or other sensitive information.

------------------------------------------------------------------------

# Phase 1 --- Linux Administration

**Status:** In Progress

## Completed Tickets

### INC-0001 --- Linux User Management

**Status:** Completed\
**GitHub Lab:** `03-Linux-User-Management`

Practical work included user creation, home-directory creation, password
assignment, UID/GID verification, account validation, troubleshooting an
incorrect username, evidence capture, and documentation.

### INC-0002 --- Linux Group Management

**Status:** Completed\
**GitHub Lab:** `04-Linux-Group-Management`

Practical work included group creation, adding/removing users,
membership verification, access-management administration, cleanup,
evidence, and documentation.

### INC-0003 --- Linux File Permissions

**Status:** Completed\
**GitHub Lab:** `05-Linux-File-Permissions`

Practical work included file/directory creation, `chmod`, `chown`,
user-context access testing, permission-denied validation, directory
traversal investigation, supplementary group troubleshooting,
restoration, cleanup, evidence, and documentation.

### INC-0004 --- Linux Service Management & Troubleshooting

**Status:** Completed\
**GitHub Lab:** `06-Linux-Troubleshooting`

Practical work included SSH service/socket investigation, systemd socket
activation, TCP port 22 verification, controlled SSH outage and
recovery, `journalctl` investigation, VirtualBox host-to-VM network
troubleshooting, preservation of the SOC-LAB network, Host-Only
management networking, Netplan backup/configuration/validation, ping
testing, and successful remote SSH verification.

------------------------------------------------------------------------

## Planned Linux Tickets

### INC-0005 --- Linux Process Management

**Status:** Planned\
**Planned GitHub Lab:** `07-Linux-Process-Management`

**Scenario:** A Linux-hosted application becomes unresponsive. IT
Operations must identify the associated process, investigate its state,
terminate it safely, and verify recovery.

**Practical Plan:**

-   List running processes.
-   Understand PID and PPID.
-   Locate processes using `ps`.
-   Inspect processes/resource usage using `top`.
-   Create a controlled background process.
-   Identify the test process.
-   Use `kill` for graceful termination.
-   Verify process termination.
-   Understand when `kill -9` may be required.
-   Capture evidence and document the incident.

**Interview Value:** Process troubleshooting, Application Support, Linux
Operations.

### INC-0006 --- Linux Log Investigation

**Status:** Planned\
**Planned GitHub Lab:** `08-Linux-Log-Investigation`

**Scenario:** An application or system component reports an error. The
support engineer must locate relevant logs, filter events, identify
useful evidence, and determine the likely cause.

**Practical Plan:**

-   Explore `/var/log`.
-   Inspect system logs.
-   Use `journalctl`.
-   Filter logs by service and time.
-   Use `grep` and `tail`.
-   Reproduce a controlled event where appropriate.
-   Correlate timestamps with the incident.
-   Document findings and verification.

**Interview Value:** Log analysis, incident investigation, Application
Support.

### INC-0007 --- Linux Disk & Storage Troubleshooting

**Status:** Planned\
**Planned GitHub Lab:** `09-Linux-Disk-Storage-Troubleshooting`

**Scenario:** A Linux server reports low disk space or an application
cannot write data.

**Practical Plan:**

-   Check filesystem usage with `df`.
-   Check directory/file usage with `du`.
-   Review mounted filesystems.
-   Identify large files/directories in a controlled scenario.
-   Inspect inode usage.
-   Perform safe cleanup.
-   Verify recovered capacity.
-   Document investigation and resolution.

**Interview Value:** Server support, disk-space incidents, operational
troubleshooting.

### INC-0008 --- Bash Support Automation

**Status:** Planned\
**Planned GitHub Lab:** `10-Bash-Support-Automation`

**Scenario:** A repetitive Linux support health check needs to be
simplified using a small Bash script.

**Practical Plan:**

-   Create a support-health script.
-   Check hostname and uptime.
-   Check disk usage.
-   Check memory/system information.
-   Check service state.
-   Produce readable output.
-   Add basic conditions.
-   Execute and verify the script.
-   Document its IT Operations use.

**Interview Value:** Support automation, Bash basics, operational
efficiency.

### Linux Final Incident

**Status:** Planned

Perform one combined troubleshooting incident requiring several Linux
skills together: users/access, permissions, services, processes, logs,
networking, storage, recovery, and verification.

**Goal:** Demonstrate a structured end-to-end Linux troubleshooting
methodology without creating unnecessary repetitive labs.

------------------------------------------------------------------------

# Phase 2 --- SQL / Database Support

**Status:** Planned

Focus on support and administration scenarios rather than
database-development theory.

**Practical Areas:**

-   Database environment setup
-   Database/table inspection
-   Practical SQL support queries
-   User/login and permission administration
-   Connection/access troubleshooting
-   Backup and restore
-   Database availability checks
-   Blocking/session investigation
-   Basic performance investigation
-   Controlled database-support incident
-   Verification and technical documentation

**Possible Tickets:**

-   SQL Access & Permission Incident
-   Database Backup & Restore
-   SQL Blocking Investigation
-   Database Connectivity Troubleshooting
-   Database Support Incident

**Goal:** Rebuild practical SQL Server/database-support confidence and
create interview-ready troubleshooting examples.

------------------------------------------------------------------------

# Phase 3 --- Application Support

**Status:** Planned

This is a major portfolio priority for Application Support and
Production Support roles.

**Practical Areas:**

-   Application deployment/configuration
-   Application service verification
-   Configuration-file investigation
-   Application log analysis
-   Service dependencies
-   Linux process investigation
-   Database dependency checks
-   Network/port verification
-   HTTP/API troubleshooting
-   Authentication/access issues
-   Application restart and recovery
-   Incident documentation
-   Root-cause analysis

**Possible Tickets:**

-   Application unavailable
-   Application service stopped
-   Configuration error
-   Database connection failure
-   Permission/access issue
-   Port/service dependency failure
-   Application log error
-   API connectivity problem

**Goal:** Build realistic production-support stories that can be
explained confidently during interviews.

------------------------------------------------------------------------

# Phase 4 --- Monitoring & Incident Management

**Status:** Planned

**Practical Areas:**

-   Basic system/application monitoring
-   Service-health checks
-   Resource monitoring
-   Alert investigation
-   Incident triage
-   Priority and severity
-   Impact assessment
-   Escalation decisions
-   Incident timeline
-   Service restoration
-   Root Cause Analysis (RCA)
-   Runbook creation
-   Post-incident documentation

A final incident should combine monitoring, troubleshooting,
restoration, verification, and RCA.

**Goal:** Demonstrate an operational support mindset rather than only
command knowledge.

------------------------------------------------------------------------

# Phase 5 --- Support Automation

**Status:** Planned

Automation remains practical and support-focused.

**Planned Areas:**

-   Bash automation
-   Basic PowerShell where useful
-   Health checks
-   Log collection
-   Disk-space checks
-   Service-state checks
-   Repetitive administration
-   Simple output/report generation

**Goal:** Demonstrate safe automation of repetitive IT support tasks,
not software-development expertise.

------------------------------------------------------------------------

# Phase 6 --- Cybersecurity Bridge

**Status:** Planned

After the core IT/Application Support portfolio is strong, transition
toward security-focused practical work aligned with Digital Forensics.

## Windows Event Investigation

-   Authentication events
-   Failed logins
-   Process execution
-   PowerShell activity
-   Event filtering
-   Timeline investigation
-   Evidence documentation

## Security Operations Fundamentals

-   Alert triage
-   Event investigation
-   Incident workflow
-   Basic detection concepts
-   Investigation notes
-   Escalation decisions

## Microsoft Sentinel

Planned for later hands-on practice:

-   Log ingestion
-   KQL fundamentals
-   Security-event queries
-   Analytics rules
-   Alert triage
-   Incident investigation

Sentinel or Defender experience should only be added to the CV as
hands-on lab experience after the practical work has actually been
completed.

------------------------------------------------------------------------

# Portfolio Strategy

Prioritize **quality over quantity**.

Each important lab should answer:

1.  What was the problem?
2.  How was it investigated?
3.  What evidence was found?
4.  How was it resolved?
5.  How was the resolution verified?

Strong labs should demonstrate troubleshooting methodology, root-cause
isolation, log analysis, verification, documentation, incident-style
thinking, and safe change implementation.

------------------------------------------------------------------------

# CV & Interview Positioning

These labs should be described as:

-   Hands-on Lab Experience
-   Technical Projects
-   Home Lab / Portfolio Projects
-   Practical IT Support Experience

They should **not** be presented as paid professional employment
experience.

During interviews, focus on explaining the practical troubleshooting
process and decisions made during each incident.

------------------------------------------------------------------------

# Documentation Rules

For every lab:

1.  Perform practical work first.
2.  Capture only useful evidence screenshots.
3.  Use clear screenshot filenames.
4.  Create detailed technical documentation after practical work.
5.  Create a concise recruiter-facing README.
6.  Update the relevant section README.
7.  Update `08-Documentation/Lab-Journal.md`.
8.  Commit with a clear professional message.
9.  Never document tools or experience that were not actually used.
10. Never expose credentials, secrets, tokens, private keys, public IP
    addresses, or sensitive information.

------------------------------------------------------------------------

# Master Project Documentation

Project-level documentation remains in:

    08-Documentation/
    ├── Lab-Journal.md
    └── MASTER-PRACTICAL-ROADMAP.md

Individual lab documentation and screenshots remain inside each
respective lab folder.

------------------------------------------------------------------------

# Current Progress

**Linux Administration**

-   INC-0001 --- Linux User Management --- Completed
-   INC-0002 --- Linux Group Management --- Completed
-   INC-0003 --- Linux File Permissions --- Completed
-   INC-0004 --- Linux Service Management & Troubleshooting ---
    Completed
-   INC-0005 --- Linux Process Management --- Planned
-   INC-0006 --- Linux Log Investigation --- Planned
-   INC-0007 --- Linux Disk & Storage Troubleshooting --- Planned
-   INC-0008 --- Bash Support Automation --- Planned
-   Linux Final Incident --- Planned

**SQL / Database Support:** Planned\
**Application Support:** Planned\
**Monitoring & Incident Management:** Planned\
**Support Automation:** Planned\
**Cybersecurity Bridge:** Planned

------------------------------------------------------------------------

# Repository Information

**Repository:** Enterprise-IT-Support-Lab\
**Document:** Master Practical Roadmap\
**Location:** `08-Documentation/MASTER-PRACTICAL-ROADMAP.md`\
**Status:** Active\
**Last Updated:** 11 August 2026\
**Version:** 1.0
