Tool description:
-----------------
This is a bash cron job to do backup specified directories/files running on Linux server.

Currently it works well for my Linux PC (with ubuntu 16 and Windows OS installed). The backup will do the following two steps:
    step 1 - will backup to a directory residing on Linux. It will only contain the latest backup in 30 days 
    step 2 - will backup to a disk shared cross-mounted between Linux and windows. It will contain all backup, if the disk usage run above
80%, an error will be reported. 

Source tools (these scripts under installation directory):
-----------------------------------------------------------------------
backup.scr:
          Backup script, will read bkup.list and do all the backup work. Need add to cron job by crontab -e.
bkup.list:
          Configure file, all directories/files to be backup'ed need to be specified in this file.
cleanup.scr:
          Clean up old backup files (more than 30 days) in directory specified for step 1. Need add to cron job by crontab -e.

log (under directory specified by step 1)
------------------------------------------
backup.log 

Debugging (do it under directory  specified by step 1)
------------------------------------------------------
touch .debug_backup

To-do items:
------------
For step 2, see whether mount/umount is needed to seperate the step2 Disk from LINUX once backup is done. In this way, the step 2 Disk 
should not be impacetd even if any corruptpion happened in LINUX enviornment.

There are following to-do items to make it portable for others to use:
----------------------------------------------------------------------
1. Make step1 and step2 configurable by users.
2. Create an install script to do
         - Read LOGIN from LINUX environment.
         - Gathe user's input for installation directory
         - Gather user's input for backup directories (step 1 and/or step 2).
