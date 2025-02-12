# VMAssist

VMAssist is a PowerShell script you run within the guest operating system of an Azure virtual machine to diagnose common health and configuration issues with the Azure VM Guest Agent. It will also gather various information about the system such as firewall rules, running services, running drivers, installed software, NIC settings, and installed Windows Updates.

Azure VM Guest Agent health is critical to the proper functioning of Azure VM extensions.

Running VMAssist generates a report showing the results of each check it performs and suggests mitigations for issues it finds.

# Prerequisites

 - Windows Server 2012 R2 and later versions of Windows
 - Windows Powershell 4.0+ and PowerShell 6.0+

# Usage

## Automatic download and run (recommended)
RDP into the VM and from an elevated PowerShell window run the following to download and run the script: 
```powershell
(Invoke-WebRequest -Uri https://raw.githubusercontent.com/kegregoi/VMAssist/refs/heads/main/VMAssist.ps1 -OutFile VMAssist.ps1) | .\VMAssist.ps1
```

## Manual download and run
Download:
```powershell
Invoke-WebRequest -Uri https://raw.githubusercontent.com/kegregoi/VMAssist/refs/heads/main/VMAssist.ps1 -OutFile VMAssist.ps1
```
Run the script:
```powershell
.\VMAssist.ps1
```
## Known issues downloading the file
If you get this error ```The request was aborted: Could not create SSL/TLS secure channel``` when trying to download the file then either:
 1. Run ```[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12``` in the PowerShell window and retry the command
 1. Or instead, just manually download the file ```VMAssist.ps1``` [from a web browser.](https://github.com/kegregoi/VMAssist/blob/main/VMAssist.ps1)

# Analyzing output

The script will run a series of checks to analyze the health of the VM Guest Agent and check for various known configurations that could cause issues. Each check will either pass or fail in the PowerShell window. 

Once completed, it will also generate a log file and an html report:
 - C:\logs\VMAssist_*.log
 - C:\logs\VMAssist_*.htm

The .log file will have a copy of the results that are displayed in the PowerShell window for later reference.

The .htm file is a report that shows all of the checks and findings if there are any failures. It will also have additional information about the Window and the VM that can further assist in troubleshooting any issues that are found.

 If you open a support request, please include both of the above files to aid your support representative in helping you.