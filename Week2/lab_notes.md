\# IT 123 - Week 2 Laboratory Report

\## Installing and Configuring Windows \& Linux Virtual Machines in VirtualBox



\*\*Student:\*\* John Mark C. Idanan \& Catlyn L. Ruiz



\## Note on Scope

Windows Server VM installation was not completed for this submission. 

Only Part 2 (Ubuntu Server) and Part 3 (Organization/GitHub) were completed.



\## Part 2 - Ubuntu Server VM



\### VM Configuration

\- VM Name: Ubuntu\_Server

\- OS Type: Linux / Ubuntu 22.04 LTS (Jammy Jellyfish), 64-bit

\- RAM: 2048 MB

\- CPU: 2 cores

\- Storage: 30 GB, VDI, Dynamically Allocated

\- ISO Used: ubuntu-22.04.5-live-server-amd64.iso

\- Network Adapter: NAT (Intel PRO/1000 MT Desktop)



\### Installation Steps

1\. Created new VM in VirtualBox, selected Linux/Ubuntu 22.04 LTS (64-bit).

2\. Attached Ubuntu 22.04.5 Server ISO.

3\. Allocated 2048 MB RAM and 2 CPU cores.

4\. Created a 30 GB VDI dynamically allocated virtual hard disk.

5\. Booted VM and ran through Ubuntu Server (subiquity) installer:

&#x20;  - Language: English

&#x20;  - Keyboard: English (US)

&#x20;  - Installation base: Ubuntu Server (default, not minimized)

&#x20;  - Network: auto-configured via DHCP (10.0.2.15)

&#x20;  - Storage: used entire disk (LVM disabled), ext4 filesystem

&#x20;  - Profile setup: 

&#x20;    - Name: John Mark

&#x20;    - Server name: ubuntu-server

&#x20;    - Username: adminuser 

&#x20;      (Note: username "admin" is reserved by Ubuntu Server and could not be used; 

&#x20;      "adminuser" was used instead)

&#x20;    - Password: P@ssw0rd123

&#x20;  - Ubuntu Pro: skipped

&#x20;  - SSH Setup: Installed OpenSSH Server, allowed password authentication

&#x20;  - Featured Server Snaps: none selected

6\. Installation completed, rebooted successfully.

7\. Logged in as adminuser at the login prompt.

8\. Verified network connectivity (IPv4: 10.0.2.15).

9\. Verified SSH service is active and running on port 22 

&#x20;  (confirmed via `sudo systemctl status ssh`).

10\. Took snapshot named "Clean Install – Ubuntu Server".



\## Part 3 - Organization and GitHub

\- Created GitHub repository: it123-labs

\- Cloned repository locally

\- Created folder structure:

&#x20; - it123-labs/VMs/

&#x20; - it123-labs/Week2/

\- Added lab notes (this file) and screenshots to Week2/

\- Committed and pushed changes to GitHub



\## Summary of VM Configuration

| Setting  | Value                          |

|----------|--------------------------------|

| RAM      | 2048 MB                        |

| CPU      | 2 cores                        |

| Storage  | 30 GB (VDI, dynamic)           |

| Network  | NAT, IPv4 10.0.2.15            |

| OS       | Ubuntu Server 22.04.5 LTS      |

