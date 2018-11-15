Tool description:   
-----------------   
The bash scripts will do backup for specified directories/files on Linux server. Ideally, it can be configured as cronjob.   

Currently it works well for my own Linux PC (with ubuntu 16 and Windows OS installed). The backup will do the following two steps:  
  step-1: will backup to a directory residing on Linux. It will only contain the latest backup in 30 days  
  step-2: will backup to a disk shared cross-mounted between Linux and windows. It will contain all backup, if the disk usage run above   80%, an error will be reported.   

Source files:  
-------------   
These sources should be put into your installation directory.  
  backup.scr - executable script:  
       Backup script, will read bkup.list and do all the backup work. Can be added to cron jobs by "crontab -e".  
  bkup.list - Data configuratin file:    
       All directories/files to be backup'ed need to be specified in this file.
  cleanup.scr - executable script:      
       Clean up old backup files (more than 30 days) in directory specified by step-1. Can be added to cron jobs by "crontab -e".  
          
Output files:  
-------------  
*<date>.tar.gz file will be created with containing all backup files/directories. It can be stored in two places as mentioned above: step-1 directory or/and step-2 Disk.  

Logging:     
--------   
Log will be stored at the directory specified by step-1, named as backup.log   

Debugging:   
----------   
In the directory specified by step-1, run the following command:   
touch .debug_backup
Debugging information will be saved to backup.log once the cron job got invoked.   

To-do items:
------------
For step-2, need to evaluate whether mount/umount is needed to seperate the step-2 Disk from LINUX once backup is done. In this way, the Disk involved in step-2 should not be impacetd even if any corruptpion happened in LINUX enviornment. However, this may require root permission. Alternatively, create a seperate cron job for root login, this is optional for users and can mount/umount step-2 Disk as schedule if needed.

More to-do items to make it portable for others to use:  
-------------------------------------------------------  
1. Make step-1 and step-2 configurable by users.
2. Create an installation script to do:  
      - Read LOGIN from LINUX environment.  
      - Gather user's input for installation directory.  
      - Gather user's input for backup directories (step-1 and/or step-2).  
