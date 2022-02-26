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


## What is Airflow?
Apache Airflow is an open source platform to programmatically author, schedule and monitor workflows.
or Airflow is an orchestrator allowing you to execute your tasks at the right time in right way in right order. Airflow helps you interact with various tools so you can execute the taks in right manner.

### Benifits:
- Data pipeline are dynamic
- Coded in python (everything that can be done in python can be done in airflow)
- Scalability
  - Execute large amount tasks in parallel, we can use kubernetes cluster or celery cluster for executing tasks.
- UI
  - Useful and easy User Interface, we can retry and monitor all our tasks.
- Extensible
  - We can create a plugin to connect to any new tool thus no dependency on third party for connecting to a new tool.

### Airflow Architecture consists of the following entities:
1. Web server
  - Flask Server with Gunicorn serving the UI
2. Scheduler
   - Daemon in charge of scheduing workflows (tasks)
3. Metastore (Database)
   - Meta data realted to airflow and data pipeline and tasks will be stored. Recommended DB- Postgres, also any sql alchemy db can be used.
4. Executor
   - Class defining how your taks should be executed. 
   - We can declare if we want the tasks to execute on the same machine as sub processes we can use local executor.
   - If we have a kuberenetes cluster running we can declare that the tasks run in the kubernetes cluster using kuberenetes executor.
   - We can use also use Celery Executor 
5. Worker
   - Process/sub process executing the task. (Executor only defines how worker is the one executing the task)

### Details:

#### Scheduler
The scheduler is responsible for monitoring all DAGs and the tasks within them. When dependencies for a task are met, the scheduler triggers the task. Under the hood, the scheduler periodically inspects active tasks to trigger.

#### Web server
The web server is Airflow’s UI. It displays the status of the jobs and allows the user to interact with the databases as well as read log files from a remote file store, such as S3, Google Cloud Storage, Azure blobs, etc.

#### Executor
The executor determines how the work gets done. There are different kinds of executors that can be plugged in for different behaviors and use cases. The SequentialExecutor is the default executor that runs a single task at any given time and is incapable of running tasks in parallel. It is useful for a test environment or when debugging deeper Airflow bugs. Other examples of executors include CeleryExecutor and LocalExecutor.

The LocalExecutor supports parallelism and hyperthreading and is a good fit for running Airflow on a local machine or a single node. The Airflow installation for this course uses the LocalExecutor.

The CeleryExecutor is the preferred method to run a distributed Airflow cluster. It requires Redis, RabbitMq, or another message queue system to coordinate tasks between workers.

The KubernetesExecutor calls the Kubernetes API to create a temporary pod for each task instance to run. Users can pass in custom configurations for each of their tasks.

#### Meta Store / Database
The state of the DAGs and their constituent tasks needs to be saved in a database so that the scheduler remembers metadata information, such as the last run of a task, and the web server can retrieve this information for an end user. Airflow uses SQLAlchemy and Object Relational Mapping (ORM), written in Python, to connect to the metadata database. Any database supported by SQLAlchemy can be used to store all the Airflow metadata. Configurations, connections, user information, roles, policies, and even key-value pair variables are stored in the metadata database. The scheduler parses all the DAGs and stores relevant metadata, such as schedule intervals, statistics from each run, and their task instances.



### DAG
DAG is Directed Acyclic Graph. In Aiflow a DAG is a data pipeline.

### Operator
An operator is wrapper around the task (item) you want to achieve.
ex:- Connecting to db and inserting data we will use a Operator

Types:
#### Action Operator
Operators executing function or commands. ex: bash operator can be used to run a bash command or a python operator can be used to run a python function.
#### Transfer Operators
Transfer opearaots are used for transfer data from source to destination.  
#### Sensor Operators
They wait for something to happen, let's say if we use a file sensor operator and provide source, whenever a file is available in that particular source the Sensor Operator will trigger.

### Task / Task Instance:
Tasks are saved as Operators in Aiflow. Each time a operator is executed that operator becomes Task Instance

### Workflow:
 Workflow is a DAG with operators(tasks) and dependencies.
 
 




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
