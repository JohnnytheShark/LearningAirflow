# Airflow 

## Data Pipelines 
Data pipelines generally consist of several tasks and actions that are needed to be executed to achieve a desired result. 

### Directed Acyclic Graph (DAG)

The graphc contains directed edges and does not contain any loops or cycles (acyclic). The acyclic property is extremely important, as it prevents us from running into circular dependencies. 

Circular Dependencies become problematic when trying to execute nodes that depend on one another to be completed. Think of a forever loop due to recursion.

DAG creates the an algorithm that achieves the following: 

1. For each open (= uncompleted) task in the graph do the following: 
    For each edge pointing toward the task, check if the "upstream" task on the other end of the edge has been completed. 
    If all upstream tasks have been completed, add the task under consideration to a queue of tasks to be executed.

2. Execute the tasks in the execution queue, marking them completed once they finish performing their work 
3. Jump back to step 1 and repeat until all tasks in the graph have been completed. 


The reason we use graphical inferface is because we can run things in parallel. 

Separation of tasks also helps when troubleshooting portions of the workflows

DAG files are Python Scripts that describe the structure of the corresponding DAG. 

## Scheduling 
Once you build out your pipeline(s) as DAG(s), Airflow allows you to define a schedule interval for each DAG.

Cron-Like Expressions are used

## Organization
* Airflow Scheduler - Parses DAGs, checks their schedule interval, and (if the DAGs' schedule has passed) starts scheduling the DAGs' tasks for execution by passing them to the Airflow Workers. 
* Airflow Workers - Pick up tasks that are scheduled for execution and execute them. 
* Airflwo Webserver - Visualizes the DAGs parsed by the scheduler and provided the main interface for users to monitor DAG runs and their results. 

## Web Interface 

Airflow provides a graph view that allows you to see the flow. 

As well as providing a tree view. The tree view allows you to dig into failing tasks to see what went wrong.

Airflow can handle failures in tasks by retrying them a couple of times (optionally with some wait time in between), which can help tasks recover from any intermittent failures. 

If retries don't help, Airflow will record the task as being failed, optionally notifying you about the failure. 









