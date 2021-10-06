# Logs and Queues

## Logs
There is a _/var/log_ dir!!!

### Some files
- Inside the dir you can check _dmesg_ for info on start.
- check _lastlog_ by running `last` for login info.
- in _messeges_ you have more info on start and login failures (httpd or apache have their own dir for their stuff)
- in _secure_ you have more login attempts.
- inside _audit/audit_ you see SELinux audit info - useful for troubleshooting problems

To read log files in real time you can do: `tail -f [logfile]`

Logs can be changed - you kinda don't want unless you are a bad hacker guy xD

### Managing logs
- Rotate logs?
    - It takes log files, and every x time it will take the exixting log files and move it to another file with a number extension and clean the current. This allows for deleting logs x period long. And also for not creating a super looooong log file.
    - _LogWatch_ automatically checks logs and emails you if somehting doesn't look right.
    - Logs can also be stored elsewhere (or even receive logs) - syslogs programs do that

## Queues
Spool - is feeding something through something - passing things through (from a to b to c to ... z).

In _var/spool_ _mail_ and _postfix_ dirs are really important as many system activities require mail.
Print jobs are in _cups_ directories (for printers) so they can also be important.