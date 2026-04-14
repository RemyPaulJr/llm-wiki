# Linux Process Management

**Summary**: Tools and commands for monitoring and controlling system processes in Linux.
**Tags**: #linux #processes #administration
**Created**: 2026-04-13

---
## Content

### Viewing Processes
Display information about a specific process by PID:
```bash
ps -p <pid>
```

Display all processes belonging to a specific user:
```bash
ps -u <username>
```

### Terminating Processes
Forcefully kill a specific process by PID:
```bash
sudo kill -9 <pid>
```

## Related Notes
- [[linux-user-management]]

## Sources
- raw/transcripts/linux-cheat-sheet.md
