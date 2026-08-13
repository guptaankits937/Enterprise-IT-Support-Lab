# Linux Process Management - Detailed Documentation

## Ticket Information

**Ticket ID:** INC-0005  
**Department:** IT Operations  
**Priority:** Medium  
**Status:** Completed  
**Environment:** Ubuntu Server

---

## Objective

The objective of this lab was to develop a practical understanding of Linux process investigation and management using a controlled application-support scenario.

The lab simulated an unresponsive Linux-hosted application process. A harmless `sleep` process was used to represent the affected application.

The investigation focused on identifying the process, examining its process information, monitoring system activity, applying the least disruptive corrective action, verifying the result, demonstrating forced termination, and performing final cleanup verification.

---

## Incident Scenario

An application hosted on a Linux server is reported as unresponsive.

In a real support environment, immediately terminating an unknown process could cause service disruption or affect other users.

The investigation therefore followed a structured workflow:

**Observe → Identify → Investigate → Act → Verify → Clean Up**

The objective was to understand the affected process before taking corrective action.

---

## Step 1 - Review Running Processes

### Command

```bash
ps aux
```

### Purpose

The `ps aux` command was used to review currently running processes on the Linux server.

It provides information such as:

- Process owner
- Process ID (PID)
- CPU utilization
- Memory utilization
- Process state
- Process start information
- Executed command

### Support Relevance

During an application-support incident, reviewing running processes can help determine whether an expected application process is running and whether any process appears to be consuming unusual system resources.

---

## Step 2 - Review PID and PPID Information

### Command

```bash
ps -ef
```

### Purpose

This command provides a process listing that includes both the Process ID (PID) and Parent Process ID (PPID).

A PID uniquely identifies a running process.

A PPID identifies the parent process responsible for starting another process.

### Support Relevance

Understanding parent-child process relationships can help during troubleshooting when investigating how an application, script, service, or subprocess was started.

---

## Step 3 - Monitor Processes in Real Time

### Command

```bash
top
```

### Purpose

The `top` utility was used to observe running processes and system resource utilization in real time.

It displays information including:

- CPU utilization
- Memory utilization
- Running processes
- Process IDs
- Process states
- System load

### Observation

The server was operating normally during the controlled lab and no abnormal resource utilization was intentionally generated.

### Support Relevance

If an application becomes slow or unresponsive in a production environment, `top` can help determine whether high CPU or memory utilization may be contributing to the incident.

---

## Step 4 - Create a Controlled Application Process

### Command

```bash
sleep 1000 &
```

### Purpose

A harmless background process was created to safely represent the simulated application.

The `&` symbol runs the command in the background, allowing the terminal to remain available for further investigation.

### Observation

The shell returned:

```text
[1] 1058
```

The background process was assigned PID:

```text
1058
```

### Support Relevance

Using a controlled process allowed process investigation and termination techniques to be practiced without affecting an actual application or service.

---

## Step 5 - Identify the Target Process

### Command

```bash
ps aux | grep '[s]leep 1000'
```

### Purpose

The running process list was searched for the controlled `sleep 1000` process.

The `[s]leep` pattern was used so that the `grep` command itself would not appear as a matching result.

### Observation

The process was identified with:

```text
USER: ankit
PID: 1058
COMMAND: sleep 1000
```

### Support Relevance

Before terminating a process, the correct process should be identified to reduce the risk of stopping an unrelated application or system component.

---

## Step 6 - Investigate Process Details

### Command

```bash
ps -o pid,ppid,user,stat,etime,cmd -p 1058
```

### Purpose

The command displayed selected information specifically for PID `1058`.

The fields examined were:

- `PID` - Process ID
- `PPID` - Parent Process ID
- `USER` - Process owner
- `STAT` - Process state
- `ETIME` - Elapsed running time
- `CMD` - Executed command

### Observation

The investigation showed:

```text
PID: 1058
PPID: 961
USER: ankit
STAT: S
CMD: sleep 1000
```

The process state `S` indicated that the process was in a sleeping state.

### Support Relevance

This step demonstrates why a process should be investigated before corrective action is taken.

The support engineer can confirm the process identity, owner, state, parent relationship, and command before deciding whether termination is appropriate.

---

## Step 7 - Graceful Process Termination

### Command

```bash
kill 1058
```

### Purpose

The controlled process was terminated using the standard `kill` command.

Without specifying another signal, `kill` sends SIGTERM.

SIGTERM requests that the process terminate and allows the process an opportunity to shut down normally.

### Why SIGTERM First?

Graceful termination is generally preferable to forced termination because an application may need an opportunity to:

- Close resources
- Complete cleanup operations
- Release files
- Close connections
- Perform its normal shutdown procedure

For this reason, forced termination should not automatically be the first response to an unresponsive process.

---

## Step 8 - Verify Graceful Termination

### Command

```bash
ps -p 1058 -o pid,ppid,user,stat,cmd
```

### Purpose

The process table was checked specifically for PID `1058`.

### Observation

The command displayed the column headings but no process entry for PID `1058`.

The shell also reported:

```text
[1]+ Terminated sleep 1000
```

This confirmed that the controlled process had successfully terminated.

### Key Operational Principle

Executing a corrective command does not by itself prove that an incident has been resolved.

The result should be independently verified.

The workflow therefore becomes:

**Corrective Action → Verification → Resolution**

---

## Step 9 - Create a Process for SIGKILL Testing

### Command

```bash
sleep 2000 &
```

### Purpose

A second harmless background process was created so that forced termination could be demonstrated separately from the graceful termination test.

### Observation

The new process received PID:

```text
1218
```

Using a separate controlled process ensured that the SIGKILL demonstration did not affect any real system service.

---

## Step 10 - Force Process Termination

### Command

```bash
kill -9 1218
```

### Purpose

The command sends SIGKILL to PID `1218`.

Unlike SIGTERM, SIGKILL forces the operating system to terminate the process.

The process cannot handle or ignore SIGKILL.

### Operational Consideration

SIGKILL should generally be considered a last-resort action when normal process termination is unsuccessful or when immediate termination is specifically required.

A typical troubleshooting approach is therefore:

```text
Investigate Process
        ↓
Attempt Graceful Termination
        ↓
Verify Result
        ↓
Use Forced Termination Only If Required
```

---

## Step 11 - Verify SIGKILL Termination

### Command

```bash
ps -p 1218 -o pid,ppid,user,stat,cmd
```

### Purpose

The process table was checked to determine whether PID `1218` still existed.

### Observation

No process entry was returned for PID `1218`.

The shell also reported:

```text
[1]+ Killed sleep 2000
```

This confirmed successful forced termination.

---

## Step 12 - Final Cleanup Verification

### Command

```bash
pgrep -a sleep
```

### Purpose

The final check searched for any remaining processes matching `sleep`.

The `-a` option would display both the PID and command line for any matching processes.

### Observation

The command returned no output.

This confirmed that no controlled `sleep` processes remained running after the lab.

### Support Relevance

Final cleanup verification helps ensure that temporary processes or resources created during troubleshooting do not remain active after the incident investigation is complete.

---

## SIGTERM vs SIGKILL

### SIGTERM

Example:

```bash
kill PID
```

SIGTERM requests graceful termination.

It should normally be considered before forced termination because the application has an opportunity to perform normal shutdown operations.

### SIGKILL

Example:

```bash
kill -9 PID
```

SIGKILL forces immediate termination by the operating system.

The target process cannot catch or ignore this signal.

It should generally be reserved for situations where graceful termination is unsuccessful or forced termination is specifically required.

---

## Process Investigation Workflow

The complete troubleshooting workflow demonstrated during this lab was:

```text
Application Reported Unresponsive
            ↓
Review Running Processes
            ↓
Monitor System Activity
            ↓
Identify Target Process
            ↓
Confirm PID / PPID / User / State / Command
            ↓
Take Corrective Action
            ↓
Attempt Graceful Termination
            ↓
Verify Termination
            ↓
Use SIGKILL Only If Required
            ↓
Verify Again
            ↓
Perform Final Cleanup Check
            ↓
Close Incident
```

This approach reduces the risk of taking corrective action against the wrong process and ensures that recovery is verified before incident closure.

---

## Evidence

The following screenshots were captured during the practical:

1. `01-list-running-processes-ps-aux.png`
2. `02-view-pid-ppid-ps-ef.png`
3. `03-live-process-monitoring-top.png`
4. `04-create-background-process.png`
5. `05-identify-background-process.png`
6. `06-investigate-process-details.png`
7. `07-graceful-process-termination.png`
8. `08-verify-process-termination.png`
9. `09-create-process-for-sigkill-test.png`
10. `10-force-terminate-process-sigkill.png`
11. `11-verify-sigkill-termination.png`
12. `12-final-process-cleanup-verification.png`

Supporting evidence is maintained in the `Screenshots/` directory.

---

## Lessons Learned

This lab demonstrated several important operational principles:

1. Do not immediately terminate a process simply because an application is reported as unresponsive.
2. Identify and investigate the target process before taking corrective action.
3. PID and PPID information can help understand process identity and relationships.
4. Process state and runtime information provide useful investigation context.
5. Real-time monitoring can help identify system resource issues.
6. Graceful termination should normally be attempted before forced termination.
7. SIGKILL should be treated as a stronger corrective action rather than the default response.
8. Corrective actions should always be followed by verification.
9. Temporary troubleshooting resources should be checked and cleaned up before incident closure.
10. A structured investigation is more valuable than simply knowing individual Linux commands.

---

## Interview Explanation

A concise way to explain this lab during an interview:

> I simulated an unresponsive application using a controlled Linux background process. I first reviewed and monitored the running processes, identified the target PID, and investigated its parent process, owner, state, runtime, and command. I then performed a graceful termination using SIGTERM and independently verified that the process had stopped. I also demonstrated SIGKILL on a separate controlled process to understand forced termination and verified the result. Finally, I checked that no test processes remained running. The main focus was following an investigate, act, and verify troubleshooting workflow rather than immediately killing a process.

---

## Final Outcome

The controlled application processes were successfully identified, investigated, terminated, and verified.

Both graceful termination using SIGTERM and forced termination using SIGKILL were demonstrated safely.

Final cleanup verification confirmed that no controlled test processes remained running.

**Ticket Status: Completed**
