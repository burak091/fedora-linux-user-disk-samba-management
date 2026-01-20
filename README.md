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
## User Management
<img width="383" height="96" alt="image" src="https://github.com/user-attachments/assets/82289dce-9cf4-429c-b545-a8801e1a7b57" />
<img width="629" height="363" alt="image" src="https://github.com/user-attachments/assets/a2279397-8af4-45c6-a325-75f467e7ee1e" />
<img width="777" height="650" alt="image" src="https://github.com/user-attachments/assets/f11416cb-00f2-4836-b130-3641335528eb" />
<img width="450" height="144" alt="image" src="https://github.com/user-attachments/assets/d3d26800-7d77-4882-bbb8-b1a4483e7dbe" />
<img width="418" height="130" alt="image" src="https://github.com/user-attachments/assets/d1dd50c1-07c9-4cbb-af86-c9c34af0aef7" />
<img width="841" height="467" alt="image" src="https://github.com/user-attachments/assets/0c9a5206-35ee-4adf-b9f9-66208ecacb22" />
<img width="338" height="164" alt="image" src="https://github.com/user-attachments/assets/cb8dbfd6-49ed-4e64-8bbc-10fdbff6074d" />
<img width="600" height="387" alt="image" src="https://github.com/user-attachments/assets/9b9d3045-e0fd-4d3b-838d-07d8fc1168d5" />
<img width="356" height="113" alt="image" src="https://github.com/user-attachments/assets/84b9324e-df68-44ef-8eeb-f2f7ea46e536" />
<img width="799" height="596" alt="image" src="https://github.com/user-attachments/assets/6ff320b7-a3d3-43cc-9842-5c8ac48c6431" />
<img width="783" height="661" alt="image" src="https://github.com/user-attachments/assets/d4c05e6a-a71b-48b5-b669-c923cbf492ef" />
<img width="344" height="165" alt="image" src="https://github.com/user-attachments/assets/bdbba20b-0828-485c-93c3-1d93a2c35766" />
<img width="349" height="151" alt="image" src="https://github.com/user-attachments/assets/1b4315db-6217-43c6-aa17-47fb511c2fd8" />




## Disk and Partition Management
<img width="1655" height="951" alt="image" src="https://github.com/user-attachments/assets/59189302-490c-4df4-89b9-6fcb6dd143f0" />
<img width="757" height="732" alt="image" src="https://github.com/user-attachments/assets/edd216cc-1875-4acc-aa9e-09bc76038e5e" />
<img width="434" height="430" alt="image" src="https://github.com/user-attachments/assets/e9198bcb-3e8e-4610-9c26-ebd4ccf6975e" />
<img width="435" height="423" alt="image" src="https://github.com/user-attachments/assets/1d83a900-0919-473d-b7d8-566f277fcb87" />
<img width="442" height="425" alt="image" src="https://github.com/user-attachments/assets/c63ad50e-2fa2-4275-85f4-d24cc684fd95" />
<img width="438" height="424" alt="image" src="https://github.com/user-attachments/assets/43ae2222-626b-4783-af40-c65837cc1988" />
<img width="442" height="425" alt="image" src="https://github.com/user-attachments/assets/2b50761c-8f64-40fa-a922-c6fd7545574c" />
<img width="753" height="729" alt="image" src="https://github.com/user-attachments/assets/d0b08823-7725-4399-a83b-a86a6d5bf2a8" />
<img width="491" height="294" alt="image" src="https://github.com/user-attachments/assets/54a4ec7a-1d0f-42b2-bf8a-6b781c747cec" />
<img width="501" height="684" alt="image" src="https://github.com/user-attachments/assets/ebec5f6a-b188-471a-a649-dec48cebfdde" />
<img width="784" height="452" alt="image" src="https://github.com/user-attachments/assets/66cb3073-dc3e-4c4c-a54e-b22004efcfc7" />
<img width="551" height="239" alt="image" src="https://github.com/user-attachments/assets/f455114a-c11b-4b73-ab7f-1c092f55140c" />
<img width="408" height="109" alt="image" src="https://github.com/user-attachments/assets/dbcf0f0b-e87d-45e1-abdc-2e4d89b6b44e" />
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
<img width="928" height="1032" alt="image" src="https://github.com/user-attachments/assets/a4e4538b-69bc-4c22-830c-27c725685786" />


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
<img width="508" height="264" alt="image" src="https://github.com/user-attachments/assets/af824e6e-eb1d-428d-a480-0f468d1d5d17" />
<img width="934" height="1031" alt="image" src="https://github.com/user-attachments/assets/0de02c3c-fd7c-4ba1-b8f4-8febef1aaaec" />
<img width="492" height="183" alt="image" src="https://github.com/user-attachments/assets/c856aa1e-10da-4f02-b702-3c48da02a69e" />
<img width="1110" height="402" alt="image" src="https://github.com/user-attachments/assets/e2d1bd5d-13da-4c56-8b5a-0f8cc459a5e6" />
<img width="1113" height="139" alt="image" src="https://github.com/user-attachments/assets/7eb26390-a436-4b22-b2ac-6110f4390304" />

<img width="1109" height="417" alt="image" src="https://github.com/user-attachments/assets/2faba5a9-7e6b-4d09-a78b-b26828bc5cba" />




## Conclusion
