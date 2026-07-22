# What is Linux?

## Definition

**Linux** is a free, open-source operating system (OS) based on the **Linux Kernel**, created by **Linus Torvalds** in 1991. It manages computer hardware resources and provides a platform for running applications.

Linux is widely used in:
- Cloud Computing (AWS, Azure, GCP)
- DevOps
- Web Servers
- Databases
- Kubernetes
- Docker
- Android
- Supercomputers

---

# What is the Linux Kernel?

The **Kernel** is the core component of Linux. It acts as a bridge between applications and the computer hardware.

The kernel is responsible for:
- Process management
- Memory management
- File system management
- Device management
- Networking
- Security

Without the kernel, Linux cannot function.

---

# Linux Architecture

```text
+----------------------------------+
|         User                     |
+----------------------------------+
               │
               ▼
+----------------------------------+
|     Application Software         |
| Chrome | Docker | Git | Jenkins  |
+----------------------------------+
               │
               ▼
+----------------------------------+
|        Shell (Bash)              |
|  Accepts user commands           |
+----------------------------------+
               │
               ▼
+----------------------------------+
|        Linux Kernel              |
| Process | Memory | Network | FS  |
+----------------------------------+
               │
               ▼
+----------------------------------+
|           Hardware               |
| CPU | RAM | Disk | NIC | USB     |
+----------------------------------+
```

---

# How Linux Works

Let's understand the flow with an example.

Suppose you type:

```bash
ls
```

### Step 1: User

The user enters the command:

```bash
ls
```

---

### Step 2: Shell

The shell (Bash) receives the command.

It checks:
- Is the command valid?
- Where is the `ls` executable?

Example:

```text
/usr/bin/ls
```

The shell starts a new process.

---

### Step 3: Kernel

The shell sends a **system call** to the Linux kernel.

The kernel:
- Reads the current directory
- Accesses the file system
- Retrieves filenames
- Checks user permissions

---

### Step 4: Hardware

The kernel communicates with:
- Disk controller
- SSD/HDD
- CPU
- RAM

It reads the required data from storage.

---

### Step 5: Return Data

The kernel sends the file list back to the shell.

---

### Step 6: Display Output

The shell prints the result.

```text
file1.txt
notes.md
images/
Downloads/
```

---

# Linux Command Flow

```text
User
  │
  ▼
Types: ls
  │
  ▼
Shell (Bash)
  │
  ▼
System Call
  │
  ▼
Linux Kernel
  │
  ▼
File System
  │
  ▼
Disk / SSD
  │
  ▼
Kernel
  │
  ▼
Shell
  │
  ▼
User Output
```

---

# Internal Working of Linux

## 1. Process Management

Every running program becomes a **process**.

Examples:
- Chrome
- Docker
- Jenkins
- Nginx

The kernel:
- Creates processes
- Schedules CPU time
- Terminates processes

Commands:

```bash
ps -ef
top
kill <PID>
```

---

## 2. Memory Management

Linux allocates RAM for each process.

Example:

```text
Chrome  → 2 GB
Docker  → 1 GB
VS Code → 800 MB
```

The kernel ensures one process cannot directly access another process's memory.

---

## 3. File System Management

Linux stores almost everything as files.

Examples:

```text
/etc
/home
/var
/dev
/proc
```

The kernel:
- Creates files
- Deletes files
- Reads files
- Writes files
- Applies permissions

---

## 4. Device Management

Hardware devices communicate with Linux through **device drivers**.

Examples:
- Keyboard
- Mouse
- USB
- Network Card
- Printer

Device files are located under:

```text
/dev
```

---

## 5. Networking

The kernel manages:
- IP addresses
- TCP/UDP
- Routing
- Firewalls
- Network interfaces

Commands:

```bash
ip addr
ping google.com
ssh user@server
```

---

## 6. Security

Linux provides:
- User accounts
- Groups
- File permissions
- SELinux/AppArmor (depending on distribution)
- Authentication

Example:

```text
-rwxr-x---
```

Permission meaning:

- Owner → Read, Write, Execute
- Group → Read, Execute
- Others → No access

---

# Linux Boot Process

```text
Power ON
      │
      ▼
BIOS / UEFI
      │
      ▼
GRUB Boot Loader
      │
      ▼
Linux Kernel
      │
      ▼
Initialize Device Drivers
      │
      ▼
Mount Root File System
      │
      ▼
Start systemd
      │
      ▼
Start Services
      │
      ▼
Login Prompt
```

---

# Real-World Example

Suppose you open **Google Chrome** on Linux.

```text
You click Chrome
      │
      ▼
Desktop launches Chrome
      │
      ▼
Shell/Desktop requests Kernel
      │
      ▼
Kernel creates Chrome process
      │
      ▼
Kernel allocates RAM
      │
      ▼
Kernel loads Chrome files from Disk
      │
      ▼
CPU executes instructions
      │
      ▼
Chrome window appears
```

---

# Why Linux is Popular

- Open source and free
- Stable and reliable
- Secure
- Excellent performance
- Multi-user support
- Multitasking
- Highly customizable
- Preferred for servers and cloud platforms

---

# Linux in DevOps

Linux is the foundation of most DevOps environments because tools such as:
- Docker
- Kubernetes
- Jenkins
- Git
- Ansible
- Terraform
- Nginx
- Apache

run primarily on Linux servers.

Cloud providers like AWS, Azure, and GCP also commonly use Linux for virtual machines and managed services.

---

# Interview Questions

1. What is Linux?
2. What is the Linux kernel?
3. How does Linux process a command?
4. What is a system call?
5. What is the difference between the shell and the kernel?
6. How does Linux manage memory?
7. What are device drivers?
8. Explain the Linux boot process.
9. Why is Linux preferred in cloud computing?
10. How does Linux improve security?

---

# Summary

- Linux is an open-source operating system built around the Linux kernel.
- The shell accepts user commands and sends system calls to the kernel.
- The kernel manages hardware resources such as CPU, memory, storage, devices, and networking.
- Applications interact with hardware through the kernel, not directly.
- Linux is widely used in servers, cloud computing, containers, DevOps, and embedded systems because of its stability, security, and performance.