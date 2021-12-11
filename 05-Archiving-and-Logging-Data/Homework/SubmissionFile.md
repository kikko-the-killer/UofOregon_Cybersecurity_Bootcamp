## Week 5 Homework Submission File: Archiving and Logging Data

Please edit this file by adding the solution commands on the line below the prompt.

Save and submit the completed file for your homework submission.

---

### Step 1: Create, Extract, Compress, and Manage tar Backup Archives

1. Command to **extract** the `TarDocs.tar` archive to the current directory:
tar xvf TarDocs.tar


2. Command to **create** the `Javaless_Doc.tar` archive from the `TarDocs/` directory, while excluding the `TarDocs/Documents/Java` directory:
sudo tar -cvf Javaless_Docs.tar --exclude=Java TarDocs/Documents

3. Command to ensure `Java/` is not in the new `Javaless_Docs.tar` archive:
tar list -f Javaless_Docs.tar | grep "java*"

**Bonus** 
- Command to create an incremental archive called `logs_backup_tar.gz` with only changed files to `snapshot.file` for the `/var/log` directory:
sudo tar -cvfz logs_backup.tar.gz --listed-incremental=logs_backup.snar --level=1 /var/log

#### Critical Analysis Question

- Why wouldn't you use the options `-x` and `-c` at the same time with `tar`?
Using -x extracts a tar file while -c creates one.  This is illogical to Bash as a tar file would have to be created before compression and only then extracted from.  However, you could use -c and -z together at thee same time to create and compress a tar file.
---

### Step 2: Create, Manage, and Automate Cron Jobs

1. Cron job for backing up the `/var/log/auth.log` file:
06**3sudo tar -cvfz /var/log/auth.log /auth_backup.tar.gz
---

### Step 3: Write Basic Bash Scripts

1. Brace expansion command to create the four subdirectories:
mkdir -p ~/backups/{freemem,diskuse,openlist,freedisk}
2. Paste your `system.sh` script edits below:

    ```bash
    #!/bin/bash

    free -h > ~/backups/freemem/free_mem.txt

    df-h > ~/backups/diskuse/disk_usage.txt

    lsof > ~/backups/openlist/openlist.txt

    du -h > ~/backups/freedisk/free_disk.txt

    [Your solution script contents here]
    ```

3. Command to make the `system.sh` script executable:

sudo chmod +x system.sh

**Optional**
- Commands to test the script and confirm its execution:
sudo ./system.sh

cd backups/freedisk
cat free_disk.txt

**Bonus**
- Command to copy `system` to system-wide cron directory:
sudo cp system.sh /etc/cron.weekly
---

### Step 4. Manage Log File Sizes
 
1. Run `sudo nano /etc/logrotate.conf` to edit the `logrotate` configuration file. 

    Configure a log rotation scheme that backs up authentication messages to the `/var/log/auth.log`.

    - Add your config file edits below:

 

    # Compress log files (uncommented to activate compression)
    Compress

    #packages drop log rotation into this directory
    include /var/log/auth.log
    ```
---!bin/bash

/var/log/auth.log {
    rotate 30
    weekly
    notifempty
    compress
    delaycompress
    missingok
    endscript
}


### Bonus: Check for Policy and File Violations

1. Command to verify `auditd` is active:

systemctl status

2. Command to set number of retained logs and maximum log file size:

sudo nano /etc/audit/rules.d/audit.rules


    - Add the edits made to the configuration file below:

max_log_file = 35
num_logs = 7


3.
    ```bash
    [Your solution edits here]
    ```
    -w /etc/shadow -p wra -k hashpasss_audit

    -w /etc/passwd -p wra -k userpass_audit

    -w /var/log/auth.log -pwra -k authlog_audit


    [Your solution edits here]
    ```

4. Command to restart `auditd`:
sudo systemctl restart auditd

5. Command to list all `auditd` rules:
sudo auditctl -l

6. Command to produce an audit report:

aureport

7. Create a user with `sudo useradd attacker` and produce an audit report that lists account modifications:
aureport -made


8. Command to use `auditd` to watch `/var/log/cron`:
sudo auditctl -w /var/log/cron

9. Command to verify `auditd` rules:
sudo auditctl -l
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
