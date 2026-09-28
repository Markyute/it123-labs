# Week 7 – Configuring and Securing Network Services

**Course:** IT 123
**Activity:** Lab Performance 2 (Fourth Graded Assessment)
**Server:** Ubuntu Server VM, static IP `10.163.157.150/24`

## Overview
In this lab we configured DNS, DHCP, HTTP, and FTP on our Ubuntu Server, secured them
with UFW, and completed the Part 6 student exercise. Our server uses `10.163.157.150`,
so we used this address wherever the lab guide shows `192.168.1.150`
(DHCP range `10.163.157.160 – 10.163.157.170`).

## What we did

| Part | Service | What we configured | Result |
|---|---|---|---|
| 1 | DNS (BIND9) | Zone `example.local` | `www.example.local` resolves to `10.163.157.150` |
| 2 | DHCP | Range `10.163.157.160 – .170` on `enp0s3` | `isc-dhcp-server` active (running) |
| 3 | HTTP (Apache2) | Installed and tested from the host browser | Default Apache page loads |
| 4 | FTP (vsftpd) | `write_enable=YES` | FTP login successful |
| 5 | Security | `listen_address=10.163.157.150`, UFW rules for 22, 53, 80, 21 | Firewall active; FTP login tested again after `listen_address` |
| 6 | Student exercise | `company.local` zone, custom Apache page, FTP for LAN only | All tasks completed |

## Part 6 – Student exercise
1. **DNS:** `www.company.local` resolves to `10.163.157.150`.
2. **DHCP:** range `10.163.157.160 – 10.163.157.170` is set in `dhcpd.conf`.
3. **Apache:** the default `index.html` was backed up and replaced with
   "Welcome to Company Intranet – Server IP: 10.163.157.150".
4. **FTP:** vsftpd listens only on the server's LAN IP (`listen_address=10.163.157.150`).
   After restarting vsftpd, we logged in again over `ftp 10.163.157.150` and ran `ls` successfully.

## Note
`db.local` was not available on our BIND9 install (`cp` failed, see
`part1_dns_bind9/06_cp_db_local_not_found.png`), so we created `db.example.local` directly.

## Folder contents
```
Week7/
├── README.md
├── configs/        # config files (some are excerpts of the lines we changed)
└── screenshots/    # part1_dns_bind9 … part6_student_exercise, in step order
```
