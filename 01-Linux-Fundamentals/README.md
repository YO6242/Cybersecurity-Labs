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


