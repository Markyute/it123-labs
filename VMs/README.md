# Virtual Machines

This folder documents the VMs used for IT 123 labs. Actual VM files (.vdi, .vbox)
are stored locally in VirtualBox and are not included in this repository since
they're several GB each and don't belong in Git.

## Ubuntu_Server
- OS: Ubuntu Server 22.04.5 LTS
- RAM: 2048 MB | CPU: 2 cores | Storage: 30 GB (VDI, dynamic)
- Network: NAT, IPv4 10.0.2.15
- Created: Week 2
- Users: adminuser (admin), student2, faculty2, student4
- Groups: labusers, facultygrp, studentgrp
- Snapshot: "Clean Install – Ubuntu Server"

## Windows_Server
- OS: Windows Server 2022 Standard Evaluation (Desktop Experience)
- RAM: 4096 MB | CPU: 2 cores | Storage: 50 GB (VDI, dynamic)
- Network: NAT, IPv4 10.0.2.15
- Created: Week 2 (installed after Week 3 was already underway)
- Users: Administrator
- Snapshot: "Clean Install – Windows Server"

Note: I picked the Desktop Experience edition (not Server Core) specifically
because Week 3's user/group management tasks require Server Manager and
Computer Management, which need a GUI.
