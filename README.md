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
<pre><code># Verify SSH service status
systemctl status sshd 
#The output confirms that the SSH service is active and running.</code></pre>
<img width="562" height="158" alt="image" src="https://github.com/user-attachments/assets/f9c81ac6-35cd-4b4d-89dc-d065abb7b2c7" />
<pre><code># The PermitRootLogin directive was reviewed in the SSH configuration file to verify root access settings.
vi /etc/ssh/sshd_config</code></pre>
<img width="1655" height="916" alt="image" src="https://github.com/user-attachments/assets/fb195fdc-27a3-441a-a431-80dfaa6ae0a5" />
<img width="1656" height="922" alt="image" src="https://github.com/user-attachments/assets/6542ab7d-126c-4d52-a446-70202d187062" />
<img width="820" height="274" alt="image" src="https://github.com/user-attachments/assets/93b8d489-70e8-46eb-a38b-726e2ed72b08" />
<pre><code># By changing the PermitRootLogin setting from prohibit-password to yes in vi insert mode, root login via SSH is now permitted.</code></pre>
<img width="377" height="128" alt="image" src="https://github.com/user-attachments/assets/a9d32ef1-6718-4494-bd65-1d738ae97e94" />
<pre><code>#By executing systemctl reload sshd, the SSH daemon reads the updated configuration without stopping the service, making the changes effective immediately.
systemctl reload sshd</code></pre>
<img width="656" height="415" alt="image" src="https://github.com/user-attachments/assets/dd073478-2e00-4b85-9ae7-7c74cfcb718e" />
<pre><code>#SSH access is provided via the PuTTY terminal.</code></pre>

## User Management
<img width="383" height="96" alt="image" src="https://github.com/user-attachments/assets/82289dce-9cf4-429c-b545-a8801e1a7b57" />
<pre><code>useradd -m user1
useradd -m user2
useradd -m user3
useradd -m user4
#New user accounts were created on the system using the useradd -m (username) command, which also creates home directories for each user.</code></pre>
  
<img width="629" height="363" alt="image" src="https://github.com/user-attachments/assets/a2279397-8af4-45c6-a325-75f467e7ee1e" />
<pre><code>passwd user1
passwd user2
passwd user3
passwd user4
#The passwd (username) command is used to set or change the password of a specified user.
#The ‘Bad password’ warning was received because the assigned password contained fewer than eight characters. Although this is acceptable in a laboratory environment, it is essential to enforce strong password policies with complex and sufficiently long passwords in production systems to ensure security.</code></pre>
<img width="777" height="650" alt="image" src="https://github.com/user-attachments/assets/f11416cb-00f2-4836-b130-3641335528eb" />
<pre><code>ls /home
#The ls /home command was used to verify whether the home directories of the created users were successfully generated. The output confirms that all users have their respective home directories.
cat /etc/passwd
#The cat /etc/passwd command was used to verify that the user information was successfully created in the /etc/passwd file. By examining the last four lines of the output, the details of the newly created users can be observed.</code></pre>
<img width="450" height="144" alt="image" src="https://github.com/user-attachments/assets/d3d26800-7d77-4882-bbb8-b1a4483e7dbe" />
<pre><code>groupadd family 
#The groupadd family command was used to create a group named family.
gpasswd -a user1 family
gpasswd -a user2 family
gpasswd -a user3 family
#Using the gpasswd -a (username) (groupname) command, the users user1, user2, and user3 were added to the family group.</code></pre>
<img width="418" height="130" alt="image" src="https://github.com/user-attachments/assets/d1dd50c1-07c9-4cbb-af86-c9c34af0aef7" />
<pre><code>cat /etc/group | tail -n 1
#The cat /etc/group | tail -n 1 command was executed to display the last line of the /etc/group file. The output shows the name of the most recently created group along with its member information and related details.</code></pre>
<img width="841" height="467" alt="image" src="https://github.com/user-attachments/assets/0c9a5206-35ee-4adf-b9f9-66208ecacb22" />
<pre><code>cat /etc/sudoers | tail -n 20
touch /etc/sudoers.d/user1
visudo /etc/sudoers.d/user1
#The cat /etc/sudoers | tail -n 20 command was used to display the last 20 lines of the /etc/sudoers file, which defines sudo privileges for users and groups on the system. Although sudo permissions can be configured directly in this file, modifying it is not recommended due to the risk of configuration errors.

#Instead, the preferred and safer approach is to define sudo rules by creating a configuration file under the /etc/sudoers.d/ directory, as the sudo mechanism also reads and applies rules from this location. In this setup, sudo privileges will be explicitly granted to the user1 account by defining a dedicated rule in the /etc/sudoers.d/ directory, without relying on group-based privilege assignment.
#To assign sudo privileges to user1, a configuration file named user1 was created under the /etc/sudoers.d/ directory.
#The file for defining sudo privileges for user1 was opened using the visudo /etc/sudoers.d/user1 command. Sudo configuration files are edited with the visudo utility rather than a standard text editor, as visudo performs syntax validation to prevent configuration errors.</code></pre>
<img width="338" height="164" alt="image" src="https://github.com/user-attachments/assets/cb8dbfd6-49ed-4e64-8bbc-10fdbff6074d" />
<pre><code>user1 ALL=(ALL)   ALL
#The rule user1 ALL=(ALL) ALL grants the user1 account permission to execute any command on any host as any user using sudo.
</code></pre>
<img width="600" height="387" alt="image" src="https://github.com/user-attachments/assets/9b9d3045-e0fd-4d3b-838d-07d8fc1168d5" />
<pre><code>su - user1
#Using the su - user1 command, the active session was changed from the root account to the user1 user, loading the user’s login environment.
sudo hostnamectl hostname fedora43
#Using sudo privileges, the user1 account changed the system hostname from localhost to fedora43.
hostname
#The output of the hostname command displays fedora43, confirming that the hostname change was successfully applied.</code></pre>
<img width="356" height="113" alt="image" src="https://github.com/user-attachments/assets/84b9324e-df68-44ef-8eeb-f2f7ea46e536" />
<img width="799" height="596" alt="image" src="https://github.com/user-attachments/assets/6ff320b7-a3d3-43cc-9842-5c8ac48c6431" />
<img width="783" height="661" alt="image" src="https://github.com/user-attachments/assets/d4c05e6a-a71b-48b5-b669-c923cbf492ef" />
<pre><code>sudo vi /etc/passwd</code></pre>
<pre>root:x:0:0:Super User:/root:/bin/bash-------> root:x:0:0:Super User:/root:/usr/sbin/nologin</pre>
<pre>#By changing the root user’s login shell from /bin/bash to /usr/sbin/nologin, the root account was prevented from logging in directly. This provides an additional layer of security, as the root account has extensive privileges and could be used to perform critical system modifications if compromised.</pre>
<img width="344" height="165" alt="image" src="https://github.com/user-attachments/assets/bdbba20b-0828-485c-93c3-1d93a2c35766" />
<pre><code>su - root
#When the su - root command was executed, the message ‘This account is currently not available’ was displayed because direct login for the root account had been disabled. This confirms that the intended security measure was successfully applied.</code></pre>
<img width="349" height="151" alt="image" src="https://github.com/user-attachments/assets/1b4315db-6217-43c6-aa17-47fb511c2fd8" />
<pre><code>sudo shutdown now
#The system was shut down using the sudo shutdown now command in preparation for adding a new disk.
</code></pre>



## Disk and Partition Management
<img width="1655" height="951" alt="image" src="https://github.com/user-attachments/assets/59189302-490c-4df4-89b9-6fcb6dd143f0" /><br><br>

<img width="757" height="732" alt="image" src="https://github.com/user-attachments/assets/edd216cc-1875-4acc-aa9e-09bc76038e5e" /><br><br>

<img width="434" height="430" alt="image" src="https://github.com/user-attachments/assets/e9198bcb-3e8e-4610-9c26-ebd4ccf6975e" /><br><br>

<img width="435" height="423" alt="image" src="https://github.com/user-attachments/assets/1d83a900-0919-473d-b7d8-566f277fcb87" /><br><br>

<img width="442" height="425" alt="image" src="https://github.com/user-attachments/assets/c63ad50e-2fa2-4275-85f4-d24cc684fd95" /><br><br>

<img width="438" height="424" alt="image" src="https://github.com/user-attachments/assets/43ae2222-626b-4783-af40-c65837cc1988" /><br><br>

<img width="442" height="425" alt="image" src="https://github.com/user-attachments/assets/2b50761c-8f64-40fa-a922-c6fd7545574c" /><br><br>

<img width="753" height="729" alt="image" src="https://github.com/user-attachments/assets/d0b08823-7725-4399-a83b-a86a6d5bf2a8" /><br><br>

Before adding a new disk, the virtual machine was safely powered off using the sudo shutdown now command. After the system was completely shut down, the virtual machine hardware settings were accessed through VMware Workstation.
From the Add Hardware wizard, the Hard Disk option was selected, and the disk type was set to NVMe, as shown in the configuration steps.
Next, the option ‘Create a new virtual disk’ was selected. The disk size was configured as 10 GB according to the project requirements. The option ‘Allocate all disk space now’ was enabled to ensure that the full disk space was reserved immediately.
The disk was configured to be stored as a single file, and the default disk file location was accepted. After completing the setup wizard, the new NVMe disk was successfully added to the virtual machine.
Finally, the virtual machine was powered on again, and the operating system successfully detected the newly added 10 GB NVMe disk, confirming that the disk addition process was completed successfully.

<img width="491" height="294" alt="image" src="https://github.com/user-attachments/assets/54a4ec7a-1d0f-42b2-bf8a-6b781c747cec" />
<pre><code>lsblk
sudo fdisk /dev/nvme0n1
#The lsblk command was used to list the disks available in the system. The nvme0n2 disk contains the operating system partitions, while nvme0n1 is the newly added disk. Since nvme0n1 does not have any partitions, it is not yet ready for use. Therefore, the disk must be partitioned before it can be utilized. To create partitions on the new disk, the sudo fdisk /dev/nvme0n1 command was executed.</code></pre>
<img width="501" height="684" alt="image" src="https://github.com/user-attachments/assets/ebec5f6a-b188-471a-a649-dec48cebfdde" /><br><br>
<img width="784" height="452" alt="image" src="https://github.com/user-attachments/assets/66cb3073-dc3e-4c4c-a54e-b22004efcfc7" /><br><br>
<img width="551" height="239" alt="image" src="https://github.com/user-attachments/assets/f455114a-c11b-4b73-ab7f-1c092f55140c" /><br><br>
<img width="408" height="109" alt="image" src="https://github.com/user-attachments/assets/dbcf0f0b-e87d-45e1-abdc-2e4d89b6b44e" /><br><br>
The command fdisk /dev/nvme0n1 was executed to start the interactive partitioning tool. m option was used to display the help menu.To create a new partition, the n (new) option was selected. Since the disk did not contain any previous partitions, a primary partition was created by accepting the default partition type.
For the first partition, the default starting sector was accepted. This ensures proper alignment with the disk’s sector boundaries and is considered best practice for performance and compatibility. The size of the first partition was defined as 5 GB by specifying the appropriate ending sector.
After creating the first partition, the n option was selected again to create a second primary partition. The default starting sector was accepted once more, allowing the partition to begin immediately after the first partition. The second partition was allocated the remaining 5 GB of the disk space.
Once both partitions were defined, the p option was used to display the current partition table and verify the configuration. Finally, the w option was selected to write the partition table to the disk and permanently save the changes.
<img width="1048" height="865" alt="image" src="https://github.com/user-attachments/assets/2e583b8b-b7c4-4f51-84f9-a3c7976fc812" />
<pre><code>lsblk -f
#By running the lsblk -f command, the newly created nvme0n1p1 and nvme0n1p2 partitions, each with a size of 5 GB, can be observed on the nvme0n1 disk. However, unlike the partitions on the nvme0n2 disk, these new partitions do not have UUID values assigned. This is because no filesystem has been created on the new disk partitions yet.
sudo mkfs.ext4 /dev/nvme0n1p1
sudo mkfs.ext4 /dev/nvme0n1p2
#The sudo mkfs.ext4 /dev/nvme0n1p1 and sudo mkfs.ext4 /dev/nvme0n1p2 commands were executed to create an ext4 filesystem on the newly created partitions.After creating the filesystems, the partitions now have UUID values assigned.</code></pre>


## Mount Configuration
<img width="458" height="64" alt="image" src="https://github.com/user-attachments/assets/92f6c55d-c344-4669-9ce5-5cda4c02ced9" />
<pre><code>sudo mkdir /share1
sudo mkdir /home/user1/share2
#The directories /share1 and /home/user1/share2 were created using the mkdir command. These directories are intended to be used as mount points for the newly configured disk partitions and will later be shared via the Samba service.</code></pre>
<img width="1068" height="504" alt="image" src="https://github.com/user-attachments/assets/5b1f1ab6-9465-4d95-a042-cdfb8f9e701b" />
<pre><code>sudo mount /dev/nvme0n1p1 /share1
sudo mount /dev/nvme0n1p2 /home/user1/share2
#The commands sudo mount /dev/nvme0n1p1 /share1 and sudo mount /dev/nvme0n1p2 /home/user1/share2 were used 
to mount the newly created disk partitions to their respective directories. This operation makes the filesystems 
on the partitions accessible through the system’s directory structure and prepares them for further configuration, including network sharing via Samba.</code></pre>
<img width="335" height="87" alt="image" src="https://github.com/user-attachments/assets/662267e6-669c-4203-baf6-75223be0faa9" />
<pre><code>sudo vi /etc/fstab
#In order for the disk configurations to persist after a system reboot, the mounted partitions must be defined in the system disk configuration file,
/etc/fstab. To edit this file, it is opened with the vi text editor using the command sudo vi /etc/fstab</code></pre>
<img width="717" height="399" alt="image" src="https://github.com/user-attachments/assets/a2e05829-15c9-4300-803e-a7fe8b41b4a2" />
<img width="1050" height="1027" alt="image" src="https://github.com/user-attachments/assets/283e585d-55c6-4211-a0e6-fe84fd2c4ed2" />
<pre><code>UUID=29769dae-5fe3-4d6e-a634-eda8f31af3cf /share1 ext4 defaults 0 0
UUID=8215ae91-bb9e-4ad7-8153-6bafe8b908b1  /home/user1/share2 ext4 defaults 0 0
#The above two entries have been manually added to the /etc/fstab configuration file to define the mount points for the newly created disk partitions.
#The /etc/fstab file was edited to ensure that the disk configurations persist after a system reboot. Each entry specifies the mount point (/share1 and /home/user1/share2) and the filesystem type (ext4) of the partition. UUIDs are preferred over device names because they uniquely identify each partition regardless of boot order or the addition of new disks, ensuring reliable mounting. The defaults option applies standard mount parameters such as read/write access, automatic mounting at boot, and user accessibility. The final two fields, dump and fsck, are set to 0 0 to indicate that these partitions should not be included in dump backups and should not undergo automatic filesystem checks during startup, which is suitable for non-critical, data-sharing partitions.</code></pre>

## Samba Installation and File Sharing
<img width="1902" height="775" alt="image" src="https://github.com/user-attachments/assets/560936bf-bb0d-42d5-92d3-a489a29cce86" />
<pre><code>sudo yum install samba
#In order to share our directories using the Samba protocol, the Samba package must be installed on the system.
For the Fedora distribution, the YUM package manager is used to install required software packages.The install command
is used to install a package, and samba specifies the name of the package to be installed. Therefore, the sudo yum install samba
command installs the necessary software to enable directory sharing via the Samba protocol.</code></pre>
<img width="1903" height="913" alt="image" src="https://github.com/user-attachments/assets/7f97f099-363f-4ae6-9e01-c02b51c5ac4d" /><br><br>
In the transaction summary section, the package manager indicates that 13 packages will be upgraded, 13 packages will be removed, and 1 package will be newly installed. This summary provides an overview of the actions required for the system to run the package in its most up-to-date and compatible state.When the system asks whether to proceed with these changes, the operation is confirmed. After approval, detailed information about the installed, removed, and upgraded packages can be viewed during the transaction process.
<img width="485" height="272" alt="image" src="https://github.com/user-attachments/assets/ee7945fe-9516-4438-a922-dfb65755a056" />
<pre><code>sudo passwd -a user1
sudo passwd -a user2
sudo passwd -a user1
#The smbpasswd -a (username) command is used to add a user to the Samba user database.The -a (add) option creates a new Samba account for the specified user.
The (username parameter) refers to an existing local Linux user account that will be enabled for authentication in Samba services.
This command allows the specified user to access shared resources over the Samba (SMB/CIFS) protocol using a Samba-specific password, which may be different from the system login password.</code></pre>
<img width="563" height="303" alt="image" src="https://github.com/user-attachments/assets/7e9c3d72-e1e0-47d8-9d3a-94d925585e1a" />
<pre><code>sudo ls -ld /share1
#With this command, the ownership and permission information of the /share1 directory is displayed.
sudo ls -ld /home/user1/share2
#With this command, the ownership and permission information of the /home/user1/share2 directory is displayed.
sudo chown -R :family /share1
#This command changes the group ownership of /share1 and all its contents to the family group, while keeping the existing owner unchanged.This ensures that only members of the family group can access the directory according to group permissions.The /share1 directory is owned by root, which is not a Samba user. Therefore, owner permissions do not apply to Samba users. Access to the directory will be granted to Samba users (user1, user2, user3) through the family group permissions. Once the Samba configuration is completed, guest access will be disabled for the directory (/share1), so the permissions for 'others' will not be relevant.
sudo chown -R :family /home/user1/share2
#The command sudo chown -R :family /home/user1/share2 changes the group ownership of the directory to family. However, this has no practical effect for this directory because it will be accessed only by guest users. In Linux, guests are mapped to the nobody user, which is not part of any group. Therefore, access permissions are determined by the ‘others’ permissions, not by the group ownership. The group change was done solely to make the ownership settings consistent with the first shared directory (/share1).
sudo chmod 775 /share1
#The command sudo chmod 775 /share1 grants full permissions to the family group. The root user’s permissions are irrelevant for Windows access because root is not a Samba user. Since guest access will be disabled, the only important permissions for this share are the group permissions. Applying the permissions recursively would be more appropriate for accessing subdirectories; however, these permissions will be adjusted again in the Access Client section. During access testing, documents will be downloaded into the system using the wget tool and then moved or copied into the shared directories using the mv and cp commands. Once the documents are placed into the directories, the permissions will be adjusted recursively.
sudo chmod 775 /home/user1/share2
The command sudo chmod 775 /home/user1/share2 changes the directory permissions. Since this directory will be accessed only by guest users, which are mapped to the nobody user, the owner and group of the directory are irrelevant. Only the ‘others’ permissions matter for guest access.Applying the permissions recursively would be more appropriate for accessing subdirectories; however, these permissions will be adjusted again in the Access Client section. During access testing, documents will be downloaded into the system using the wget tool and then moved or copied into the shared directories using the mv and cp commands. Once the documents are placed into the directories, the permissions will be adjusted recursively.
sudo ls -ld /share1
#With this command, the ownership and permission information of the /share1 directory is displayed.
sudo ls -ld /home/user1/share2
#With this command, the ownership and permission information of the /home/user1/share2 directory is displayed.</code></pre>
<img width="463" height="200" alt="image" src="https://github.com/user-attachments/assets/686f5ec6-6fcb-4323-9761-2dabdc79a3b1" />
<pre><code>sudo vi /etc/samba/smb.conf
#This command allows you to open and edit the Samba configuration file as root. Changes made here control Samba shares, user access, permissions, and other server settings.</code></pre>
<img width="727" height="854" alt="image" src="https://github.com/user-attachments/assets/80fd30f7-e549-4b98-865d-43aa92779fdb" />
<img width="838" height="1030" alt="image" src="https://github.com/user-attachments/assets/8616b06c-d69e-4e9e-9cc9-5d79778e3f57" />
<pre><code>[global]
   workgroup = SAMBA
   security = user
   passdb backend = tdbsam

   printing = cups
   printcap name = cups
   load printers = yes
   cups options = raw
   map to guest = Bad User
   #Install samba-usershares package for support
   include = /etc/samba/usershares.conf
   #The map to guest = bad user setting in Samba ensures that users who are not defined as Samba users are automatically mapped to the guest account
[Share1]
   comment = First Share
   #This provides a descriptive label for the share. In this case, the share is labeled “First Share”, which helps users identify it in network browsing.
   path = /share1
   #This specifies the directory on the server that will be shared. Here, /share1 is the folder that users will access through Samba.
   browsable = yes
   #Determines whether the share is visible when browsing the network. With yes, users can see this share in their network browser.
   read only = no
   #Defines the write permissions. Setting no allows users to read and write to this share.
   guest ok = no
   #Specifies whether guest (unauthenticated) access is allowed. no means only authenticated users can access the share.
   valid users = user1 user2 user3
   #Lists the users who are allowed to access this share. Only user1, user2, and user3 can log in and use this share.
   directory mask = 775
   #Sets the permissions for newly created directories inside the share. 775 means:Owner: read/write/execute Group: read/write/execute Others: read/execute
   #Lists the users who are allowed to access this share. Only user1, user2, and user3 can log in and use this share.
   create mask = 775
   #Sets the permissions for newly created files inside the share. 775 ensures files are readable, writable, and executable by owner and group, readable and executable by others.
   force group = family
   #Forces all files and directories created in this share to belong to the family group, regardless of the creating user’s default group.
[Share2]
   comment = Second Share
   #This is a descriptive label for the share. It helps users identify the share in the network browser, here labeled “Second Share”.
   path = /home/user1/share2
   #Specifies the directory on the server that will be shared. In this case, the folder /home/user1/share2 is shared through Samba.
   browsable = yes
   #Determines whether the share is visible when browsing the network. With yes, users can see this share in their network browser.
   read only = no
   #Allows users to read and write to this share. They can create, modify, or delete files and directories.
   guest ok = yes
   #Specifies that guest (unauthenticated) access is allowed. Users can access this share without a valid Samba account.
   guest only = yes
   #Specifies that access to this share is restricted to guest users only; only guest users can access it.
   directory mask = 775
   #Sets the permissions for newly created directories inside the share.Owner: read/write/execute Group: read/write/execute Others: read/execute.
   create mask = 775
   #Sets the permissions for newly created files inside the share. Files are readable, writable, and executable by owner and group, readable and executable by others.</code></pre>



<img width="629" height="237" alt="image" src="https://github.com/user-attachments/assets/0fa17e71-4a64-4c98-8a3a-7852fa042830" />
<pre><code>sudo testparm
#The sudo testparm command is used to check the Samba configuration file for errors and display the effective settings that Samba will apply.</code></pre>




## Firewall, SELinux and Service Verification
<img width="773" height="604" alt="image" src="https://github.com/user-attachments/assets/7edfa737-8f6c-4317-bd4d-f5611a9fd76c" />
<pre><code>sudo systemctl status smb
#The command sudo systemctl status smb is used to check the current status of the Samba (SMB) service on a Linux system. It shows whether the service is running, stopped, or has failed, along with detailed information such as uptime, process ID, and recent log messages. Administrator privileges are required to view the full service status.
sudo systemctl start smb
The command sudo systemctl start smb is used to start the Samba (SMB) service on a Linux system. It activates the service so that file and printer sharing over the network becomes available.Administrator privileges (sudo) are required to start the service.
sudo systemctl status smb
#Checking the current status of the Samba service.</code></pre>
<img width="1176" height="1031" alt="image" src="https://github.com/user-attachments/assets/3130261e-151e-4909-a7c8-10f77f727aa6" />
<pre><code>firewall-cmd --get-zones
firewall-cmd --get-default-zone
firewall-cmd --set-default-zone=internal
firewall-cmd --info-zone=internal
firewall-cmd --zone=internal --permanent --add-service=samba
firewall-cmd --reload
#In this process, firewall-cmd --get-zones is used to list all available firewall zones, and firewall-cmd --get-default-zone checks the currently active default zone. The default zone is then changed to internal using firewall-cmd --set-default-zone=internal. The command firewall-cmd --info-zone=internal displays detailed information about the internal zone, including active services and network interfaces. To allow Samba traffic permanently, the Samba service is added to the internal zone using firewall-cmd --zone=internal --permanent --add-service=samba. After applying the changes with firewall-cmd --reload, the firewall configuration is reloaded, and the updated zone settings are verified again.</code></pre>

<img width="875" height="229" alt="image" src="https://github.com/user-attachments/assets/f246f596-7fa8-4d62-b5e3-e0c039b97e9e" />
<pre><code>sudo semanage fcontext --add --type samba_share_t "/share1(/.*)?"
sudo semanage fcontext --add --type samba_share_t "/home/user1/share2(/.*)?"
sudo restorecon -R /share1
sudo restorecon -R /home/user1/share2

#In this step, SELinux file contexts are configured to allow Samba access to shared directories. The semanage fcontext --add --type samba_share_t command is used to define the appropriate SELinux context for /share1 and /home/user1/share2, including all files and subdirectories. After defining the contexts, the restorecon -R command is executed to apply the new SELinux labels recursively. This ensures that the specified directories are correctly labeled and accessible by the Samba service under SELinux enforcement.</code></pre>

## Windows Client Access
<img width="760" height="247" alt="image" src="https://github.com/user-attachments/assets/658f1d7e-9ece-4030-8ac8-e0f61a08adab" /><br><br>
When the directory /home/user1/share2 is shared via Samba on a Linux system, all of its parent directories must have at least read and execute permissions for the Samba users.
The read (r) permission allows listing the contents of a directory, while the execute (x) permission allows entering directories and accessing files and subdirectories within them.
Without execute permission on any parent directory, users cannot access the shared directory or its files, even if they have full permissions on the shared folder itself.<br><br>
[user1@fedora43 ~]$ ls -ld /home/user1/share2<br><br>
drwxrwxr-x. 3 root family 4096 Jan 19 18:51 /home/user1/share2<br><br>
On the shared directory /home/user1/share2, full permissions are granted to the family group, of which the Samba users are members.<br><br>
[user1@fedora43 ~]$ ls -ld /home/user1<br><br>
drwx------. 5 user1 user1 4096 Jan 19 22:03 /home/user1<br><br>
The parent directory /home/user1 is owned by the user user1 and the group user1. While user1 has full permissions on this directory, it is not the only Samba user.
user2 and user3 are also Samba users, but they do not have user or group permissions on this directory.<br><br> 
[user1@fedora43 ~]$ sudo chmod 705 /home/user1<br><br>
[sudo] password for user1:<br><br>
Since changing ownership is not desired, permissions can be granted through the others permission set.<br><br>
By assigning read and write permissions to others, users user2 and user3, as members of the others category, gain the necessary access rights to the directory without modifying its ownership.<br><br>
[user1@fedora43 ~]$ ls -ld /home<br><br>
drwxr-xr-x. 6 root root 4096 Jan 19 17:19 /home<br><br>
The /home directory is owned by the root user and the root group. Since Samba users are neither the owner nor members of the owning group, they fall under the others permission category.
Because the others category already has read and execute permissions on the /home directory, Samba users have sufficient access rights to read and traverse this parent directory.
Therefore, no permission changes are required on the /home directory with respect to Samba access.<br><br>

<img width="832" height="558" alt="image" src="https://github.com/user-attachments/assets/0bf445e8-0afd-4835-be90-7b87b8353bf3" />
<pre><code>sudo wget http://ftp.debian.org/debian/README  
sudo wget http://ftp.debian.org/debian/extrafiles
#The purpose of executing these commands is to download several files from the internet
sudo mv extrafiles README /share1
#By executing the command sudo mv extrafiles README /share1, the files named extrafiles and README are moved into the first shared directory /share1.
sudo cp /share1/extrafiles /share1/README /home/user1/share2
#By executing the command sudo cp /share1/extrafiles /share1/README /home/user1/share2, the files named extrafiles and README are copied into the second shared directory /home/user1/share2.</code></pre>
The purpose of executing these commands was to download several files from the internet and place them into the shared directories in order to verify access permissions.
Specifically, the goal was to test whether Samba users could access the files in the first shared directory, and whether guest users could access the files in the second shared directory
<img width="600" height="252" alt="image" src="https://github.com/user-attachments/assets/775cde45-8c60-4f92-bae6-da724ac2ce95" />
<br>These permission commands are explained in the Samba installation and file sharing section of the project.The commands were re-executed to configure the permissions and ownership of the files added to the shared directories.<br>
<img width="743" height="661" alt="image" src="https://github.com/user-attachments/assets/e884d5e0-79b1-4a7a-8d06-76b7d4e44d92" />
<br>In the next step, a shortcut to the first shared directory on the Linux system will be created on the host operating system, Windows 11. On the Windows 11 host system, the Desktop is opened and the mouse pointer is moved to an empty area.<br>
<br>Left click,New,Shortcut<br>
<br><br>
<img width="610" height="451" alt="image" src="https://github.com/user-attachments/assets/010a3c56-95a9-4ab5-9ebb-05c3c81e010e" /><br><br>
<br>In the dialog box that appears, enter the shared directory address in the format \\(server-ip)\(sharedfoldername). Then click next.<br>
<br><br>
<img width="740" height="679" alt="image" src="https://github.com/user-attachments/assets/e461e633-1c60-4ba4-844e-be19b37834b3" /><br><br>
<br>At this point, the Windows credentials window is displayed<br>
<br><br>
<img width="452" height="500" alt="image" src="https://github.com/user-attachments/assets/074ff10d-d7ac-4e79-8c76-29ac71d83aad" /><br><br>
<br>The credentials for user1 are entered<br>
<br><br>
<img width="611" height="451" alt="image" src="https://github.com/user-attachments/assets/d4cdfaf9-b481-43e0-b0cf-a9a6d0761ca8" /><br><br>
<br>In this tab, the name under which the shared directory will be displayed can be specified. In this case, it is left unchanged.<br>
<br><br>
<img width="291" height="268" alt="image" src="https://github.com/user-attachments/assets/c90d7ad0-baf4-4487-ba7b-61b61ba8a1f4" /><br><br>
<br>At the end of these steps, a shortcut to the first shared directory is created.By double-clicking the shortcut, access to the shared folder is attempted.<br>
<br><br>
<img width="980" height="631" alt="image" src="https://github.com/user-attachments/assets/3dcaa47d-89a7-4263-9722-be094b0cab85" /><br><br>
<br>Access to the shared directory is confirmed by successfully listing its contents.Access to the files that were previously placed in the shared directory is tested<br>
<br><br>
<img width="821" height="810" alt="image" src="https://github.com/user-attachments/assets/346e2729-0e7a-4168-b94d-de7996415566" /><br><br>
<br>The attempt to access the files that were previously placed in the shared directory was unsuccessful, despite the permissions and ownership being configured correctly.This failure is caused by the SELinux security module. In the following steps, additional configuration will be performed to resolve this issue.<br>
<br><br>
<img width="1034" height="843" alt="image" src="https://github.com/user-attachments/assets/44a4d82f-b7d8-464e-9ed1-036a74c5ce30" />
<img width="981" height="634" alt="image" src="https://github.com/user-attachments/assets/79b8e72f-4893-4166-ae50-c0354e14b192" />
<img width="995" height="811" alt="image" src="https://github.com/user-attachments/assets/24878cbd-68d3-4f15-a519-18af30550a11" />
<img width="983" height="638" alt="image" src="https://github.com/user-attachments/assets/3aa53ac4-d770-4a8d-a646-96a91fc66918" />
<img width="988" height="708" alt="image" src="https://github.com/user-attachments/assets/0b841c58-6d6f-43c5-870b-52d07a6c32de" /><br><br>
<br>As shown in the images above, new files and directories can be created and modified as desired using the user1 account<br>
<br><br>
<img width="623" height="226" alt="image" src="https://github.com/user-attachments/assets/08bf4ac5-84da-406a-b2ca-c52e4787e08c" /><br><br>
<pre><code></code>sudo setsebool -P samba_export_all_rw on
#The command sudo setsebool -P samba_export_all_rw on enables SELinux to allow Samba to read from and write to exported files and directories, provided that the underlying Linux file and directory permissions permit such access.
</pre></code>
<img width="978" height="631" alt="image" src="https://github.com/user-attachments/assets/5b7413f8-1190-4917-b656-32b84a2ca41f" /><br><br>
<br>Access to the contents of the previously placed files in the shared directory is tested<br>
<br><br>
<img width="820" height="807" alt="image" src="https://github.com/user-attachments/assets/5ba10b58-f54b-418d-85d4-87455c9cf7be" /><br><br>
<br>After the final SELinux configuration, access to the previously added files is successfully achieved<br>
<br><br>
<img width="1108" height="625" alt="image" src="https://github.com/user-attachments/assets/b3c91c1f-e19f-4cd8-85c4-76649365c75e" />
<pre><code>taskkill /f /im explorer.exe
#taskkill /f /im explorer.exe resets the File Explorer session and prevents UI‑level SMB credential reuse. It does not terminate SMB sessions on its own.This command prevents Windows from automatically reconnecting to the SMB share using user1’s credentials after the active SMB session has been terminated.
start explorer.exe
#This command is used to start (or restart) the Windows Explorer process, which provides the main graphical user interface of Windows.
net use /delete *
#net use /delete * disconnects active smb connections. (user1 disconnects)
net use \\192.168.1.28\Share1 /user:user2 *
#This command is used to establish an SMB network connection to the shared folder using the user2 account.</pre></code>
<img width="1120" height="331" alt="image" src="https://github.com/user-attachments/assets/adaff6a8-6bf5-415d-ab92-40d056795930" />
<pre><code>sudo smbstatus
#The sudo smbstatus command allows verification of which users are currently connected to the shared directories. As intended, the output confirms that user2 is actively connected.</pre></code>
<img width="978" height="631" alt="image" src="https://github.com/user-attachments/assets/26f10ed6-4aa5-4641-b35d-85477417c963" />
<img width="1003" height="628" alt="image" src="https://github.com/user-attachments/assets/2c493085-23d6-4754-b6a9-3adb3c7ed2ca" />
<img width="973" height="629" alt="image" src="https://github.com/user-attachments/assets/47a5fe13-c84a-4a0a-9186-9f0d770917d7" />
<img width="975" height="629" alt="image" src="https://github.com/user-attachments/assets/22201e43-63f0-4d63-be0b-6cd972c1a2d6" />
<img width="982" height="772" alt="image" src="https://github.com/user-attachments/assets/9daadc47-3623-4625-9915-263991ac4060" />
<img width="975" height="631" alt="image" src="https://github.com/user-attachments/assets/e66a5134-2548-4ee6-b25d-efe327366283" />
<img width="976" height="632" alt="image" src="https://github.com/user-attachments/assets/14fc94dd-9685-4a66-a1cc-2c3df8937074" />
<img width="1110" height="629" alt="image" src="https://github.com/user-attachments/assets/2fb84589-21eb-4b17-b552-41c802d41429" />
<img width="1176" height="387" alt="image" src="https://github.com/user-attachments/assets/e8ed3153-a95b-40cf-9d01-376b36441576" />
<img width="979" height="630" alt="image" src="https://github.com/user-attachments/assets/6749a1be-9077-43dd-a80b-e748801a05a3" />
<img width="976" height="628" alt="image" src="https://github.com/user-attachments/assets/7646897c-c260-4022-a923-807282dba1b8" />
<img width="978" height="878" alt="image" src="https://github.com/user-attachments/assets/21682e11-0b2e-4a2c-a8db-680dbaf1c2bf" />
<img width="975" height="883" alt="image" src="https://github.com/user-attachments/assets/134e6d17-6474-4cbb-b699-bbc5580916cd" />
<img width="978" height="778" alt="image" src="https://github.com/user-attachments/assets/1d18fcb8-80c9-4c7c-855a-e46d0498bd3a" />
<img width="974" height="630" alt="image" src="https://github.com/user-attachments/assets/9d4b3f51-f9ad-4108-bb23-ae500950c272" />
<img width="980" height="628" alt="image" src="https://github.com/user-attachments/assets/eac50070-66ae-4023-9a3a-186c4ed1c105" />
<img width="976" height="630" alt="image" src="https://github.com/user-attachments/assets/36ed0de1-a001-4544-8060-5d6c462924fd" />
<img width="980" height="630" alt="image" src="https://github.com/user-attachments/assets/6670d4a2-c584-42e8-9879-7adb485bfb19" />
<img width="1111" height="626" alt="image" src="https://github.com/user-attachments/assets/343c0b1e-1e34-4052-8316-5d024942381f" />
<img width="1156" height="372" alt="image" src="https://github.com/user-attachments/assets/6ba04b23-06e3-4d2a-89e1-b9f79453146c" />
<img width="833" height="783" alt="image" src="https://github.com/user-attachments/assets/e2605f87-959c-45a8-9c2d-c8cdf63fb591" />
<img width="1106" height="862" alt="image" src="https://github.com/user-attachments/assets/5a03a324-99ac-4538-a646-5fb3dc237716" />
<img width="1111" height="503" alt="image" src="https://github.com/user-attachments/assets/1f7ad104-262d-4be4-8377-3d000e477246" />
<img width="778" height="819" alt="image" src="https://github.com/user-attachments/assets/c37ea856-9f08-4de9-9722-a1ac087b1bcd" />
<img width="610" height="448" alt="image" src="https://github.com/user-attachments/assets/eeb6e532-e381-4878-8b79-2488c2b59d8e" />
<img width="612" height="450" alt="image" src="https://github.com/user-attachments/assets/9a55fdd2-b0c3-447c-b611-db9721cc8271" />
<img width="978" height="629" alt="image" src="https://github.com/user-attachments/assets/b702aaae-c5ce-49bb-96d6-3d14781a80aa" />
<img width="822" height="752" alt="image" src="https://github.com/user-attachments/assets/8b127f79-4ab8-46ee-9ce8-161b221572c6" />
<img width="985" height="826" alt="image" src="https://github.com/user-attachments/assets/20fe1959-cd3b-4dcf-8c0b-01892bd4b58a" />
<img width="1135" height="833" alt="image" src="https://github.com/user-attachments/assets/8ca30296-e4d5-4abf-bf60-404f5645b3ae" />
<img width="995" height="790" alt="image" src="https://github.com/user-attachments/assets/dc4872ea-dc59-481f-8024-967caa61cbc1" />
<img width="1123" height="638" alt="image" src="https://github.com/user-attachments/assets/ae63ee99-a5be-420a-87a6-95f692ad5d7f" />
















## Conclusion
