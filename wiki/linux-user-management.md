# Linux User Management

**Summary**: Commands and files for managing users, groups, and permissions on a Linux system.
**Tags**: #linux #users #groups #administration
**Created**: 2026-04-13

---
## Content

### User Operations
- Create a new user with a home directory and password:
  ```bash
  sudo adduser <username>
  ```
- Delete a user and their home directory:
  ```bash
  sudo deluser --remove-home <username>
  ```
- Kill all processes belonging to a specific user:
  ```bash
  sudo pkill -u <username>
  ```

### Group Operations
- Add a user to the `sudo` group:
  ```bash
  sudo usermod -aG sudo <username>
  ```
- List all groups a user belongs to:
  ```bash
  groups <username>
  ```
- List all users in a specific group:
  ```bash
  getent group <groupname>
  ```

### System Listings
- List all users on the system:
  ```bash
  cut -d: -f1 /etc/passwd
  ```
- List all groups on the system:
  ```bash
  cat /etc/group
  ```

## Related Notes
- [[linux-sudo]]
- [[linux-process-management]]

## Sources
- raw/transcripts/linux-cheat-sheet.md
