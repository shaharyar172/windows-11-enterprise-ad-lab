# Windows 11 Enterprise Active Directory Home Lab

## Project Overview

Built and troubleshot a Windows 11 Enterprise virtual machine using VirtualBox in preparation for an Active Directory home lab.

This project documents real-world virtualization conflicts and system-level troubleshooting involving Hyper-V, VBS (Virtualization-Based Security), and Windows security features.

---

## Environment

- **Host OS:** Windows 11
- **Hypervisor:** VirtualBox 7.2.6
- **VM OS:** Windows 11 Enterprise Evaluation (64-bit)
- **Hardware:** NVMe SSD, 16GB RAM
- **BIOS Virtualization:** Enabled

---

# Issue: Windows 11 VM Fails to Boot (Black Screen)

## Symptoms

- VM launched but displayed a black screen
- Windows installer did not appear
- Inconsistent boot behavior
- VirtualBox failed to fully control virtualization extensions

---

## Investigation

- Verified BIOS virtualization was enabled
- Confirmed ISO was properly attached
- Adjusted VM chipset to PIIX3
- Disabled Secure Boot
- Increased video memory to 128MB
- Checked Task Manager for system resource usage
- Reviewed VirtualBox version compatibility

---

## Root Cause

Conflict between VirtualBox and Windows Hyper-V / Virtual Machine Platform / VBS.

Windows was using its own hypervisor (Hyper-V), which prevented VirtualBox from accessing hardware virtualization extensions directly.

---

## Resolution Steps

1. Disabled **Virtual Machine Platform**
2. Disabled **Windows Hyper-V**
3. Disabled **Memory Integrity (Core Isolation)**
4. Rebooted the system
5. Relaunched the VM

---

## Result

After disabling Hyper-V and VBS-related features, VirtualBox successfully accessed hardware virtualization extensions and the Windows 11 VM booted correctly.

---

# Screenshots

## BIOS Virtualization Enabled
![BIOS Virtualization](images/bios-virtualization.jpg.jpeg)

## Black Screen Issue
![Black Screen](images/black-screen.jpg.jpeg)

## Full Screen Hotkey Message
![Full Screen Hotkey](images/full-screen-hotkey.jpg.jpeg)

## ISO Download
![ISO Download](images/iso-download.jpg)

## Task Manager - Memory Usage
![Task Manager Memory](images/task-manager-memory.jpg.jpeg)

## VirtualBox Version
![VirtualBox Version](images/virtualbox-version.jpg.jpeg)

---

# Key Takeaways

- Hyper-V and VirtualBox cannot share hardware virtualization extensions simultaneously.
- Windows security features (VBS / Memory Integrity) can silently enable Hyper-V.
- BIOS virtualization must be enabled before troubleshooting OS-level settings.
- Structured troubleshooting prevents unnecessary OS reinstallation.
- Understanding hypervisor conflicts is critical for enterprise environments.

---

## Skills Demonstrated

- Virtualization troubleshooting
- Hypervisor conflict resolution
- BIOS/UEFI configuration
- Windows Feature management
- System-level diagnostics
- Root cause analysis
