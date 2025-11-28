# Win-Audit-PS: Windows System Health Monitor

## Project Overview

**Win-Audit-PS** is an automated PowerShell script designed to perform a rapid security and health audit of a Windows system. The project was created to demonstrate proficiency in core Windows administrative commands and PowerShell scripting for automation purposes.

The script executes a series of diagnostics and compiles the data into a single, human-readable text report saved to a structured audit directory.

## Key Features

**System Information Gathering:** Collects OS version, hardware details, and processor information.
**Security Service Check:** Audits the status of critical services, including **Windows Defender**, **Windows Firewall (MpsSvc)**, and **Windows Update (wuauserv)**.
**Patch Management Review:** Uses `Get-HotFix` to quickly list critical updates installed in the last 30 days.
**Network Diagnostics:** Utilizes modern PowerShell cmdlets like `Get-NetIPConfiguration` and `Test-NetConnection` to verify network settings and external connectivity.
**Performance Monitoring:** Identifies and reports the top 10 processes consuming the most CPU resources.

## Technical Concepts Demonstrated

| Concept | PowerShell Cmdlet/Function |
| :--- | :--- |
| **Scripting Fundamentals** | Variables, `foreach` loops, `if/else` conditional logic, and piping (`|`). |
| **System Security** | Understanding and configuring the **PowerShell Execution Policy**. |
| **System Administration** | Using `Get-Service` to manage critical system processes. |
| **Diagnostics** | Using `Get-Process` with `Sort-Object` to perform basic performance auditing. |
| **Modern Networking** | Utilizing `Get-NetIPConfiguration` and `Test-NetConnection` (modern alternative to `ipconfig` and `ping`). |
| **Reporting & Output** | Redirecting and formatting output using `Out-File -Append` and `Format-Table`. |

## How to Run the Script

1.  Open a PowerShell terminal as Administrator.
2.  **Execution Policy:** Temporarily set the execution policy to allow local scripts to run:
    ```powershell
    Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope Process
    ```
3.  **Execution:** Navigate to the script's directory and run it:
    ```powershell
    .\Get-SystemHealthReport.ps1
    ```
    A new report file will be generated in the systematic log path.

## Troubleshooting and Production Enhancements

The initial audit flagged standard environmental issues, which were resolved to ensure a clean, production-ready report.

**Critical Service Stabilization:** Initial audits flagged services like **TermService** and **wuauserv** as stopped. These were quickly stabilized using **`Set-Service`** to ensure persistent **Automatic** startup, guaranteeing system health compliance.
**Network Diagnostics Workaround:** External connectivity failed due to host-level firewall filtering (blocking ICMP traffic). The script was enhanced to use **`Get-NetAdapter`** to verify the network adapter status is `Up`, providing accurate network health reporting while isolating the blockage to the external environment.

**Report Path:** `C:\AuditLogs\$($env:COMPUTERNAME)\$(Get-Date -Format 'yyyy-MM-dd')`
