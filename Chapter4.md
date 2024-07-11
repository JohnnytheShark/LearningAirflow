# Templating tasks using the Airflow Context

## Templating Operator Arguments 
### Formatting and Templates
{{}} - Double curly braces denote a variable inserted at runtime 
Any python variable or expression can be provided. 

execution_date is one of the variables that is magically available in the runtime of a task.

Jinja is the templating engine that allows for variables.

Pendulum library is used for datetimes. It is a drop-in replacement for native PYthon datetime, so all methods that can be applied to Python can be applied to Pendulum. Example:
``` 
datetime.now().year
pendulum.now().year
```
Formatting Strings: 

{{ '{:02}'.format(execution_date.hour) }}

## All task context variables 

| Key | Description|
| --- | --- |
| conf | Provides Access to Airflow Configuration | 
| dag | The current DAG | 
| dag_run | The current DagRun Object | 
| ds | execution_date formatted as %Y-%m-%d | 
| ds_nodash | execution_date formatted as %Y%m%d | 
| execution_date | The start datetime of the task's interval | 
| inlets | Shorthand for task.inlets, a feature to track input data sources for data lineage | 
| macros | airflow.macros module | 
| next_ds | execution_date of the interval(=end of current interval) formatted as %Y-%m-%d | 
|next_ds_nodash | execution_Date of the next interval(=end of current interval) formatted as %Y%m%d | 
|next_execution_date | the Start datetime of the tasks's next interval (=end of current interval) | 
| outlets | Shorthand for task.outlets, a feature to track output data sources for data lineage | 
| params | User-provided variables to the task context | 
| prev_ds | execution_date of the previous interval formatted as %Y-%m-%d | 
| prev_ds_nodash | execution_Date of the previous interval formatted as %Y%m%d | 
| prev_execution_date | The start datetime of the task's previous interval | 
|prev_execution_date_success | Start datetime of the last successfully completed run of the same task (only in past) | 
| prev_start_date_success | Date and time on which the last successful run of the same task (only in past) was started | 
| run_id | The DagRun's run_id (a key composed of a prefix + datetime) |
| task | The current operator | 
| task_instance| The current TaskInstance Object | 
|task_instance_key_str | A unique identifier for the current taskinstance ({dag_id}__{task_id}__{ds_nodash})|
| templates_dict | User-provided variables to the task context | 
| test_mode | Whether AIrflow is running in test mode (configuration property) | 
| ti | THe current TaskInstance object, same as task_instance | 
| tomorrow_ds | ds plus one day |
| tomorrow_ds_nodash | ds_nodash plus one day | 
| ts | execution_date formatted according to ISO8601 format | 
| ts_nodash | execution_date formatted as %Y%m%dT%H%M%S | 
| ts_nodash_with_tz | ts_nodash with time zone information | 
| var | Helpers objects for dealing with Airflow variables | 
| yesterday_ds | ds minus one day | 
| yesterday_ds_nodash | ds_nodash minus one day | 

## Context Python Operators
In Airflow 1, the task context variables must be provided explicitly by setting an argument on the PythonOperator provide_context=True, which passes all(!) context variables to you callable. 

In Airflow 2, the Python Operator determines which context variables must be passed along to your callable by inferring these from the callable argument names. It is therefore not required to set provide_context=True anymore. Airflow 2 is backwards compatible.

Keywords arguments (**kwargs)
**context is a kwarg 


