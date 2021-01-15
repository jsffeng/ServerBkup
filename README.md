Tool Usage: 
-----------------   
- Put bkup.list to your $HOME, and add directories into it.   
- Edit backup.scr for remote PC login, ip and directory     
- Manual run backup.scr and cleanup.scr, verify backup successful   
- Install backup.scr and cleanup.scr to be your cronjob   

Tool description:   
-----------------   
The bash scripts will do backup for specified directories/files on Linux server to a remote PC or server.     
It is designed to work as a cronjob.    
  
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
- Remote directory disk monitoring and notification
