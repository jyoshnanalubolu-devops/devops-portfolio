# Day 3 – Linux Users, Groups & sudo

## Viewing Users and Groups
### view all users:
```bash
cat /etc/paswd
```
### view only normal (Human) users:
```bash
awk -F: '$3 >= 1000 {print $1}' /etc/passwd
```
### view all groups:
```bash
cat /etc/group
```

## Creating Users and Groups
### Create a Group:

```bash
sudo groupadd devops  (sudo groupadd nameOfTheGroup)
```

### Create a user with home directory and bash shell
```bash
sudo useradd -m -s /bin/bash appuser
```

### Set Password for the User:
```bash
sudo passwd appuser
```

### Verify User Creation:
```bash
id appuser
```

## Adding Users to Groups
### Add User to devops group:
```bash
sudo usermod -aG devops appuser
```

### Veryfying group membership:
```bash
groups appuser
```

### Switch to user:
```bash
su - appuser
```
### Exit back to original user:
```bash
exit
```


## sudo Access
### Check sudo permissions:
```bash
sudo -l
```

### Grant sudo access to user:
```bash
sudo usermod -aG sudo appuser
```

### Verify sudo access
```bash
su - appuser
sudo -l
```


## Real DevOps Scenario
### Problem:
Application user was unable to deploy files to the application directoryr due to permission issues.
### Root Cause:
The application user was not part of the deployment group and lacked write permissions.
### Fix
```bash
sudo groupadd deploy
sudo usermod -aG deploy appuser
sudo chown -R root:deploy /var/www/app
sudo chmod -R 775 /var/www/app
