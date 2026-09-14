# Week 5 Notes – System Initialization and Service Management

**Names:** John Mark Idanan & Catlyn Ruiz

**Course, Year and Section:** BSIT-4A


This file lists the commands we used during the Week 5 lab (Ubuntu Server only, per instructor's instructions), along with a short explanation of what each command does and why we used it.

---

## Part 1 – Exploring the Boot Process

| Command | Explanation |
|---|---|
| `systemctl get-default` | Shows the current default systemd target (boot target) the system boots into. The output showed `multi-user.target`, which is the correct target for Ubuntu Server since it has no GUI. |
| `systemctl list-units --type=target` | Lists all currently loaded and active target units, showing which stages of the boot process (networking, local file systems, multi-user, graphical, etc.) are active. |
| `sudo systemctl isolate rescue.target` | Switches the system to rescue mode (single-user maintenance mode), which loads a minimal set of services for troubleshooting. |
| `systemctl isolate multi-user.target` | Returns the system from rescue mode back to the normal multi-user (CLI) mode. |

---

## Part 2 – Service Management

| Command | Explanation |
|---|---|
| `systemctl list-units --type=service --state=running` | Lists all services that are currently active and running on the system. |
| `systemctl status ssh` | Displays detailed status information about the SSH service, including whether it is active, when it last started, and recent log entries. |
| `sudo systemctl start ssh` | Starts the SSH service if it is not already running. |
| `sudo systemctl stop ssh` | Stops the SSH service. |
| `sudo systemctl restart ssh` | Stops and then immediately starts the SSH service again, useful after a configuration change. |
| `sudo systemctl enable ssh` | Configures the SSH service to start automatically every time the system boots. |
| `sudo systemctl disable ssh` | Prevents the SSH service from starting automatically at boot (it can still be started manually). |
| `systemctl is-enabled ssh` | Checks and reports whether the SSH service is currently set to start at boot (`enabled` or `disabled`). |

---

## Part 3 – Troubleshooting Services

| Command | Explanation |
|---|---|
| `sudo systemctl stop ssh` | Used to simulate a failed/stopped service for troubleshooting practice. |
| `systemctl status ssh` | Confirms the service is stopped by showing `Active: inactive (dead)`. |
| `journalctl -u ssh --since "5 minutes ago"` | Displays the system log entries specifically related to the SSH service from the last 5 minutes, useful for diagnosing why a service failed or stopped. |
| `sudo systemctl start ssh` | Restarts the service to resolve the simulated failure. |

---

## Part 5 – Student Exercise (Apache2 and vsftpd)

**Scenario:** Apache2 (web server) must always be available after boot, while vsftpd (FTP server) should only run when needed and not start automatically.

| Command | Explanation |
|---|---|
| `sudo apt update` | Refreshes the local package index so the system knows the latest available versions of packages before installing anything. |
| `sudo apt install apache2 vsftpd -y` | Installs both the Apache2 web server and the vsftpd FTP server in one command. By default, Ubuntu's package manager automatically enables services that ship with a systemd unit, which is why apache2 was already linked to `multi-user.target.wants` right after installation. |
| `dpkg -l \| grep -E "apache2\|vsftpd"` | Confirms that both apache2 and vsftpd packages were successfully installed by listing their installed status. |
| `sudo systemctl enable apache2` | Explicitly ensures apache2 is set to start automatically at every boot. |
| `sudo systemctl disable vsftpd` | Removes vsftpd from automatic startup, so it will not run unless started manually. This matches the requirement that vsftpd should only run when needed. |
| `sudo reboot` | Restarts the VM to confirm that the enable/disable settings persist after a real reboot, not just in the current session. |
| `systemctl is-enabled apache2` | Verifies that apache2 is still set to `enabled` after reboot — confirming it will always start automatically. |
| `systemctl is-enabled vsftpd` | Verifies that vsftpd is still set to `disabled` after reboot — confirming it will not start automatically, but can still be started manually with `sudo systemctl start vsftpd` when needed. |

**Result:** After rebooting, `systemctl is-enabled apache2` returned `enabled`, and `systemctl is-enabled vsftpd` returned `disabled`, confirming the configuration met the scenario's requirements.

---

## Summary

This lab helped us understand how systemd organizes the Linux boot process into targets (replacing the older runlevel system), and gave us practice managing services using `systemctl` (start, stop, restart, enable, disable, and check status), as well as troubleshooting a stopped service using `journalctl` logs. In the student exercise, we applied these skills to a practical scenario where one service needed to always run at boot (apache2) while another needed to remain off unless we started it manually (vsftpd).
