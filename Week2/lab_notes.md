# IT 123 - Week 2 Lab Notes
## Installing and Configuring Windows & Linux Virtual Machines in VirtualBox

**Student:** John Mark C. Idanan & Catlyn L. Ruiz

## Part 1 - Windows Server VM

I created a new VM named Windows_Server, set to Microsoft Windows / Windows
Server 2022 (64-bit), and attached the evaluation ISO downloaded from
Microsoft's Evaluation Center.

Settings I used:
- RAM: 4096 MB
- CPU: 2 cores
- Disk: 50 GB, VDI, dynamically allocated

During installation, I had to pick between "Standard Evaluation" and "Standard
Evaluation (Desktop Experience)" — I went with the Desktop Experience version
since I knew Week 3's tasks needed Server Manager and Computer Management,
which require a GUI. The plain "Standard Evaluation" option is a GUI-less
Server Core install, which wouldn't work for that.

Like with Ubuntu, I made sure to uncheck "Proceed with Unattended
Installation" so I could walk through the installer manually.

The install itself was mostly automatic (choose language, accept license,
custom install, select the disk), then it asked me to set a password for the
built-in Administrator account — same situation as Ubuntu rejecting "admin,"
Windows Server also uses a fixed "Administrator" username you can't change at
setup.

After it booted into the desktop, I confirmed networking was working via
`ipconfig` in Command Prompt — got 10.0.2.15 on NAT, same subnet as my Ubuntu
VM. Took a snapshot named "Clean Install – Windows Server" afterward.

## Part 2 - Ubuntu Server VM

I created a new VM in VirtualBox and named it Ubuntu_Server. It auto-detected
Linux/Ubuntu as the type once I typed the name, which was convenient.

For the ISO, I first grabbed the wrong one — I accidentally downloaded Ubuntu
Desktop instead of Server, and it also wasn't the 22.04 version the guide asked
for (Ubuntu had already moved on to 26.04 as their latest LTS by the time I was
doing this). Had to go back to ubuntu.com/download/server, click into "Previous
releases," and grab the actual 22.04.5 LTS server ISO to match the lab guide.

I also had "Proceed with Unattended Installation" checked by default in the new
VirtualBox wizard, which I had to uncheck — otherwise it installs everything
automatically in the background and you never get to see or interact with the
installer screens, which defeats the point of the exercise.

Settings I used:
- RAM: 2048 MB
- CPU: 2 cores
- Disk: 30 GB, VDI, dynamically allocated (not pre-allocated)

### Installing Ubuntu Server

Went through the text-based installer (no mouse, all keyboard). A few notes:
- Picked English for language and keyboard, left defaults for most screens.
- For storage, I used "entire disk" but had to manually uncheck "Set up this
  disk as an LVM group" since I didn't need that complexity.
- When I got to picking a username, I tried "admin" like the guide says, but
  Ubuntu rejected it — turns out "admin" is a reserved system username on
  Ubuntu Server and can't be used. I went with "adminuser" instead.
- Made sure to check "Install OpenSSH server" during setup since later labs
  would probably need SSH access.
- Skipped Ubuntu Pro and all the optional server snaps (Kubernetes, Nextcloud,
  etc.) — none of that was needed here.

Installation took a while, mostly waiting on the "downloading and installing
security updates" step. After reboot I logged in as adminuser and confirmed
things worked with a few terminal commands: 
whoami -> adminuser
hostname -> ubuntu-server
ip addr -> got 10.0.2.15 on enp0s3 (NAT)

Also checked that SSH was actually running:
sudo systemctl status ssh
Came back "active (running)" on port 22, so that's confirmed working.

Took a snapshot afterward named "Clean Install – Ubuntu Server" so I have a
clean rollback point before I mess anything up in later labs.

## Organizing and GitHub

Realized partway through that I never actually had the it123-labs repo set up
from Week 1, so I created it fresh on GitHub, cloned it locally into
Documents\it123-labs, and made the VMs/ and Week2/ folders.

Wrote these notes and copied over the screenshots I took along the way, then
pushed everything with:
git add .
git commit -m "Week 2 - Windows and Ubuntu Server installation"
git push origin main


Went through fine on the first try. Also discovered Git Bash gives a much
nicer terminal than plain cmd (shows the current branch right in the prompt),
so I'll probably switch to using that going forward.

## VM Configuration Summary

| Setting  | Windows_Server                    | Ubuntu_Server                |
|----------|------------------------------------|-------------------------------|
| RAM      | 4096 MB                            | 2048 MB                       |
| CPU      | 2 cores                            | 2 cores                       |
| Storage  | 50 GB (VDI, dynamic)                | 30 GB (VDI, dynamic)          |
| Network  | NAT, IPv4 10.0.2.15                 | NAT, IPv4 10.0.2.15            |
| OS       | Windows Server 2022 Standard Eval   | Ubuntu Server 22.04.5 LTS      |
| Extra    | Desktop Experience (GUI)            | OpenSSH, active on port 22     |

## Reflection

The username thing threw me off for a second since I didn't expect the Ubuntu
installer to reject a value straight from the guide. Also spent more time than
I expected just figuring out which Ubuntu ISO to actually download, since the
"current" version has moved past what the lab was written for. The Windows
Server edition choice (Desktop Experience vs Server Core) was another decision
point I had to think through, since the guide doesn't spell that part out.
Still, once I got through both installs, this made a lot more sense than I
expected — I'd used VirtualBox before, so a lot of the concepts (RAM/CPU
allocation, virtual disks) weren't new, just applying them to server installs
instead of a desktop one this time.
