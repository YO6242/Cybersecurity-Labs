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








