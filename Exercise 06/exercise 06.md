![Altschool Africa Logo](./images/1633989073690.jpg)



# Exercise

## Task:
 Review the CIS benchmark for ubuntu, and try to implement at least 10 of the recommendations that we made within the benchmark.

 ## Solution
 <ol>

 <li><b>Ensure package manager repositories are configured</b>

 Systems need to have package manager repositories configured to ensure they receive the latest patches and updates.If a system's package repositories are misconfigured important patches may not be identified or a rogue repository could introduce compromised software.

<b>Remediation:</b>
Configure your package manager repositories according to site policy.
</li>

<li>

<b>Disable IPV6</b>

Although IPv6 has many advantages over IPv4, not all organizations have IPv6 or dual stack configurations implemented. If IPv6 or dual stack is not to be used, it is recommended that IPv6 be disabled to reduce the attack surface of the system.

<b>Remediation:</b>
Edit /etc/default/grub and add ipv6.disable=1 to the GRUB_CMDLINE_LINUX parameters:

Run the following command:

 ```sh
  GRUB_CMDLINE_LINUX="ipv6.disable=1"
  ``` 
Update grub

 ```sh
  update-grub
  ``` 
</li>

<li>
<b>Ensure DHCP server is not installed</b>

The Dynamic Host Configuration Protocol (DHCP) is a service that allows machines to be dynamically assigned IP addresses. Unless a system is specifically set up to act as a DHCP server, it is recommended that this package be removed to reduce the potential attack surface.

<b> Remediation:</b>
Run the following command to remove isc-dhcp-server:


 ```sh
  apt purge isc-dhcp-server
  ``` 
</li>

<li>
<b>Ensure ufw is installed</b>

The Uncomplicated Firewall (ufw) is a frontend for iptables and is particularly well-suited for host-based firewalls. ufw provides a framework for managing netfilter, as well as a command-line interface for manipulating the firewall. A firewall utility is required to configure the Linux kernel's netfilter framework via the iptables or nftables back-end.
The Linux kernel's netfilter framework host-based firewall can protect against threats originating from within a corporate network to include malicious mobile code and poorly configured software on a host.

<b>Remediation:</b>
Run the following command to install Uncomplicated Firewall (UFW):

```sh
  apt install ufw
  ``` 
</li>

<li>
<b>Ensure successful file system mounts are collected</b>

Monitor the use of the mount system call. The mount (and umount ) system call controls the mounting and unmounting of file systems. The parameters below configure the system to create an audit record when the mount system call is used by a non-privileged user.

<b>Remediation:</b>
Edit or create a file in the /etc/audit/rules.d/ directory ending in .rules 

Example: 
```sh 
vi /etc/audit/rules.d/50-mounts.rules 
   ```
Add the following lines:

```sh
  -a always,exit -F arch=b64 -S mount -F auid>=1000 -F auid!=4294967295 -k mounts
   -a always,exit -F arch=b32 -S mount -F auid>=1000 -F auid!=4294967295 -k mounts
  ``` 
</li>

<li>
<b>Ensure permissions on /etc/ssh/sshd_config are configured</b>

The /etc/ssh/sshd_config file contains configuration specifications for sshd. The command below sets the owner and group of the file to root. The /etc/ssh/sshd_config file needs to be protected from unauthorized changes by non-privileged users.

<b>Remediation:</b>
Run the following commands to set ownership and permissions on /etc/ssh/sshd_config:

```sh
   chown root:root /etc/ssh/sshd_config 
   chmod og-rwx /etc/ssh/sshd_config
   ```
</li>

<li>
<b>Ensure permissions on SSH private host key files are configured</b>
An SSH private key is one of two files used in SSH public key authentication. In this authentication method, The possession of the private key is proof of identity. Only a private key that corresponds to a public key will be able to authenticate successfully. The private keys need to be stored and handled carefully, and no copies of the private key should be distributed.

<b>Remediation:</b>
Run the following commands to set permissions, ownership, and group on the private SSH host key files:

```sh
  find /etc/ssh -xdev -type f -name 'ssh_host_*_key' -exec chown root:root {} \; 
  find /etc/ssh -xdev -type f -name 'ssh_host_*_key' -exec chmod u-x,go-rwx {} \;
   ```
</li>

<li>
<b>Ensure password reuse is limited</b>

The /etc/security/opasswd file stores the users' old passwords and can be checked to ensure that users are not recycling recent passwords. Forcing users not to reuse their past 5 passwords make it less likely that an attacker will be able to guess the password.

<b>Remediation:</b>
Edit the /etc/pam.d/common-password file to include the remember option and conform to site policy as shown:

```sh
  password required pam_pwhistory.so remember=5
  ```
</li>

<li>
<b>Ensure password hashing algorithm is SHA-512</b>

The commands below change password encryption from md5 to sha512 (a much stronger hashing algorithm). All existing accounts will need to perform a password change to upgrade the stored hashes to the new algorithm.

The SHA-512 algorithm provides much stronger hashing than MD5, thus providing additional protection to the system by increasing the level of effort for an attacker to successfully determine passwords.
Note that these change only apply to accounts configured on the local system.

<b>Remediation:</b>
Edit the /etc/pam.d/common-password file to include the sha512 option for pam_unix.so as shown:

```sh
  password [success=1 default=ignore] pam_unix.so sha512
  ```
</li>

<li>
<b>Ensure root is the only UID 0 account</b>

Any account with UID 0 has superuser privileges on the system.
This access must be limited to only the default root account and only from the system console. Administrative access must be through an unprivileged account using an approved mechanism as noted in Item 5.6 Ensure access to the su command is restricted.

<b>Remediation:</b>
Remove any users other than root with UID 0 or assign them a new UID if appropriate.
</li>