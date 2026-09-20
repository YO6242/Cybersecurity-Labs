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
