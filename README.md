# networkwalks-B083-week1-Cybersecurity-lab-setup
🔐 Cybersecurity Lab Environment Setup
Building an isolated virtual lab with VirtualBox and Kali Linux for cybersecurity and ethical hacking practice
![Skill](https://img.shields.io/badge/Skill-Cybersecurity-red?style=for-the-badge)
![VirtualBox](https://img.shields.io/badge/Ver-VirtualBox%207.x-blue?style=for-the-badge&logo=virtualbox&logoColor=white)
![Kali Linux](https://img.shields.io/badge/Kali%20Linux-v2026.2-557C94?style=for-the-badge&logo=kalilinux&logoColor=white)
![Skill](https://img.shields.io/badge/Skill-Virtualization-orange?style=for-the-badge)
![Skill](https://img.shields.io/badge/Skill-Linux-yellow?style=for-the-badge&logo=linux&logoColor=black)
![Topic](https://img.shields.io/badge/Ethical-Hacking-darkred?style=for-the-badge)
![Internship](https://img.shields.io/badge/Internship-Week%201-success?style=for-the-badge)
</div>
---
📌 Project Overview
This project documents the setup of a safe, isolated virtual lab for cybersecurity practice. Kali Linux (v2026.2) runs as a guest machine inside Oracle VirtualBox on a Windows host, so security tools can be tested without touching the host system.
This is my Week 1 task for the cybersecurity internship. Besides the setup itself, this repository records the real problems I ran into (folder permissions, a VM that aborted, and network settings) and how I solved them.
🎯 Objectives
Install and configure VirtualBox on the host machine
Import and run the Kali Linux virtual machine
Allocate suitable resources (RAM, CPU, video memory)
Configure networking so the VM can reach the internet
Verify the lab and troubleshoot any problems
Document the whole process on GitHub
🧰 Tools & Environment
Component	Details
Host OS	Windows 11
Hypervisor	Oracle VirtualBox 7.x
Guest OS	Kali Linux 2026.2 (amd64, pre-built VirtualBox image)
RAM	2048 MB
Processors	2 CPU cores
Video Memory / Controller	128 MB / VMSVGA
Acceleration	Nested Paging, PAE/NX, KVM Paravirtualization
Network Adapter	Adapter 1, NAT (Intel PRO/1000 MT Desktop)
VM Location	`D:\Kali\kali-linux-2026.2-virtualbox-amd64`



🏗️ Lab Architecture
```
┌───────────────────────────────────────────────┐
│               Windows 11 (Host)               │
│                                               │
│   ┌───────────────────────────────────────┐   │
│   │          Oracle VirtualBox            │   │
│   │                                       │   │
│   │   ┌───────────────────────────────┐   │   │
│   │   │  Kali Linux 2026.2 (Guest VM) │   │   │
│   │   │  2 CPU | 2048 MB RAM | NAT    │   │   │
│   │   └───────────────────────────────┘   │   │
│   └───────────────────────────────────────┘   │
└───────────────────────┬───────────────────────┘
                        │ NAT
                     Internet
```
⚙️ Setup Steps
1. Install VirtualBox
Downloaded and installed Oracle VirtualBox from the official website on the Windows host.
2. Download and extract Kali Linux
Downloaded the pre-built VirtualBox image of Kali Linux from the official Kali website (https://www.kali.org/get-kali/) and extracted it to `D:\Kali`.
3. Add the VM to VirtualBox
In VirtualBox Manager: Machine → Add (or File → Open) and select the `.vbox` file inside the extracted folder.
4. Configure VM settings
Opened Settings for the VM and configured:
System → Motherboard: Base memory `2048 MB`, chipset `PIIX3`, I/O APIC enabled
System → Processor: `2` CPUs
System → Acceleration: Hardware virtualization with Nested Paging
Network → Adapter 1: Enabled, attached to NAT
5. Start the VM and log in
Started the machine from VirtualBox Manager. The pre-built image uses the default credentials `kali / kali`, which should be changed after the first login:
```bash
passwd
```
6. Update the system
```bash
sudo apt update && sudo apt upgrade -y
```
7. Optional: static IP configuration
Using Network icon → Edit Connections → Wired connection 1 → IPv4 Settings (Method: Manual):
Field	Value
Address	`10.0.0.2`
Netmask	`24`
Gateway	`10.0.0.1`
DNS	`8.8.8.8` (use `10.0.0.1` if internet gives issues)
✅ Verification
Ran the following inside Kali to confirm everything works:
```bash
whoami              # current user
uname -a            # kernel and architecture
ip a                # network interfaces and IP address
ping -c 4 8.8.8.8   # internet connectivity
ping -c 4 google.com  # DNS resolution
```
[x] Kali Linux boots successfully in VirtualBox
[x] Resources allocated correctly
[x] Network adapter connected
[x] System updated
🛠️ Troubleshooting: Issues Faced
❌ Issue 1: "Access Denied" on the VM folder
Problem: Opening the VM folder's Properties showed "You will need to provide administrator permission to change these attributes." The Users group only had Read & execute, List folder contents and Read, with no Write or Modify.
Cause: The extracted VM folder on drive `D:` had restricted permissions, so VirtualBox could not write to its own VM files.
Solution: Opened Properties → Security → Edit, selected the Users group and allowed Modify / Full control, then applied the changes with administrator approval.
❌ Issue 2: VM state showed "Aborted"
Problem: In VirtualBox Manager the VM appeared as Aborted and would not start normally.
Cause: The machine could not access or write its files properly (see Issue 1), so the session ended unexpectedly.
Solution: After fixing the folder permissions, I discarded the saved/aborted state and started the VM again from VirtualBox Manager.
❌ Issue 3: Network settings not displaying / greyed out
Problem: Network adapter options were greyed out and the network settings were not showing as expected.
Cause: Most adapter settings cannot be edited while the VM is running.
Solution: Powered off the VM completely, changed the network settings, and started it again. Adapter 1 was set to NAT with the virtual cable connected.
📸 Screenshots
#	Description	Screenshot
1	Kali Linux running inside VirtualBox	![Kali running](1-screenshot-kali-running.png)
2	VirtualBox network settings (Adapter 1, NAT)	![Network settings](2-screenshot-network-settings.png)
3	VM showing "Aborted" state	![VM aborted](3-screenshot-vm-aborted.png)
4	"Access Denied" administrator prompt	![Access denied](4-screenshot-access-denied.png)
5	Folder Security permissions	![Permissions](5-screenshot-folder-permissions.png)
📚 Key Learnings
How virtualization lets me run a full penetration-testing OS safely inside another OS
How to allocate CPU, RAM and video memory to a VM
The difference between VirtualBox network modes, and why NAT is a safe default
How Windows folder permissions can break a VM, and how to fix them
A systematic troubleshooting approach: read the error, find the cause, fix it, verify
📁 Repository Structure
```
├── 1-screenshot-kali-running.png
├── 2-screenshot-network-settings.png
├── 3-screenshot-vm-aborted.png
├── 4-screenshot-access-denied.png
├── 5-screenshot-folder-permissions.png
└── README.md
```
👤 Author
Manahil Aamir
Cybersecurity Intern | Week 1: Lab Setup
---
<div align="center">
⭐ If you found this helpful, feel free to star the repository.

How to troubleshoot VM installation and boot problems.
[Add your own learning here]
