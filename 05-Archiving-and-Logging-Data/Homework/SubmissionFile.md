## Week 5 Homework Submission File: Archiving and Logging Data

Please edit this file by adding the solution commands on the line below the prompt.

Save and submit the completed file for your homework submission.

---

### Step 1: Create, Extract, Compress, and Manage tar Backup Archives

1. Command to **extract** the `TarDocs.tar` archive to the current directory:
tar -xvf TarDoc.tar
2. Command to **create** the `Javaless_Docs.tar` archive from the `TarDocs/` directory, while excluding the `TarDocs/Documents/Java` directory:
tar -cf Javaless_Docs.tar --exclude "Java" ~/projects/TarDocs/Documents
3. Command to ensure `Java/` is not in the new `Javaless_Docs.tar` archive:
tar -tvf Javaless_Docs | grep "Java"
**Bonus** 
- Command to create an incremental archive called `logs_backup_tar.gz` with only changed files to `snapshot.file` for the `/var/log` directory:

#### Critical Analysis Question

- Why wouldn't you use the options `-x` and `-c` at the same time with `tar`?

--- it creates an error trying to make a tar archive and extract a archive at the same time

### Step 2: Create, Manage, and Automate Cron Jobs

1. Cron job for backing up the `/var/log/auth.log` file:

* 6 * * 3 sudo tar czf auth_backup.tgz auth.log.2.gz auth.log.3.gz auth.log.4.gz

### Step 3: Write Basic Bash Scripts

1. Brace expansion command to create the four subdirectories:
mkdir -p Backups/{freemem,diskuse,openlist,freedisk}
2. Paste your `system.sh` script edits below:

    ```bash
    #!/bin/bash

    #free memory
    free -mh >> ~/Desktop/Backups/freemem/freemem.txt

    #free disk
    df -h >> ~/Desktop/Backups/freedisk/freedisk.txt

    #disk use
    du -h >> ~/Desktop/Backups/diskuse/diskuse.txt

    #openlist
    sudo lsof >> ~/Desktop/Backups/openlist/openlist.txt
    ```

3. Command to make the `system.sh` script executable:
chmod +x system.sh
**Optional**
- Commands to test the script and confirm its execution:

**Bonus**
- Command to copy `system` to system-wide cron directory:

---

### Step 4. Manage Log File Sizes
 
1. Run `sudo nano /etc/logrotate.conf` to edit the `logrotate` configuration file. 

    Configure a log rotation scheme that backs up authentication messages to the `/var/log/auth.log`.

    - Add your config file edits below:
# see "man logrotate" for details
# rotate log files weekly
weekly

# use the syslog group by default, since this is the owning group
# of /var/log/syslog.
su root syslog

# keep 7 weeks worth of backlogs
rotate 7

# create new (empty) log files after rotating old ones
create

#don't rotate if log is empty
notifempty

# uncomment this if you want your log files compressed
nocompress

# packages drop log rotation information into this directory
include /var/log/auth.log

# system-specific logs may be configured here

    ```bash
   /var/log/wtmp {
    missingok
    weekly
    create 0664 root utmp
    rotate 7
}

/var/log/btmp {
    missingok
    weekly
    create 0660 root utmp
    rotate 7
}
    ```
---

### Bonus: Check for Policy and File Violations

1. Command to verify `auditd` is active:

2. Command to set number of retained logs and maximum log file size:

    - Add the edits made to the configuration file below:

    ```bash
    [Your solution edits here]
    ```

3. Command using `auditd` to set rules for `/etc/shadow`, `/etc/passwd` and `/var/log/auth.log`:


    - Add the edits made to the `rules` file below:

    ```bash
    [Your solution edits here]
    ```

4. Command to restart `auditd`:

5. Command to list all `auditd` rules:

6. Command to produce an audit report:

7. Create a user with `sudo useradd attacker` and produce an audit report that lists account modifications:

8. Command to use `auditd` to watch `/var/log/cron`:

9. Command to verify `auditd` rules:

---

### Bonus (Research Activity): Perform Various Log Filtering Techniques

1. Command to return `journalctl` messages with priorities from emergency to error:

1. Command to check the disk usage of the system journal unit since the most recent boot:

1. Comand to remove all archived journal files except the most recent two:


1. Command to filter all log messages with priority levels between zero and two, and save output to `/home/sysadmin/Priority_High.txt`:

1. Command to automate the last command in a daily cronjob. Add the edits made to the crontab file below:

    ```bash
    [Your solution cron edits here]
    ```

---
© 2020 Trilogy Education Services, a 2U, Inc. brand. All Rights Reserved.
