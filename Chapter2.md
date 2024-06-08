# Exploring Airflow

Python is the main source of code for the data pipelines.

The DAG class takes two required arguments 
Name, Datetime at which the workflow should first start running

You can set the schedule to None so it doesn't run a

In Airflow Tasks and their dependencies are set up with arrows: 

download_launches >> get_pictures >> notify 

The role of a DAG is to orchestrate the execution of a collection of operators. THat includes the starting and stopping of operators, starting consecutive tasks once an operator is done, ensuring dependencies between operators are met, and so on. 

Operators provide the implementation of a piece of work. 

Tasks in Airflow manage the execution of an operator; they can be though of as a small wrapper or manager around an operator that ensures the operator executes correctly. 

## Bare Minimum Airflow consists of three core components: 
A Scheduler
A Webserver
A Database 

(Run Airflow in a Docker Container)

## Dag Portions 
The DAG class takes the following arguments when intiating:
dag_id = the name of your workflow 
start_date = when did your airflow start 
schedule_interval = how often your workflow is running.

## Benefits
Benefits to using airflow is that you can restart from the point of failure and onward, without having to restart any previously succeeded tasks. 

## Running Locally 
You can run a command or build an image that is based on apache/airflow to be able to test out your DAG. 

However, I hate writing run commands or having them memorized all the time. Use a .yml file to create your run commands. An example of one can be found in this repository to base your run on. 

Remember this only works if you are not changing anything from your base image, however if you want to add new items or scripts then you would use the base apache/airflow container to create a new image and then reference that image in yml file for testing or running locally.

## Summary 

* Workflows in Airflow are DAGs

* Operators are single units of work. 

* Airflow contains an array of operators both for generic or specific work 

* Airflow UI offers a graph view for viewing the DAG structure 
 
* Failed tasks can be restarted anywhere in a DAG. 

