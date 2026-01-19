# Fedora Linux User, Disk and Samba Management

A hands-on system administration project demonstrating user management,
disk partitioning, and Samba-based file sharing on Fedora Linux.

## Purpose
This project demonstrates fundamental Linux system administration tasks on Fedora Linux. 
It covers secure remote access, user and privilege management, disk partitioning and mounting, 
and Samba-based file sharing integrated with firewall and SELinux configurations. 
The project is designed as a hands-on portfolio for system administration roles.
## Environment
- Operating System: Fedora Linux 43
- Deployment: Virtual Machine
- Access Method: SSH (PuTTY from Windows host)
- Host OS: Windows
- User Context: Initial setup performed as root, subsequent tasks executed with a sudo-enabled user
## Initial Setup (Root SSH & PuTTY)
<img width="1184" height="542" alt="image" src="https://github.com/user-attachments/assets/e6ee97f1-5c64-4b79-b4f6-40c547f211f5" />
```console
# Verify SSH service status
$ systemctl status sshd   
#The output confirms that the SSH service is active and running.
<img width="562" height="158" alt="image" src="https://github.com/user-attachments/assets/f9c81ac6-35cd-4b4d-89dc-d065abb7b2c7" />
<p>```bash</p>
<p># The PermitRootLogin directive was reviewed in the SSH configuration file to verify root access settings.</p>
<p>vi /etc/ssh/sshd_config</p>
<img width="1655" height="916" alt="image" src="https://github.com/user-attachments/assets/fb195fdc-27a3-441a-a431-80dfaa6ae0a5" />
<img width="1656" height="922" alt="image" src="https://github.com/user-attachments/assets/6542ab7d-126c-4d52-a446-70202d187062" />
<img width="820" height="274" alt="image" src="https://github.com/user-attachments/assets/93b8d489-70e8-46eb-a38b-726e2ed72b08" />
<p>```bash</p>
<p># By changing the PermitRootLogin setting from prohibit-password to yes in vi insert mode, root login via SSH is now permitted.</p>
<img width="377" height="128" alt="image" src="https://github.com/user-attachments/assets/a9d32ef1-6718-4494-bd65-1d738ae97e94" />
<p>```bash</p>
<p>#By executing systemctl reload sshd, the SSH daemon reads the updated configuration without stopping the service, making the changes effective immediately.</p>
<p>systemctl reload sshd</p>
<img width="656" height="415" alt="image" src="https://github.com/user-attachments/assets/dd073478-2e00-4b85-9ae7-7c74cfcb718e" />
## User Management
## Disk and Partition Management
## Mount Configuration
## Samba Installation and File Sharing
## Firewall, SELinux and Service Verification
## Windows Client Access
## Conclusion
