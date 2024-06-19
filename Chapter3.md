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

## CRON MACROS 

| MACRO | Definition | 
| --- | --- | 
| @once | Scheduler once and only once | 
| @hourly | Run once an hour at hte beginning of the hour. | 
| @daily | Run once a day at midnight | 
| @weekly | Run once a week at midnight on Sunday Morning | 
| @monthly | Run once a month at midnight on the first day of the month. | 
| @yearly | Run once a year at midnight on January 1. | 

## Limitations 
Frequency, challenges if you wanted your DAG to run every 3 days. Since you don't know when the last run was you run into issues.

To run in intervals in Airflow you can pass a timedelta instance as a schedule interval

### Example: 
    dag = DAG (
        dag_id = "04_time_delta",
        schedule_interval=dt.timedelta(days=3),
        start_date=dt.datetime(year=2019,month=1,day=1),
        end_date=dt.datetime(year=2019,month=1,day=5),
    )

This would result in our DAG being run every three days following the start date. On the 4th, 7th, and 10th

## Processing Data Incrementally: 
Depending on your API, you may need to adjust how you are retreiving data. For the example in this chapter the API allowed for a start and end date to be included and we could adjust it as such in our python code. 

Execution_date = represents the date and time for which our DAG is being executed. This parameter is not a date rather a timestamp. Airflow also provides a previous_execution_date parameter which describes the start of the previous schedule interval.

## Syntax JINJA 
{{variable_name}} Jinja-based templating syntax for referencing one of Airflow's specific parameters.

## Shorthand Notation for dates: 
ds, next_ds, next_ds_nodash, prev_ds, prev_ds_nodash
translating to execution_date datestamp (YYYY-MM-DD) and no_dash (YYYYMMDD)

Caveat to keep in mind is that previous_execution_date and next_execution_date only work for DAG runs following a schedule interval. Manual runs will not have this.

## Partitioning 
Diving data sets into smaller more manageable pieces is a common strategy in data storage and processing systems.

## Backfilling 

By default, AIrflow will schedule and run any past schedule intervals that have not been run. To disable this feature you pass the parameter: catchup=False

With this setting, the DAG will only be run for the most recent schedule interval rather than executing all open intervals.

Backfilling is great but limited to the data in source systems. Backfilling can also be used to reprocess data after we have made changes in our code. 

## Best Practices: 
### Atomicity 
An atomic transaction is considered an indivisible and irreducible series of database operations such that either all occur or nothing occurs. 

Airflow tasks should follow this and will either all succeed and produce result or fail in a manner that does not affect the state of the system. No half work is produced. 

In simple terms for atomicity it is the reliance of being able to write cleaner code, and that a task accomplishes one task and that each task is independent of one another. This allows for us to be able to determine where something is broken or failing better. Splitting tasks truly depends on the dependencies of each task on one another. Logging in and fetching data while they seem can be done one by one it might just be better to combine the tasks together.

### Idempotency 
Idempotency - Basically when calling the same task mutlitiple times with the same inputs has no additional effect. It produces the same result, no matter how many times you run it.




