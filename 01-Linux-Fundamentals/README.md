# Linux Fundamentals Lab
## Lab Objective

The objective of this lab is to develop practical Linux command-line
skills that are useful for cybersecurity, networking, and system
administration.

## Lab Environment

- Operating System: Kali Linux
- Interface: Terminal
- Shell: Zsh
- Environment: Personal authorized cybersecurity lab

## Lab 01 - System Information

### Check Current User

Command:

```bash
whoami
```
### Result

```text
kali
```

### Explanation

The `whoami` command displays the username of the currently logged-in user.
The result shows that the current user is `kali`.
### Check Hostname

Command:

```bash
hostname
```

### Result

```text
kali
```

### Explanation

The `hostname` command displays the name assigned to the system.
The result shows that the hostname of this Kali Linux machine is `kali`.
### Check Operating System Information

Command:

```bash
cat /etc/os-release
```

### Result

```text
PRETTY_NAME="Kali GNU/Linux Rolling"
NAME="Kali GNU/Linux"
VERSION_ID="2026.3"
VERSION="2026.3"
VERSION_CODENAME=kali-rolling
ID=kali
ID_LIKE=debian
```

### Explanation

The `/etc/os-release` file contains information about the Linux operating
system. The output shows that this lab machine is running Kali GNU/Linux
Rolling version 2026.3, which is based on Debian.
### Check Kernel and System Information

Command:

```bash
uname -a
```

### Result

```text
Linux kali 7.0.12+kali-amd64 #1 SMP PREEMPT_DYNAMIC Kali 7.0.12-2kali1 (2026-06-18) x86_64 GNU/Linux
```

### Explanation

The `uname -a` command displays detailed information about the Linux
system and kernel. The output shows that the system is running the
Kali Linux kernel `7.0.12+kali-amd64` on a 64-bit (`x86_64`)
architecture.

---

## Lab 02 - File System Navigation

### Objective

The objective of this lab is to practice navigating the Linux file system
using basic command-line tools.

### Check Current Working Directory

Command:

```bash
pwd
```
### Result

```text
/home/kali
```

### Explanation

The `pwd` command stands for **Print Working Directory**.
It displays the full path of the directory I am currently working in.

The result `/home/kali` shows that I am currently in the home
directory of the `kali` user.
### List Files and Directories

Command:

```bash
ls
```

### Result

The command displayed the files and directories located in my current
working directory, including standard directories such as:

```text
Desktop
Documents
Downloads
Music
Pictures
Projects
Public
Templates
Videos
```

### Explanation

The `ls` command lists the files and directories in the current working
directory. It is commonly used to inspect the contents of a directory
before navigating to or working with files.

### View Detailed and Hidden Files

Command:

```bash
ls -la
```

### Result

Example entries from the output:

```text
drwxr-xr-x  2 kali kali  4096 Desktop
drwxr-xr-x  2 kali kali  4096 Documents
drwxr-xr-x  2 kali kali  4096 Downloads
drwxr-xr-x  2 kali kali  4096 Pictures
drwxr-xr-x  2 kali kali  4096 Projects
drwxr-xr-x  2 kali kali  4096 Public
drwxr-xr-x  2 kali kali  4096 Templates
drwxr-xr-x  2 kali kali  4096 Videos
```

### Explanation

The `ls -la` command displays a detailed listing of files and directories.

- `-l` displays detailed information such as permissions, owner, group, and size.
- `-a` includes hidden files and directories.
- Files beginning with `.` are normally hidden in Linux.

This command is useful for examining file ownership and permissions during
Linux system administration and security analysis.

### Change Directory

Command:

```bash
cd Documents
pwd
```

### Result

```text
/home/kali/Documents
```

### Explanation

The `cd` command stands for **Change Directory** and is used to move
between directories in the Linux file system.

In this example, I moved from `/home/kali` to the `Documents` directory.
The `pwd` command was then used to confirm the current working directory.

---

## Lab 03 - File and Directory Management

### Objective

The objective of this lab is to practice creating, copying, moving,
renaming, and deleting files and directories using Linux commands.

### Create a Directory

Command:

```bash
mkdir cybersecurity-lab
```
### Result

```text
cybersecurity-lab
```

### Explanation

The `mkdir` command stands for **Make Directory**. It is used to create
a new directory in Linux.

In this lab, I created a directory named `cybersecurity-lab` inside
`/home/kali/Documents` and used the `ls` command to verify that the
directory was created successfully.

### Create a File

Command:

```bash
cd cybersecurity-lab
touch notes.txt
ls -l
```

### Result

```text
total 0
-rw-rw-r-- 1 kali kali 0 Sep 20 06:59 notes.txt
```

### Explanation

The `touch` command can be used to create an empty file if the specified
file does not already exist.

In this lab, I created a file named `notes.txt` inside the
`cybersecurity-lab` directory. I then used `ls -l` to verify that the
file was created successfully.

### Copy a File

Command:

```bash
cp notes.txt notes-backup.txt
ls -l
```

### Result

```text
total 0
-rw-rw-r-- 1 kali kali 0 Sep 20 07:01 notes-backup.txt
-rw-rw-r-- 1 kali kali 0 Sep 20 06:59 notes.txt
```

### Explanation

The `cp` command is used to copy files and directories in Linux.

In this lab, I copied `notes.txt` and created a new file named
`notes-backup.txt`. The `ls -l` command confirmed that both the
original file and the copied file exist.

### Rename a File

Command:

```bash
mv notes.txt linux-notes.txt
ls -l
```

### Result

```text
total 0
-rw-rw-r-- 1 kali kali 0 Sep 20 06:59 linux-notes.txt
-rw-rw-r-- 1 kali kali 0 Sep 20 07:01 notes-backup.txt
```

### Explanation

The `mv` command is used to move or rename files and directories in Linux.

In this lab, I renamed `notes.txt` to `linux-notes.txt`. The `ls -l`
command confirmed that the original filename was replaced by the new
filename.

### Delete a File

Command:

```bash
rm notes-backup.txt
ls -l
```

### Result

```text
total 0
-rw-rw-r-- 1 kali kali 0 Sep 20 06:59 linux-notes.txt
```

### Explanation

The `rm` command is used to remove files in Linux.

In this lab, I deleted the `notes-backup.txt` file. I then used
`ls -l` to verify that the file had been removed successfully.

The `rm` command should be used carefully because deleted files are
not normally moved to a recycle bin when removed from the terminal.

### Remove a Directory

First, I attempted to remove the directory while it still contained a file.

Command:

```bash
rmdir cybersecurity-lab
```

### Result

```text
rmdir: failed to remove 'cybersecurity-lab': Directory not empty
```

The command failed because `rmdir` only removes empty directories.

I then removed the remaining test file:

```bash
rm cybersecurity-lab/linux-notes.txt
```

I verified that the directory was empty:

```bash
ls -la cybersecurity-lab
```

Result:

```text
total 8
drwxrwxr-x 2 kali kali 4096 Sep 20 07:10 .
drwxr-xr-x 3 kali kali 4096 Sep 20 06:57 ..
```

I then removed the empty directory:

```bash
rmdir cybersecurity-lab
```

### Explanation

The `rmdir` command is used to remove empty directories in Linux.

This exercise demonstrated that `rmdir` will not remove a directory
that still contains files. After deleting the remaining file, the
directory was successfully removed.

This behavior helps prevent accidental deletion of directories that
still contain data.

---

## Lab 04 - Linux File Permissions

### Objective

The objective of this lab is to understand Linux file permissions and
practice viewing and modifying access permissions using commands such
as `ls -l` and `chmod`.

### Create a Test File

Command:

```bash
touch permission-test.txt
ls -l permission-test.txt
```
### Result

```text
-rw-rw-r-- 1 kali kali 0 Sep 20 11:09 permission-test.txt
```

### Explanation

The `ls -l` command displays detailed information about a file,
including its permissions, owner, group, size, and modification time.

The permission string for this file is:

```text
-rw-rw-r--
```

This means:

- `-` - Regular file
- `rw-` - Owner can read and write
- `rw-` - Group can read and write
- `r--` - Others can only read

Linux file permissions are represented using:

- `r` - Read
- `w` - Write
- `x` - Execute
- `-` - Permission not granted

 ### Change File Permissions to 600

Command:

```bash
chmod 600 permission-test.txt
ls -l permission-test.txt
```

### Result

```text
-rw------- 1 kali kali 0 Sep 20 11:09 permission-test.txt
```

### Explanation

The `chmod` command is used to change file permissions in Linux.

The permission value `600` means:

- Owner: Read + Write (`rw-`)
- Group: No permissions (`---`)
- Others: No permissions (`---`)

The resulting permission string is:

```text
-rw-------
```

This configuration is useful for files that should only be accessible
by their owner.

### Change File Permissions to 755

Command:

```bash
chmod 755 permission-test.txt
ls -l permission-test.txt
```

### Result

```text
-rwxr-xr-x 1 kali kali 0 Sep 20 11:09 permission-test.txt
```

### Explanation

The `chmod 755` command changes the file permissions so that the owner
has full read, write, and execute permissions, while the group and
others have read and execute permissions.

The numeric permissions are calculated as:

- Read (`r`) = 4
- Write (`w`) = 2
- Execute (`x`) = 1

Therefore:

- Owner: `rwx` = 4 + 2 + 1 = 7
- Group: `r-x` = 4 + 1 = 5
- Others: `r-x` = 4 + 1 = 5

This produces the permission string `rwxr-xr-x`.

### Change File Permissions to 644

Command:

```bash
chmod 644 permission-test.txt
ls -l permission-test.txt
```

### Result

```text
-rw-r--r-- 1 kali kali 0 Sep 20 11:09 permission-test.txt
```

### Explanation

The `chmod 644` command changes the file permissions so that the owner
can read and write the file, while the group and others can only read it.

The numeric permissions are:

- Owner: `rw-` = 4 + 2 = 6
- Group: `r--` = 4
- Others: `r--` = 4

Therefore, `644` produces the permission string `rw-r--r--`.

### Cleanup

After completing the permission tests, the temporary file was removed.

Command:

```bash
rm permission-test.txt
ls -l permission-test.txt
```

### Result

```text
ls: cannot access 'permission-test.txt': No such file or directory
```

This confirms that the test file was successfully removed.

### Lab Conclusion

This lab demonstrated how Linux file permissions control access to files.
I practiced viewing permissions with `ls -l` and modifying permissions
using `chmod`.

The permission modes tested were:

- `600` - Owner can read and write; group and others have no permissions.
- `755` - Owner can read, write, and execute; group and others can read and execute.
- `644` - Owner can read and write; group and others can only read.

Understanding Linux permissions is important in cybersecurity because
incorrect permissions can expose sensitive files or allow unauthorized
users to modify or execute files.

---

## Lab 05 - Linux Users and Groups

### Objective

The objective of this lab is to understand Linux users and groups and
practice commands used to identify user accounts, user IDs, group IDs,
and group memberships.

### Check the Current User

Command:

```bash
whoami
```
### Result

```text
kali
```
### Explanation

The `whoami` command displays the username of the currently logged-in
user. In this lab, the current user is `kali`.

### Check User and Group Information

Command:

```bash
id
```

### Result

```text
uid=1000(kali) gid=1000(kali) groups=1000(kali),4(adm),20(dialout),24(cdrom),25(floppy),27(sudo),29(audio),30(dip),44(video),46(plugdev),100(users),101(netdev),102(scanner),118(wireshark),119(kaboxer),968(vboxsf),982(bluetooth),999(lpadmin)
```

### Explanation

The `id` command displays the current user's User ID (UID), primary
Group ID (GID), and group memberships.

In this system:

- `uid=1000(kali)` - The user `kali` has UID 1000.
- `gid=1000(kali)` - The primary group is `kali` with GID 1000.
- `groups=...` - Shows all groups that the user belongs to.
- `sudo` - Allows the user to perform authorized administrative tasks using `sudo`.
- `wireshark` - Provides access associated with Wireshark packet capture.
- `vboxsf` - Used for VirtualBox shared-folder access.

### Check Group Memberships

Command:

```bash
groups
```

### Result

```text
kali adm dialout cdrom floppy sudo audio dip video plugdev users netdev scanner wireshark kaboxer vboxsf bluetooth lpadmin
```

### Explanation

The `groups` command displays all groups that the current user belongs to.

The user `kali` belongs to several groups. Some important examples are:

- `sudo` - Allows authorized administrative commands to be executed with elevated privileges.
- `wireshark` - Provides access associated with network packet capturing.
- `vboxsf` - Provides access to VirtualBox shared folders.
- `audio` and `video` - Provide access to audio and video devices.
- `plugdev` - Provides access to certain removable and connected devices.

Group membership is important in Linux security because permissions and
access to system resources can be granted to groups instead of individual
users.

### View System User Accounts

Command:

```bash
cut -d: -f1 /etc/passwd
```

### Example Result

```text
root
daemon
www-data
sshd
postgres
mysql
kali
```

### Explanation

The `/etc/passwd` file contains information about user accounts on the
Linux system. The `cut` command was used to extract only the username
field.

Not every account shown is a normal human user. Linux also uses system
and service accounts to run specific services with controlled privileges.

For example:

- `root` - The system administrator account.
- `www-data` - Commonly associated with web server processes.
- `sshd` - Associated with the SSH service.
- `postgres` - Associated with PostgreSQL.
- `mysql` - Associated with MySQL/MariaDB.
- `kali` - The normal user account used in this lab.

Using separate service accounts helps support the principle of least
privilege by limiting the permissions available to individual services.

### View a Specific User Account

Command:

```bash
grep '^kali:' /etc/passwd
```

### Result

```text
kali:x:1000:1000::/home/kali:/usr/bin/zsh
```

### Explanation

This command searches `/etc/passwd` for the account named `kali`.

The fields are separated by colons (`:`):

- `kali` - Username
- `x` - Indicates that password information is stored separately
- `1000` - User ID (UID)
- `1000` - Primary Group ID (GID)
- Empty field - User information/comment field
- `/home/kali` - User's home directory
- `/usr/bin/zsh` - User's login shell

This demonstrates how Linux stores basic account information and assigns
each user a UID, GID, home directory, and login shell.

### Check the Root User

Command:

```bash
id root
```

### Result

```text
uid=0(root) gid=0(root) groups=0(root)
```

### Explanation

The `root` account is the Linux superuser account.

- `uid=0` - Root has User ID 0.
- `gid=0` - Root has Group ID 0.
- `groups=0(root)` - Root belongs to the root group.

A normal user such as `kali` has a different UID, such as `1000`,
while the root account uses UID `0`.

The root account has extensive privileges, so administrative access
should be used carefully and only when required.

### Check the Root User

Command:

```bash
id root
```

### Result

```text
uid=0(root) gid=0(root) groups=0(root)
```

### Explanation

The `root` account is the Linux superuser account.

- `uid=0` - Root has User ID 0.
- `gid=0` - Root has Group ID 0.
- `groups=0(root)` - Root belongs to the root group.

A normal user such as `kali` has a different UID, such as `1000`,
while the root account uses UID `0`.

The root account has extensive privileges, so administrative access
should be used carefully and only when required.

### Check Sudo Privileges

Command:

```bash
sudo -l
```

### Result

```text
Matching Defaults entries for kali on kali:
    secure_path=/usr/sbin:/usr/bin:/sbin:/bin

User kali may run the following commands on kali:
    (ALL : ALL) ALL
```

### Explanation

The `sudo -l` command lists the commands that the current user is
allowed to execute using `sudo`.

The result:

```text
(ALL : ALL) ALL
```

shows that the `kali` user is permitted to run all commands through
`sudo` with elevated privileges.

This is important in Linux security because sudo permissions determine
which users can perform administrative operations. Excessive sudo
permissions can increase security risk, so privileged access should be
granted according to the principle of least privilege.

### Lab Conclusion

In this lab, I practiced Linux user and group management concepts using
commands such as `whoami`, `id`, `groups`, `cut`, `grep`, and `sudo -l`.

I learned how Linux identifies users using UIDs, organizes permissions
using groups and GIDs, stores basic account information in `/etc/passwd`,
and controls administrative access using sudo privileges.

Understanding users, groups, and privilege management is important for
Linux system administration and cybersecurity because these mechanisms
help control access to system resources.

### Check Sudo Privileges

Command:

```bash
sudo -l
```

### Result

```text
Matching Defaults entries for kali on kali:
    secure_path=/usr/sbin:/usr/bin:/sbin:/bin

User kali may run the following commands on kali:
    (ALL : ALL) ALL
```

### Explanation

The `sudo -l` command lists the commands that the current user is
allowed to execute using `sudo`.

The result:

```text
(ALL : ALL) ALL
```

shows that the `kali` user is permitted to run all commands through
`sudo` with elevated privileges.

This is important in Linux security because sudo permissions determine
which users can perform administrative operations. Excessive sudo
permissions can increase security risk, so privileged access should be
granted according to the principle of least privilege.

### Lab Conclusion

In this lab, I practiced Linux user and group management concepts using
commands such as `whoami`, `id`, `groups`, `cut`, `grep`, and `sudo -l`.

I learned how Linux identifies users using UIDs, organizes permissions
using groups and GIDs, stores basic account information in `/etc/passwd`,
and controls administrative access using sudo privileges.

Understanding users, groups, and privilege management is important for
Linux system administration and cybersecurity because these mechanisms
help control access to system resources.

---

## Lab 06 - Linux Processes and Services

### Objective

The objective of this lab is to understand Linux processes and services
and practice commands used to identify running processes and inspect
system activity.

### View Running Processes

Command:

```bash
ps
```
### Result

```text
PID TTY          TIME CMD
1952 pts/0    00:00:00 zsh
2240 pts/0    00:00:00 ps
```

### Explanation

The `ps` command displays processes associated with the current terminal
session.

- `PID` - Unique Process ID.
- `TTY` - Terminal associated with the process.
- `TIME` - CPU time used by the process.
- `CMD` - Name of the command or process.

In this result, `zsh` is the current shell and `ps` is the command used
to display the process information.

### View System-Wide Processes

Command:

```bash
ps -ef | head
```

### Result

```text
UID          PID    PPID  C STIME TTY          TIME CMD
root           1       0  0 12:21 ?        00:00:00 /sbin/init splash
root           2       0  0 12:21 ?        00:00:00 [kthreadd]
root           3       2  0 12:21 ?        00:00:00 [pool_workqueue_release]
root           4       2  0 12:21 ?        00:00:00 [kworker/R-rcu_gp]
root           5       2  0 12:21 ?        00:00:00 [kworker/R-sync_wq]
```

### Explanation

The `ps -ef` command displays running processes across the system in
full-format output. The `head` command limits the displayed output to
the first few lines.

Important fields include:

- `UID` - User that owns the process.
- `PID` - Process ID.
- `PPID` - Parent Process ID.
- `C` - CPU utilization information.
- `STIME` - Process start time.
- `TTY` - Associated terminal.
- `TIME` - CPU time used by the process.
- `CMD` - Command that started the process.

For example, PID `1` is the system initialization process, while entries
such as `kthreadd` and `kworker` represent kernel-related processes.

### Monitor Processes in Real Time

Command:

```bash
top
```

### Example Result

```text
Tasks: 177 total, 1 running, 176 sleeping, 0 stopped, 0 zombie

MiB Mem : 1969.1 total, 303.6 free, 779.4 used
MiB Swap: 953.7 total, 953.7 free, 0.0 used

PID   USER   %CPU   %MEM   COMMAND
611   root    3.7    7.8   Xorg
1916  kali    1.0    3.6   qterminal
```

### Explanation

The `top` command provides a real-time view of running processes and
system resource usage.

It can display:

- Number of running and sleeping processes
- CPU utilization
- Memory usage
- Swap usage
- Process IDs (PID)
- Process owners
- CPU usage per process
- Memory usage per process
- Running command names

The `q` key can be used to exit `top`.

This command is useful in system administration and cybersecurity for
monitoring system activity and identifying processes that consume
unusual amounts of CPU or memory.

### View Running Services

Command:

```bash
systemctl --type=service --state=running
```

### Example Result

```text
UNIT                           LOAD   ACTIVE SUB     DESCRIPTION
accounts-daemon.service        loaded active running Accounts Service
cron.service                   loaded active running Regular background program processing daemon
dbus.service                   loaded active running D-Bus System Message Bus
lightdm.service                loaded active running Light Display Manager
NetworkManager.service         loaded active running Network Manager
systemd-journald.service       loaded active running Journal Service
systemd-logind.service         loaded active running User Login Management
virtualbox-guest-utils.service loaded active running VirtualBox guest utils
```

### Explanation

The `systemctl` command is used to inspect and manage services on
systems that use systemd.

The options used in this command are:

- `--type=service` - Displays service units.
- `--state=running` - Displays only currently running services.
- `LOAD` - Indicates whether the service configuration was loaded.
- `ACTIVE` - Shows the general activation state.
- `SUB` - Shows the detailed service state.
- `DESCRIPTION` - Provides a description of the service.

Monitoring running services is important in cybersecurity because
unnecessary, unexpected, or unauthorized services may increase the
system's attack surface.

### Inspect a Specific Service

Command:

```bash
systemctl status NetworkManager --no-pager
```

### Example Result

```text
NetworkManager.service - Network Manager
Loaded: loaded (...; enabled; preset: enabled)
Active: active (running)
Main PID: 505 (NetworkManager)
Memory: 20M
CGroup: /system.slice/NetworkManager.service
        └─505 /usr/sbin/NetworkManager --no-daemon
```

### Explanation

The `systemctl status` command displays detailed information about a
specific systemd service.

In this example:

- `Loaded` - The NetworkManager service configuration was successfully loaded.
- `enabled` - The service is configured to start automatically.
- `Active: active (running)` - The service is currently running.
- `Main PID` - Identifies the main process associated with the service.
- `Memory` - Shows the memory being used by the service.
- `CGroup` - Shows the control group containing the service process.

NetworkManager is responsible for managing network connections on the
system. Checking service status is useful in system administration and
cybersecurity when investigating whether expected or unexpected services
are running.

### Find a Process by Name

Command:

```bash
pgrep -a NetworkManager
```

### Result

```text
505 /usr/sbin/NetworkManager --no-daemon
```

### Explanation

The `pgrep` command searches for running processes by name.

The `-a` option displays both the Process ID (PID) and the full command
associated with the matching process.

In this result:

- `505` - Process ID (PID)
- `/usr/sbin/NetworkManager` - NetworkManager executable
- `--no-daemon` - Command-line option used by the process

This command is useful for quickly identifying whether a specific
process is running and determining its PID.

### View the Process Tree

Command:

```bash
pstree -p | head -20
```

### Example Result

```text
systemd(1)-+-ModemManager(527)-+-{ModemManager}(535)
           |                   |-{ModemManager}(547)
           |                   `-{ModemManager}(550)
           |-NetworkManager(505)-+-{NetworkManager}(533)
           |                     |-{NetworkManager}(534)
           |                     `-{NetworkManager}(537)
           |-VBoxClient(1002)---VBoxClient(1004)
```

### Explanation

The `pstree` command displays running processes in a hierarchical tree
structure.

The `-p` option displays the Process ID (PID) of each process, while
`head -20` limits the displayed output to the first 20 lines.

The output shows parent-child relationships between processes. For
example, `systemd` has PID 1 and acts as the parent of many system
services.

Understanding process relationships is useful in cybersecurity when
investigating system activity and identifying processes started by other
processes.

### Lab Conclusion

In this lab, I practiced monitoring Linux processes and services using
commands such as `ps`, `ps -ef`, `top`, `systemctl`, `pgrep`, and
`pstree`.

I learned how to identify process IDs, process owners, parent-child
relationships, resource usage, and running system services.

Process and service monitoring is important in cybersecurity because it
can help identify unexpected processes, unauthorized services, abnormal
resource usage, and suspicious system activity.


---

## Lab 07 - Linux Networking Fundamentals

### Objective

The objective of this lab is to understand basic Linux networking and
practice commands used to inspect network interfaces, IP addresses,
routing information, and network connectivity.

### View Network Interfaces and IP Addresses

Command:

```bash
ip addr
```
### View Network Interfaces and IP Addresses

Command:

```bash
ip addr
```

### Example Result

```text
1: lo: <LOOPBACK,UP,LOWER_UP>
    inet 127.0.0.1/8

2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP>
    inet6 fe80::f8bf:8070:cd17:1564/64
```

### Explanation

The `ip addr` command displays the network interfaces and IP addresses
configured on the Linux system.

In this result:

- `lo` - The loopback interface used for communication with the local system.
- `127.0.0.1` - The IPv4 loopback address, also known as localhost.
- `eth0` - The Ethernet network interface.
- `UP` - Indicates that the network interface is enabled.
- `LOWER_UP` - Indicates that the interface has an active link.
- `inet` - Indicates an IPv4 address.
- `inet6` - Indicates an IPv6 address.
- `/8` and `/64` - Represent network prefix lengths.

The `eth0` interface currently shows an IPv6 link-local address but no
IPv4 address.

Inspecting network interfaces is important in cybersecurity because it
helps identify network connectivity, interface configuration, and the
addresses assigned to a system.

### View IPv4 Addresses Only

Command:

```bash
ip -4 addr
```

### Result

```text
1: lo: <LOOPBACK,UP,LOWER_UP>
    inet 127.0.0.1/8 scope host lo
```

### Explanation

The `ip -4 addr` command displays only IPv4 addresses configured on the
system.

In this result, only the loopback interface (`lo`) has an IPv4 address:

- `127.0.0.1` - IPv4 loopback address.
- `/8` - Network prefix length.
- `scope host` - The address is valid only within the local system.

The `eth0` interface does not currently have an IPv4 address assigned.
This indicates that IPv4 network configuration has not been completed
for that interface.

### View the IPv4 Routing Table

Command:

```bash
ip route
```

### Result

```text
No IPv4 routes were displayed.
```

### Explanation

The `ip route` command displays the IPv4 routing table used by Linux to
determine where network traffic should be sent.

In this test, no IPv4 routes were displayed. The `eth0` interface also
did not have an IPv4 address assigned.

Normally, a connected system may contain entries such as a local network
route and a default route through a gateway.

Checking the routing table is useful when troubleshooting network
connectivity and identifying how traffic is routed through a system.

### Check Network Device Status

Command:

```bash
nmcli device status
```

### Result

```text
DEVICE  TYPE      STATE                   CONNECTION
lo      loopback  connected (externally)  lo
eth0    ethernet  disconnected            --
```

### Explanation

The `nmcli device status` command displays the status of network devices
managed by NetworkManager.

In this result:

- `lo` is the loopback interface and is connected locally.
- `eth0` is the Ethernet interface.
- `disconnected` indicates that `eth0` is not currently connected to a
  network connection profile.
- `--` under CONNECTION indicates that no active NetworkManager
  connection is associated with `eth0`.

This explains why the `eth0` interface currently has no IPv4 address and
why no IPv4 route was displayed.

### View Network Connection Profiles

Command:

```bash
nmcli connection show
```

### Result

```text
NAME                TYPE
lo                  loopback
Wired connection 1  ethernet
```

### Explanation

The `nmcli connection show` command displays network connection profiles
configured in NetworkManager.

In this result:

- `lo` represents the loopback connection.
- `Wired connection 1` is an Ethernet connection profile.
- The Ethernet profile exists, but the `eth0` interface was previously
  shown as disconnected.

A connection profile contains network configuration that NetworkManager
can use when connecting an interface to a network.

### Inspect IPv4 Connection Configuration

Command:

```bash
nmcli -f connection.id,connection.interface-name,ipv4.method,ipv4.addresses,ipv4.gateway connection show "Wired connection 1"
```

### Result

```text
connection.id:              Wired connection 1
connection.interface-name:  eth0
ipv4.method:                auto
ipv4.addresses:             --
ipv4.gateway:               --
```

### Explanation

The connection profile is associated with the `eth0` network interface.

The `ipv4.method` value is set to `auto`, which means NetworkManager is
configured to obtain IPv4 network settings automatically, normally
using DHCP.

No static IPv4 address or gateway has been manually configured for this
connection profile.

### Check Ethernet Interface Link State

Command:

```bash
ip link show eth0
```

### Result

```text
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP>
    state UP
    link/ether 08:00:27:5a:87:bc
```

### Explanation

The `ip link show eth0` command displays link-layer information about
the `eth0` network interface.

In this result:

- `UP` - The interface is enabled.
- `LOWER_UP` - The underlying network link is available.
- `state UP` - The interface is operational at the link layer.
- `link/ether` - Displays the MAC address of the Ethernet interface.

The Ethernet link is available, but the earlier DHCP connection attempt
failed to obtain IPv4 configuration. Therefore, further investigation
of the DHCP/network configuration is required.

### Verify the IPv4 Address

Command:

```bash
ip -4 addr show eth0
```

### Result

```text
2: eth0: <BROADCAST,MULTICAST,UP,LOWER_UP>
    inet 10.0.2.15/24 brd 10.0.2.255 scope global dynamic eth0
```

### Explanation

The `eth0` interface successfully received an IPv4 address after the
VirtualBox network configuration was changed to NAT.

- `10.0.2.15` - IPv4 address assigned to the Kali Linux virtual machine.
- `/24` - Network prefix length.
- `10.0.2.255` - Broadcast address.
- `dynamic` - The IPv4 address was assigned automatically using DHCP.
- `scope global` - The address can be used for network communication
  beyond the local host.

This confirms that the Ethernet interface now has valid IPv4
configuration.

### Verify the Routing Table

Command:

```bash
ip route
```

### Result

```text
default via 10.0.2.2 dev eth0 proto dhcp src 10.0.2.15 metric 100
10.0.2.0/24 dev eth0 proto kernel scope link src 10.0.2.15 metric 100
```

### Explanation

The `ip route` command displays the system's IPv4 routing table.

In this result:

- `default via 10.0.2.2` - Traffic for networks without a more specific
  route is sent through the default gateway at `10.0.2.2`.
- `dev eth0` - The `eth0` interface is used for the route.
- `src 10.0.2.15` - The Kali Linux system uses this IPv4 address as the
  source address.
- `10.0.2.0/24` - Represents the directly connected IPv4 network.
- `proto dhcp` - The default route was obtained through DHCP.

This confirms that the system now has an IPv4 address and a valid
default route.

### Test Default Gateway Connectivity

Command:

```bash
ping -c 4 10.0.2.2
```

### Result

```text
4 packets transmitted, 4 received, 0% packet loss
rtt min/avg/max/mdev = 0.362/0.565/1.002/0.257 ms
```

### Explanation

The `ping` command was used to test connectivity between the Kali Linux
virtual machine and its default gateway.

The `-c 4` option instructs `ping` to send four ICMP Echo Request
packets.

In this test:

- `4 packets transmitted` - Four ICMP requests were sent.
- `4 received` - All four responses were received.
- `0% packet loss` - No packets were lost.
- `10.0.2.2` - The default gateway used by the virtual machine.

This confirms that the Kali Linux virtual machine can successfully
communicate with its default gateway.

### Test Internet IP Connectivity

Command:

```bash
ping -c 4 8.8.8.8
```

### Result

```text
4 packets transmitted, 4 received, 0% packet loss
rtt min/avg/max/mdev = 79.669/110.059/190.798/46.793 ms
```

### Explanation

The `ping` command was used to test connectivity to a public Internet
IP address.

In this test:

- `8.8.8.8` - A public IP address used for the connectivity test.
- `4 packets transmitted` - Four ICMP Echo Requests were sent.
- `4 received` - All four responses were received.
- `0% packet loss` - No packets were lost.

This confirms that the Kali Linux virtual machine has working IP
connectivity beyond its local network.

Testing an IP address directly is also useful when troubleshooting
because it can help distinguish general network connectivity problems
from DNS name-resolution problems.

### Test DNS Resolution

Command:

```bash
ping -c 4 google.com
```

### Result

```text
PING google.com (142.250.146.113)

4 packets transmitted, 4 received, 0% packet loss
rtt min/avg/max/mdev = 61.449/74.258/80.690/7.526 ms
```

### Explanation

The `ping` command was used with a domain name to test both DNS
resolution and network connectivity.

The domain name `google.com` was successfully resolved to an IP address,
which confirms that DNS name resolution is working.

The test also received responses to all four ICMP Echo Requests with
0% packet loss.

This confirms that the Kali Linux virtual machine has:

- A working network interface
- A valid IPv4 address
- A default gateway
- Internet connectivity
- Working DNS name resolution

DNS testing is important in network troubleshooting because a system
may have Internet connectivity while still being unable to resolve
domain names.

### View DNS Configuration

Command:

```bash
cat /etc/resolv.conf
```

### Result

```text
# Generated by NetworkManager
nameserver 10.0.2.3
nameserver fd17:625c:f037:2::3
```

### Explanation

The `/etc/resolv.conf` file contains DNS resolver configuration used by
the Linux system.

In this result:

- `nameserver 10.0.2.3` - IPv4 DNS resolver configured for the system.
- `nameserver fd17:625c:f037:2::3` - IPv6 DNS resolver.
- `Generated by NetworkManager` - Indicates that NetworkManager manages
  the DNS configuration automatically.

DNS servers translate domain names, such as `google.com`, into IP
addresses that computers can use for network communication.

Inspecting DNS configuration is useful in cybersecurity and network
troubleshooting when investigating name-resolution problems.

### Perform a DNS Lookup

Command:

```bash
nslookup google.com
```

### Example Result

```text
Server:         10.0.2.3
Address:        10.0.2.3#53

Non-authoritative answer:
Name:   google.com
Address: 142.250.146.100
Name:   google.com
Address: 142.250.146.113
Name:   google.com
Address: 2404:6800:4000:100e::64
```

### Explanation

The `nslookup` command is used to query DNS servers and resolve domain
names into IP addresses.

In this result:

- `10.0.2.3` - The DNS server used for the query.
- `#53` - DNS normally uses port 53.
- `google.com` - The domain name being resolved.
- Multiple IPv4 addresses were returned for the domain.
- Multiple IPv6 addresses were also returned.
- `Non-authoritative answer` means the response was provided by a DNS
  resolver rather than directly by the authoritative DNS server for
  the domain.

DNS lookup tools are useful in cybersecurity for network
troubleshooting, reconnaissance in authorized environments, and
investigating domain-name resolution.

### Check Listening Network Ports

Command:

```bash
ss -tuln
```

### Result

```text
Netid State Recv-Q Send-Q Local Address:Port Peer Address:Port
```

### Explanation

The `ss` command is used to inspect network sockets on a Linux system.

The options used are:

- `-t` - Display TCP sockets.
- `-u` - Display UDP sockets.
- `-l` - Display listening sockets only.
- `-n` - Display numerical IP addresses and port numbers.

In this test, no listening TCP or UDP sockets were displayed.

This means that, at the time of the test, no services matching these
options were listening on network ports.

Checking listening ports is important in cybersecurity because exposed
network services can increase the attack surface of a system.

### Identify a Listening TCP Port

A temporary local HTTP server was started using:

```bash
python3 -m http.server 8080 --bind 127.0.0.1
```

The listening TCP sockets were then checked using:

```bash
ss -tln
```

### Result

```text
State   Recv-Q  Send-Q  Local Address:Port  Peer Address:Port
LISTEN  0       5       127.0.0.1:8080      0.0.0.0:*
```

### Explanation

The result shows that a TCP service is listening on port `8080`.

- `LISTEN` - The socket is waiting for incoming TCP connections.
- `127.0.0.1` - The service is bound to the local loopback interface.
- `8080` - The TCP port used by the temporary HTTP server.
- `0.0.0.0:*` in the peer field indicates that there is no specific
  remote peer associated with the listening socket.

Because the server was bound to `127.0.0.1`, it is accessible only from
the local system and is not directly exposed through the `eth0`
interface.

This demonstrates how Linux networking tools can be used to identify
services that are listening on network ports.

### Stop the Temporary HTTP Server

The temporary HTTP server was stopped by pressing:

```text
Ctrl + C
```

### Result

```text
^C
Keyboard interrupt received, exiting.
```

### Explanation

`Ctrl + C` sends an interrupt signal to the foreground process running
in the terminal.

In this test, the Python HTTP server received the interrupt and
terminated successfully.

Stopping temporary services after testing is an important security
practice because unnecessary listening services can increase the attack
surface of a system.

### Verify the Port is Closed

Command:

```bash
ss -tln
```

### Result

```text
State  Recv-Q  Send-Q  Local Address:Port  Peer Address:Port
```

### Explanation

After stopping the temporary HTTP server, the `ss -tln` command was
used again to check listening TCP sockets.

Port `8080` was no longer displayed, confirming that the HTTP server
had stopped and the listening socket had been closed.

This demonstrates an important cybersecurity principle: temporary or
unnecessary network services should be stopped when they are no longer
required in order to reduce the system's attack surface.

### Trace the Network Path

Command:

```bash
traceroute 8.8.8.8
```

### Result

```text
traceroute to 8.8.8.8 (8.8.8.8), 30 hops max, 60 byte packets
1  10.0.2.2 (10.0.2.2)  0.348 ms  0.322 ms  0.309 ms
2  10.0.2.2 (10.0.2.2)  5.087 ms  5.077 ms  6.783 ms
```

### Explanation

The `traceroute` command is used to examine the network path toward a
destination.

In this test:

- `8.8.8.8` was used as the destination.
- `30 hops max` represents the maximum number of hops traceroute was
  configured to test.
- `10.0.2.2` is the VirtualBox NAT gateway used by the Kali Linux
  virtual machine.
- The time values shown in milliseconds represent round-trip timing
  measurements for traceroute probes.

In this virtualized NAT environment, the complete external network path
was not displayed. However, the result demonstrates how traceroute can
be used to investigate the path network traffic takes toward a
destination.

Traceroute is useful in network troubleshooting and cybersecurity for
investigating routing paths and locating connectivity problems.

### Lab Conclusion

In this lab, I practiced fundamental Linux networking commands and
learned how to inspect and troubleshoot network connectivity.

The practical activities included:

- Viewing network interfaces and IP addresses with `ip addr`
- Inspecting IPv4 configuration with `ip -4 addr`
- Viewing the routing table with `ip route`
- Checking NetworkManager status with `nmcli`
- Testing gateway connectivity with `ping`
- Testing Internet connectivity
- Verifying DNS resolution
- Inspecting DNS configuration
- Performing DNS lookups with `nslookup`
- Inspecting listening ports with `ss`
- Starting and stopping a temporary local HTTP service
- Tracing a network path with `traceroute`

During troubleshooting, the Kali Linux virtual machine initially failed
to obtain an IPv4 address through DHCP while using the VirtualBox
Bridged Adapter configuration. After changing the virtual network mode
to NAT, the `eth0` interface successfully received the dynamic IPv4
address `10.0.2.15/24`, a default route was installed through
`10.0.2.2`, and Internet and DNS connectivity were successfully
verified.

These networking skills are important for cybersecurity because they
provide the foundation for network reconnaissance, traffic analysis,
service identification, vulnerability assessment, and network
troubleshooting.







