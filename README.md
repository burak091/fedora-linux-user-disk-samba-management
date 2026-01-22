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
<img width="501" height="684" alt="image" src="https://github.com/user-attachments/assets/ebec5f6a-b188-471a-a649-dec48cebfdde" />
<img width="784" height="452" alt="image" src="https://github.com/user-attachments/assets/66cb3073-dc3e-4c4c-a54e-b22004efcfc7" />
<img width="551" height="239" alt="image" src="https://github.com/user-attachments/assets/f455114a-c11b-4b73-ab7f-1c092f55140c" />
<img width="408" height="109" alt="image" src="https://github.com/user-attachments/assets/dbcf0f0b-e87d-45e1-abdc-2e4d89b6b44e" />
The command fdisk /dev/nvme0n1 was executed to start the interactive partitioning tool. m option was used to display the help menu.To create a new partition, the n (new) option was selected. Since the disk did not contain any previous partitions, a primary partition was created by accepting the default partition type.
For the first partition, the default starting sector was accepted. This ensures proper alignment with the disk’s sector boundaries and is considered best practice for performance and compatibility. The size of the first partition was defined as 5 GB by specifying the appropriate ending sector.
After creating the first partition, the n option was selected again to create a second primary partition. The default starting sector was accepted once more, allowing the partition to begin immediately after the first partition. The second partition was allocated the remaining 5 GB of the disk space.
Once both partitions were defined, the p option was used to display the current partition table and verify the configuration. Finally, the w option was selected to write the partition table to the disk and permanently save the changes.
<img width="1048" height="865" alt="image" src="https://github.com/user-attachments/assets/2e583b8b-b7c4-4f51-84f9-a3c7976fc812" />




## Mount Configuration
<img width="458" height="64" alt="image" src="https://github.com/user-attachments/assets/92f6c55d-c344-4669-9ce5-5cda4c02ced9" />
<img width="1068" height="504" alt="image" src="https://github.com/user-attachments/assets/5b1f1ab6-9465-4d95-a042-cdfb8f9e701b" />
<img width="335" height="87" alt="image" src="https://github.com/user-attachments/assets/662267e6-669c-4203-baf6-75223be0faa9" />
<img width="717" height="399" alt="image" src="https://github.com/user-attachments/assets/a2e05829-15c9-4300-803e-a7fe8b41b4a2" />
<img width="1050" height="1027" alt="image" src="https://github.com/user-attachments/assets/283e585d-55c6-4211-a0e6-fe84fd2c4ed2" />

## Samba Installation and File Sharing
<img width="1902" height="775" alt="image" src="https://github.com/user-attachments/assets/560936bf-bb0d-42d5-92d3-a489a29cce86" />
<img width="1903" height="913" alt="image" src="https://github.com/user-attachments/assets/7f97f099-363f-4ae6-9e01-c02b51c5ac4d" />
<img width="485" height="272" alt="image" src="https://github.com/user-attachments/assets/ee7945fe-9516-4438-a922-dfb65755a056" />
<img width="563" height="303" alt="image" src="https://github.com/user-attachments/assets/7e9c3d72-e1e0-47d8-9d3a-94d925585e1a" />
<img width="463" height="200" alt="image" src="https://github.com/user-attachments/assets/686f5ec6-6fcb-4323-9761-2dabdc79a3b1" />
<img width="727" height="854" alt="image" src="https://github.com/user-attachments/assets/80fd30f7-e549-4b98-865d-43aa92779fdb" />
<img width="838" height="1030" alt="image" src="https://github.com/user-attachments/assets/8616b06c-d69e-4e9e-9cc9-5d79778e3f57" />




<img width="629" height="237" alt="image" src="https://github.com/user-attachments/assets/0fa17e71-4a64-4c98-8a3a-7852fa042830" />





## Firewall, SELinux and Service Verification
<img width="773" height="604" alt="image" src="https://github.com/user-attachments/assets/7edfa737-8f6c-4317-bd4d-f5611a9fd76c" />
<img width="1176" height="1031" alt="image" src="https://github.com/user-attachments/assets/3130261e-151e-4909-a7c8-10f77f727aa6" />
<img width="875" height="229" alt="image" src="https://github.com/user-attachments/assets/f246f596-7fa8-4d62-b5e3-e0c039b97e9e" />

## Windows Client Access
<img width="760" height="247" alt="image" src="https://github.com/user-attachments/assets/658f1d7e-9ece-4030-8ac8-e0f61a08adab" />
<img width="832" height="558" alt="image" src="https://github.com/user-attachments/assets/0bf445e8-0afd-4835-be90-7b87b8353bf3" />
<img width="600" height="252" alt="image" src="https://github.com/user-attachments/assets/775cde45-8c60-4f92-bae6-da724ac2ce95" />
<img width="743" height="661" alt="image" src="https://github.com/user-attachments/assets/e884d5e0-79b1-4a7a-8d06-76b7d4e44d92" />
<img width="610" height="451" alt="image" src="https://github.com/user-attachments/assets/010a3c56-95a9-4ab5-9ebb-05c3c81e010e" />
<img width="740" height="679" alt="image" src="https://github.com/user-attachments/assets/e461e633-1c60-4ba4-844e-be19b37834b3" />
<img width="452" height="500" alt="image" src="https://github.com/user-attachments/assets/074ff10d-d7ac-4e79-8c76-29ac71d83aad" />
<img width="611" height="451" alt="image" src="https://github.com/user-attachments/assets/d4cdfaf9-b481-43e0-b0cf-a9a6d0761ca8" />
<img width="291" height="268" alt="image" src="https://github.com/user-attachments/assets/c90d7ad0-baf4-4487-ba7b-61b61ba8a1f4" />
<img width="980" height="631" alt="image" src="https://github.com/user-attachments/assets/3dcaa47d-89a7-4263-9722-be094b0cab85" />
<img width="821" height="810" alt="image" src="https://github.com/user-attachments/assets/346e2729-0e7a-4168-b94d-de7996415566" />
<img width="1034" height="843" alt="image" src="https://github.com/user-attachments/assets/44a4d82f-b7d8-464e-9ed1-036a74c5ce30" />
<img width="981" height="634" alt="image" src="https://github.com/user-attachments/assets/79b8e72f-4893-4166-ae50-c0354e14b192" />
<img width="995" height="811" alt="image" src="https://github.com/user-attachments/assets/24878cbd-68d3-4f15-a519-18af30550a11" />
<img width="983" height="638" alt="image" src="https://github.com/user-attachments/assets/3aa53ac4-d770-4a8d-a646-96a91fc66918" />
<img width="988" height="708" alt="image" src="https://github.com/user-attachments/assets/0b841c58-6d6f-43c5-870b-52d07a6c32de" />
<img width="623" height="226" alt="image" src="https://github.com/user-attachments/assets/08bf4ac5-84da-406a-b2ca-c52e4787e08c" />
<img width="978" height="631" alt="image" src="https://github.com/user-attachments/assets/5b7413f8-1190-4917-b656-32b84a2ca41f" />
<img width="820" height="807" alt="image" src="https://github.com/user-attachments/assets/5ba10b58-f54b-418d-85d4-87455c9cf7be" />
<img width="1108" height="625" alt="image" src="https://github.com/user-attachments/assets/b3c91c1f-e19f-4cd8-85c4-76649365c75e" />
<img width="1120" height="331" alt="image" src="https://github.com/user-attachments/assets/adaff6a8-6bf5-415d-ab92-40d056795930" />
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
