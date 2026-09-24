# networkwalks-B083-week1-Cybersecurity-lab-setup
CyberSecurity Lab setup
Week 1: Kali Linux Virtual Machine Setup
Objective

Set up Kali Linux inside a virtual machine so I have a safe, isolated environment for cybersecurity practice during my internship.

Environment
Item	Details
Host OS	[e.g., Windows 11]
Virtualization software	[VirtualBox / VMware Workstation]
Kali Linux version	[e.g., 2025.x, installer or pre-built VM image]
RAM allocated	[e.g., 4 GB]
CPU cores	[e.g., 2]
Disk size	[e.g., 40 GB]
Setup Steps
Downloaded the tools
Installed [VirtualBox / VMware] on the host machine.
Downloaded the Kali Linux image from the official site: https://www.kali.org/get-kali/
Created the virtual machine
Created a new VM (Type: Linux, Version: Debian 64-bit).
Allocated RAM, CPU cores, and disk space as listed above.
Installed / imported Kali
[Mounted the ISO and ran the graphical installer / Imported the pre-built .ova or .vmdk image].
First boot and configuration
Logged in and updated the system:
bash
     sudo apt update && sudo apt upgrade -y
Verified the installation:
bash
     whoami
     uname -a
Issues Faced and How I Solved Them
Issue 1: [Short title, e.g., "VM would not boot / 64-bit option missing"]
Problem: [What happened]
Cause: [Why it happened, e.g., virtualization (VT-x / SVM) disabled in BIOS]
Solution: [What fixed it, e.g., enabled virtualization in BIOS settings]
Key Learnings
How virtualization works and why it is used for security testing.
How to allocate VM resources (RAM, CPU, disk) properly.
How to troubleshoot VM installation and boot problems.
[Add your own learning here]
