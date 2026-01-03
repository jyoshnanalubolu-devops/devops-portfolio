# Day 2 – Linux File Permissions & Ownership

## 1. Understanding Linux Permissions
Linux has 3 types of permissions:
- r → read
- w → write
- x → execute

And 3 entities:
- User (u)
- Group (g)
- Others (o)

---

## 2. Viewing Permissions
```bash
ls -l

## 3. Chmod Examples
```bash
chmomd 755 script.sh
chmod u+x script.sh
chmod g-w file.txt

## 4. Ownership Commands
```bash
chown user:group file.txt
chgrp devops file.txt

## 5.Umask 
- umask defines the default permission values for newly created files and directories.
- It works bby subtracting permissions from the system default.
### Default Permissions
- Files -> 666 (rw-rw-rw-)
- Directories -> 777 (rrwxrwxrwx)

### check current umask
```bash
umask

### umask Example
```bash
umask 027
touch secure.txt
mkdir secure-dir
ls -l

## Real DevOps Scenario

An application failed to write logs due to permission issues.

### Fix
```bash
chown appuser:appgroup /var/log/app
chmod 775 /var/log/app
