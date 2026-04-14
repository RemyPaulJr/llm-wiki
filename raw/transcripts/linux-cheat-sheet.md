# Linux Commands Reference

## Network

Check current IP address and network interfaces.
```bash
ip addr
```

Check current gateway and routing table.
```bash
ip route
```

## Hostname

Change the machine's hostname permanently.
```bash
sudo hostnamectl set-hostname <name>
```

Display the current hostname.
```bash
hostname
```

## Users & Groups

Create a new user with a home directory and password.
```bash
sudo adduser <username>
```

Add a user to the sudo group, granting admin privileges.
```bash
sudo usermod -aG sudo <username>
```

List all groups a user belongs to.
```bash
groups <username>
```

List all users on the system.
```bash
cut -d: -f1 /etc/passwd
```

List all groups on the system.
```bash
cat /etc/group
```

List all users in a specific group.
```bash
getent group <groupname>
```

Delete a user and their home directory.
```bash
sudo deluser --remove-home <username>
```

Kill all processes belonging to a specific user.
```bash
sudo pkill -u <username>
```

## Processes

Display information about a specific process by PID.
```bash
ps -p <pid>
```

Forcefully kill a specific process by PID.
```bash
sudo kill -9 <pid>
```

## Permissions

Verify that the current user has working sudo privileges.
```bash
sudo whoami
```
