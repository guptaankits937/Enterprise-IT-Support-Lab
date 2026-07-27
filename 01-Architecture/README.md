# Enterprise Architecture

## Overview

This module describes the architecture of the Enterprise IT Support Lab.

The objective is to build a realistic enterprise-style environment that simulates the daily responsibilities of an Application Support Engineer, Production Support Engineer, Linux Administrator, SQL Database Administrator, and Technical Support Engineer.

Rather than creating isolated practice labs, this project integrates multiple technologies into a single environment to demonstrate troubleshooting, administration, monitoring, documentation, and operational support.

---

# Business Scenario

MissionIT Solutions Ltd. is a fictional software and IT services company headquartered in Stockholm, Sweden.

The company provides an internal business application used by approximately 200 employees for:

* Employee authentication
* Customer management
* Support ticket management
* Operational reporting
* Internal administration

Business operations depend on the availability of this application.

When users experience login failures, application crashes, slow performance, or database connectivity issues, the IT Support team is responsible for restoring services as quickly as possible.

This lab simulates that production environment.

---

# Lab Objectives

The architecture has been designed to achieve the following objectives:

* Build an enterprise-style support environment
* Simulate production incidents
* Practice Linux administration
* Practice SQL database administration
* Investigate application failures
* Perform root cause analysis
* Create monitoring and automation scripts
* Produce professional technical documentation
* Prepare for technical interviews

---

# Logical Architecture

Internet

↓

Home Network

↓

VirtualBox Network

↓

Ubuntu Linux Server

↓

Business Application

↓

Microsoft SQL Server

↓

Windows Support Workstation

The environment is intentionally simple but follows enterprise support concepts.

---

# Lab Components

## Ubuntu Linux Server

Purpose:

* Application hosting
* Linux administration
* SSH access
* System monitoring
* Log analysis
* Bash scripting

---

## Windows Support Workstation

Purpose:

* Remote administration
* SQL Server Management Studio
* Technical documentation
* Incident investigation
* Windows administration

---

## SQL Database

Purpose:

* Store business application data
* User management
* Backup and restore
* Performance monitoring
* Database troubleshooting

---

# Network Design

The lab uses an isolated virtual network.

Benefits include:

* Safe testing
* Repeatable troubleshooting
* Controlled environment
* No impact on personal devices
* Easy recovery through VM snapshots

---

# Future Expansion

Future modules will introduce additional enterprise technologies including:

* Windows Server
* Active Directory
* DNS
* DHCP
* Sysmon
* Windows Event Logs
* Microsoft Sentinel
* KQL
* Threat Hunting
* Security Monitoring

---

# Why This Architecture?

This architecture has been selected because it closely reflects the responsibilities performed in many enterprise IT Support teams.

Instead of learning individual technologies separately, the lab demonstrates how Linux, databases, applications, monitoring, automation, and documentation work together to support business operations.

---

# Expected Learning Outcomes

After completing this module, I will be able to:

* Explain enterprise architecture
* Describe application dependencies
* Understand support workflows
* Identify system components
* Prepare production-style documentation
* Discuss enterprise environments during technical interviews

---

# Interview Questions

1. Explain the architecture of your Enterprise IT Support Lab.

2. Why did you choose Ubuntu Linux?

3. Why is SQL Server required?

4. How do application servers communicate with databases?

5. Why is documentation important in production support?

6. What would happen if the database became unavailable?

7. How would you isolate an application issue from a database issue?

8. Why is monitoring important in enterprise environments?

9. How would you scale this environment?

10. What improvements would you add in the future?

---

# Lessons Learned

* Enterprise environments consist of multiple dependent components.
* Proper architecture simplifies troubleshooting.
* Documentation is as important as technical implementation.
* A structured environment improves operational efficiency.
* Planning before implementation reduces future complexity.

