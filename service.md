# SFTP, SCP, and Systemd Service File for Spring PetClinic

# 1. What is SCP?

## Definition
SCP (Secure Copy Protocol) is used to securely copy files or directories between two Linux systems over SSH.

- Uses SSH (Port 22)
- Secure and encrypted
- Mainly used for copying files
- Does not provide an interactive file browser

## Syntax

```bash
scp source destination
```

## Examples

### Copy local file to remote server

```bash
scp app.jar ubuntu@192.168.1.100:/home/ubuntu/
```

### Copy remote file to local machine

```bash
scp ubuntu@192.168.1.100:/home/ubuntu/app.jar .
```

### Copy directory

```bash
scp -r project ubuntu@192.168.1.100:/home/ubuntu/
```

### Specify SSH Key

```bash
scp -i mykey.pem app.jar ec2-user@10.0.0.10:/opt/apps/
```

---

# 2. What is SFTP?

## Definition

SFTP (SSH File Transfer Protocol) is an interactive file transfer protocol that works over SSH.

Features

- Secure
- Interactive shell
- Upload files
- Download files
- Rename
- Delete
- Create directories

Uses Port 22

---

## Connect

```bash
sftp ubuntu@192.168.1.100
```

---

## Common Commands

### Show current remote directory

```bash
pwd
```

### Show local directory

```bash
lpwd
```

### List remote files

```bash
ls
```

### List local files

```bash
lls
```

### Upload file

```bash
put app.jar
```

### Upload directory

```bash
put -r project
```

### Download file

```bash
get app.jar
```

### Download directory

```bash
get -r logs
```

### Change remote directory

```bash
cd /opt/apps
```

### Change local directory

```bash
lcd Downloads
```

### Exit

```bash
bye
```

---

# SCP vs SFTP

| Feature | SCP | SFTP |
|----------|------|------|
| Secure | Yes | Yes |
| Uses SSH | Yes | Yes |
| Interactive | No | Yes |
| Upload | Yes | Yes |
| Download | Yes | Yes |
| Rename Files | No | Yes |
| Delete Files | No | Yes |
| Browse Directories | No | Yes |
| Automation | Excellent | Good |

---

# When to Use

## Use SCP

- Copy one or more files
- Automation scripts
- CI/CD deployment
- Fast file transfer

Example

```bash
scp app.jar ubuntu@server:/opt/apps/
```

---

## Use SFTP

- Manual upload/download
- File management
- Browse remote directories

Example

```bash
sftp ubuntu@server
```

---

# 3. What is a Systemd Service?

Systemd manages Linux services.

Instead of manually running

```bash
java -jar app.jar
```

Create a service so Linux starts the application automatically.

Benefits

- Auto restart
- Auto start after reboot
- Easy management
- Logging with journalctl

---

# Spring PetClinic Service File

Location

```text
/etc/systemd/system/spring-petclinic.service
```

Sample

```ini
[Unit]
Description=Spring PetClinic Application
After=network.target

[Service]
Type=simple

User=ubuntu
Group=ubuntu

WorkingDirectory=/opt/spring-petclinic

ExecStart=/usr/bin/java -jar /opt/spring-petclinic/spring-petclinic.jar

SuccessExitStatus=143

Restart=always
RestartSec=10

Environment=SPRING_PROFILES_ACTIVE=prod

[Install]
WantedBy=multi-user.target
```

---

# Service File Sections

## [Unit]

Contains service description and dependencies.

Example

```ini
[Unit]
Description=Spring PetClinic
After=network.target
```

---

## [Service]

Contains application details.

### User

```ini
User=ubuntu
```

Runs the application as ubuntu user.

---

### Working Directory

```ini
WorkingDirectory=/opt/spring-petclinic
```

Application directory.

---

### ExecStart

```ini
ExecStart=/usr/bin/java -jar /opt/spring-petclinic/spring-petclinic.jar
```

Command to start the application.

---

### Restart Policy

```ini
Restart=always
RestartSec=10
```

Automatically restarts after failure.

---

### Environment Variables

```ini
Environment=SPRING_PROFILES_ACTIVE=prod
```

Pass Spring Boot profile.

---

# Reload Systemd

Whenever a new service is created

```bash
sudo systemctl daemon-reload
```

---

# Enable Service

Starts automatically after reboot.

```bash
sudo systemctl enable spring-petclinic
```

---

# Start Service

```bash
sudo systemctl start spring-petclinic
```

---

# Stop Service

```bash
sudo systemctl stop spring-petclinic
```

---

# Restart Service

```bash
sudo systemctl restart spring-petclinic
```

---

# Check Status

```bash
sudo systemctl status spring-petclinic
```

---

# View Logs

```bash
journalctl -u spring-petclinic -f
```

---

# Disable Service

```bash
sudo systemctl disable spring-petclinic
```

---

# Real Deployment Flow

```
Developer
    │
    ▼
Build Spring Boot Project
    │
    ▼
Generate spring-petclinic.jar
    │
    ▼
Copy JAR using SCP
    │
    ▼
scp spring-petclinic.jar ubuntu@server:/opt/spring-petclinic/
    │
    ▼
SSH to Server
    │
    ▼
Restart Service
    │
    ▼
systemctl restart spring-petclinic
    │
    ▼
Check Status
    │
    ▼
systemctl status spring-petclinic
    │
    ▼
View Logs
    │
    ▼
journalctl -u spring-petclinic -f
```

---

# Interview Questions

### What is the difference between SCP and SFTP?

SCP is used for secure file copying, while SFTP provides an interactive file transfer session with file management capabilities.

---

### Why use a Systemd service?

- Automatic startup after reboot
- Automatic restart on failure
- Centralized logging
- Easy service management

---

### Which port is used by SCP and SFTP?

Both use **SSH Port 22**.

---

### Why run Spring Boot as a service?

To ensure the application runs in the background, starts automatically on boot, restarts after failures, and can be managed easily using `systemctl`.