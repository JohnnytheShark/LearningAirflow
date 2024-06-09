# Scheduling DAGs

## CRON
Cron is a time-based job scheduler used by Unix-like computer operating systems such as macOS and Linux.
Understanding CRON based intervals: 

┌─────── minute (0 - 59)
│ ┌────── hour (0 - 23)
│ │ ┌───── day of the month (1 - 31)
│ │ │ ┌───── month (1 - 12)
│ │ │ │ ┌──── day of the week (0 - 6) (Sunday to Saturday; 7 is also Sunday on some systems)
│ │ │ │ │
* * * * *

Examples: 
0 * * * * = hourly (running on the hour) 
0 0 * * * = daily (running at midnight)
0 0 * * 0 = weekly (running at midngith on Sunday) 
45 23 * * SAT = 23:45 every Saturday
0 0 * * MON, WED, FRI = run every Monday, Wednesday, Friday at midnight 

0 0 * * MON-FRI = run everyday at midnight 

0 0,12 * * * = run every day at 00:00 and 12:00

Airflow also provides support for several macros that represent shorthand for commonly used scheduling intervals. 