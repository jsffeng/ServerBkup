Tool description:   
-----------------   
The bash scripts will do backup for specified directories/files on Linux server. Ideally, it can be   
configured as cronjob.   
  
Currently they work well for my own Linux PC (with ubuntu 16 and Windows OS installed). The backup   
will do the following two steps:  
- step-1: will backup to a directory residing on Linux. It will only contain the latest backup in 30 days  
- step-2: will backup to a disk shared cross-mounted between Linux and windows. It will contain all history  
 backup, if the disk usage run above 80%, an error will be printed to log file.

There are a few of alternatives to handle error notification in log file. For example, create another cronjob    
to screen log file every day and send emails if any errors. In my practice, I just created a simple tool to screen   
log file and added it into my $HOME/.profile. In this way, I will see the errors in the screen if exist whenever       
I log into my PC/system.    

Source files:  
-------------   
These sources should be put into your installation directory.   
- backup.scr:    
Backup script, will read bkup.list and do all the backup work. Can be added to cron jobs by "crontab -e".    
- bkup.list:  
All directories/files to be backup'ed need to be specified in this file.  
- cleanup.scr:      
Clean up old backup files (more than 30 days) in directory specified by step-1. Can be added to cron jobs  
 by "crontab -e".   
          
Output files:  
-------------  
*\<date\>.tar.gz file will be created with containing all backup files/directories. It can be stored in  
two places as mentioned above: step-1 directory or/and step-2 Disk.   

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
- Need to evaluate whether mount/umount is needed so as to separate the Disk (used by step-2) from LINUX after  
 backup is done. With mount/umount implemented, the Disk involved in step-2 should not be impacted even if   
 any corruption happened in LINUX environment. However, this may require root permission. Alternatively,   
users can create a separate cron job for root login to mount/umount step-2 Disk as scheduled.  
  
- Make it more user-friendly for others' use (for general backup purpose)   
	- Enhance scripts to make step-1 and step-2 configurable by end-users.
	- Create an installation script to help users to use:   
		- Read LOGNAME from LINUX environment.   
		- Gather user's input for installation directory.  
		- Gather user's input for backup directories (step-1's, and/or step-2's).   


