# AIRFLOW


## Why Airflow?
Airflow is used to manage data pipelines and execute tasks in reliable way also you can monitor & retry taks easily. 

Let's say we have a data pipeline that contains 3 steps:
- Downloading Data  
  - Request API
- Processing Data 
   - Spark Job
- Storing Data
  - DB Insertion

For this we have to not only execute tasks in data pipeline but also make sure the external tools like API and Database are available, let's say if there is a case that API or Spark Job Fails or DB service is not available and managing all this manually will prove a challenging task. Assume we have 100 such pieplines to manage thus this data pipeline cannot be managed manually and we need a tool loke Airflow for handling such multiple pipelines.







Airflow Architecture consists of the following entities:
1. Scheduler
2. Web server
3. Database
4. Executor

![Screenshot 2022-01-03 at 12 07 56 PM](https://user-images.githubusercontent.com/22169012/147904766-faed9565-4552-44aa-a388-b0aa8a602b21.png)


#### Scheduler
The scheduler is responsible for monitoring all DAGs and the tasks within them. When dependencies for a task are met, the scheduler triggers the task. Under the hood, the scheduler periodically inspects active tasks to trigger.

#### Web server
The web server is Airflow’s UI. It displays the status of the jobs and allows the user to interact with the databases as well as read log files from a remote file store, such as S3, Google Cloud Storage, Azure blobs, etc.

#### Executor
The executor determines how the work gets done. There are different kinds of executors that can be plugged in for different behaviors and use cases. The SequentialExecutor is the default executor that runs a single task at any given time and is incapable of running tasks in parallel. It is useful for a test environment or when debugging deeper Airflow bugs. Other examples of executors include CeleryExecutor and LocalExecutor.

The LocalExecutor supports parallelism and hyperthreading and is a good fit for running Airflow on a local machine or a single node. The Airflow installation for this course uses the LocalExecutor.

The CeleryExecutor is the preferred method to run a distributed Airflow cluster. It requires Redis, RabbitMq, or another message queue system to coordinate tasks between workers.

The KubernetesExecutor calls the Kubernetes API to create a temporary pod for each task instance to run. Users can pass in custom configurations for each of their tasks.

#### Database
The state of the DAGs and their constituent tasks needs to be saved in a database so that the scheduler remembers metadata information, such as the last run of a task, and the web server can retrieve this information for an end user. Airflow uses SQLAlchemy and Object Relational Mapping (ORM), written in Python, to connect to the metadata database. Any database supported by SQLAlchemy can be used to store all the Airflow metadata. Configurations, connections, user information, roles, policies, and even key-value pair variables are stored in the metadata database. The scheduler parses all the DAGs and stores relevant metadata, such as schedule intervals, statistics from each run, and their task instances.


## Dag Commands:
#### Start Airflow by running the start.sh script
./start.sh

#### Examine the version of Airflow
airflow version

#### List all the DAGs available.
airflow list_dags

#### Examine the DAG. Tasks are listed with dependencies
airflow show_dag your_dag_name

#### List the tasks for DAG 
airflow list_tasks your_dag_name

#### List the runs for DAG.
airflow list_dag_runs your_dag_name

#### Unpause DAG so that it executes.
airflow unpause your_dag_name

#### List All the DAG runs
airflow list_dag_runs your_dag_name

#### To check logs
ls airflow/logs/your_dag_name

#### Manually trigger the DAG
airflow trigger_dag your_dag_name
