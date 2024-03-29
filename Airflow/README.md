# AIRFLOW


## Data Pipelines
- Data pipelines extract data from a data source, apply operations, such as transformations, filters, joins, or aggregations to the data, and publish the processed data to a data sink.

### Batch Data Pipelines
- Batch data pipelines are executed manually or recurringly. In each run, they extract all data from the data source, apply operations to the data, and publish the processed data to the data sink. They are done once all data have been processed.
- Typical use cases for batch data pipelines have complex requirements on the data processing, such as joining dozens of different data sources (or tables), and are not time-sensitive. Examples include payroll, billing, or low-frequency reports based on historical data.

### Streaming Data Pipelines
- As opposed to batch data pipelines, streaming data pipelines are executed continuously, all the time. They consume streams of messages, apply operations, such as transformations, filters, aggregations, or joins, to the messages, and publish the processed messages to another stream.

- Typically, they are deployed together with
  - a data source connector, which takes care of extracting data change events from a data store, e.g., a database system, and writing them into the stream consumed by the data pipeline, and
  - a data sink connector, which extracts processed messages from the stream filled by the data pipeline and publishes them to a data store, e.g., a data warehouse.

- Traditional message queues, such as RabbitMQ, delete messages once they have been consumed. Modern event stores, such as Apache Kafka, allow to keep messages as long as needed: for a certain time period, up to a certain amount of storage space, or even forever. This does not only enable to reconstruct the state of a data set at the time of a certain message (or event) but also emphasizes reprocessing (or replaying) messages.

- Common use cases for streaming data pipelines are time-sensitive and must gain insights into the most recent changes that occurred in a certain data store. Examples include fraud detection, critical reports supporting important operational decisions, monitoring of customer behavior, or cybersecurity.


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
- Def 1: Apache Airflow is an open source platform to programmatically author, schedule and monitor workflows.
- Def 2: Airflow is an orchestrator allowing you to execute your tasks at the right time in right way in right order. Airflow helps you interact with various tools so you can execute the taks in right manner.
- Def 3: An orchestrator to deal with batch data pipelines programmatically by authoring, scheduling and monitoring them through a beautiful web UI.

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
- A DAG is basically a graph object representing our data pipeline composed of different tasks with their dependencies.
- DAG is Directed Acyclic Graph. In Aiflow a DAG is a data pipeline.
- Python is used to code DAGs with Apache Airflow.

<img width="1323" alt="Screenshot 2022-02-26 at 5 14 43 PM" src="https://user-images.githubusercontent.com/22169012/155841922-3ae51d9d-f585-4664-a0b9-4c9cab8d1d65.png">


### Operator
- An operator is wrapper around the task (item) you want to achieve.
- ex:- Connecting to db and inserting data we will use a Operator
- One Operator should handle one task, ex:- if a python operator contains two taks Cleaning Data & Processing Data and let's say Processing Data step fails on rerun the cleaning data will also need to be executed again even if Cleaning Data was executed successfully.

Types:
#### Action Operator
Operators executing function or commands. ex: bash operator can be used to run a bash command or a python operator can be used to run a python function.
#### Transfer Operators
Transfer opearaots are used for transfer data from source to destination.  
#### Sensor Operators
- Wait for a Condition to be met.
- They wait for something to happen, let's say if we use a file sensor operator and provide source, whenever a file is available in that particular source the Sensor Operator will trigger.
- ex:- Wait for a file to land at specified location we can use File Sensor, if we want to wait for an mysql record update we will use SQL Sensor.

### Task / Task Instance:
Tasks are saved as Operators in Aiflow. Each time a operator is executed that operator becomes Task Instance

### Workflow:
 Workflow is a DAG with operators(tasks) and dependencies.
 
 

## How Airflow Works?

### One Node Architecture
- Web server, schduler, metastore and executor will be on same machine
- Web server will fetch meta data from meta store
- Scheduler will talk to metasore and executor and schedule the task for execution
- Executor will contain a Queue that will defined the order in which the tasks will be executed.

<img width="768" alt="Screenshot 2022-02-26 at 2 45 33 PM" src="https://user-images.githubusercontent.com/22169012/155837531-19106e56-2fb2-4803-bc9b-8a7b4db50b04.png">

Used for limited no of tasks or POC purpose.

### Multi Nodes Architecture (Celery)

2 Nodes are assigned for running Airflow 
#### The first node will contain 
- Web Server
- Scheduler
- Executor
#### The Second node will contain
- Metasotre
- Queue

#### Worker Nodes
There can be multiple Worker Nodes (Celery  Worker) that will be executing the Airflow tasks unlike Single Node Architecture the Tasks will not be executing on Nodes that contains the Airflow components also the Queue will be external to the Executor.
While the Tasks 
*Queue used can be RabbitMQ or Redis.*

- The Web Server will be in sync with meta store for powering the UI and displaying the status and monitoring part of airflow.
- The Scheduler will be interacting with Metastore and Executor to scheule the taks execution.
- The Executor will push the task in Queue for processing
- The Airflow Worker / Celery Worker will listen to the Queue and execute the tasks.-

<img width="875" alt="Screenshot 2022-02-26 at 2 57 57 PM" src="https://user-images.githubusercontent.com/22169012/155837877-ff50f108-f096-419c-8288-30561fa1605b.png">


### How it Works
- We will add our python file containing data piepelines in Folder Dags.
- The Folder Dags is parsed by both Web Server and Scheduler
- Once it's time to trigger the DAG, the Scheduler will udpate the Metastore and a DagRun instance will be created in Metastore, this DagRun instance status will be running 
-  The first TaskInstance of this DAGRun will be created.
-  Once the TaskInstance object is created the TaskIntance is sent to Executor by Scheduler. 
-  Once the TaskInstance is executed/run by Executor it will update the TaskInstance 
-  Scheduler will check the DAGRun instance and check if the DAGRun instance is complete and subsquently update the status of DAG to Completed


<img width="832" alt="Screenshot 2022-02-26 at 3 07 16 PM" src="https://user-images.githubusercontent.com/22169012/155838160-d7072dda-6675-40fc-a383-89d478cc6c8a.png">



## Airflow Commands:
#### Start Airflow by running the start.sh script
./start.sh (We need to start webserver and scheduler to start and monitor Airflow)

#### Start Airflow webserver
airflow webserver

#### Start Airflow scheduler
airflow scheduler

#### Examine the version of Airflow
airflow version

#### Create airflow user
airflow users create -u user_name -p password_here -r Admin -f first_name -l last_name -e your_email_id (for role Admin)

#### List all the DAGs available.
airflow dags list

#### Examine the DAG. Tasks are listed with dependencies
airflow dags show your_dag_name

#### List the tasks for DAG 
airflow tasks list your_dag_name

#### To test a task
airflow tasks test dag_id task_id date_prev_than_today

#### Trigger a DAG
airflow dags trigger -e 2022-02-27 example_xcom_args

#### List All the DAG runs
airflow dags list-runs

#### To list all the Providers
airflow providers list

#### Pause DAG so that it executes.
airflow pause your_dag_name

#### Unpause DAG so that it executes.
airflow unpause your_dag_name

#### To check logs
ls airflow/logs/your_dag_name

#### To start airflow flower
airflow celery flower


## Airflow UI
- DAG
  - Tree View
    - Shows history of DAG Runs and status of each task instance of that DAG Run
  - Graph View
    - Shows the status of task instances of the current active DAG Run
  - Gantt View
    - Shows the time taken and order (parallel or serial order) of Task Instances
- You can click on any Task Instance to check additional details about the task instance including the log of Task Instance (also we can mark a task instance success or failed from the same modal)


## Creating Data Pipeline


<img width="1617" alt="Screenshot 2022-02-26 at 5 52 04 PM" src="https://user-images.githubusercontent.com/22169012/155842998-a4bec83d-9b4d-4cf2-aa34-097d9dfc34b4.png">

### Connection
#### Adding a new connection
- We can create a new connection using airflow webserver, in header > admin > Connections

#### To test a new connection
airflow db check

#### To initialize db (Only run this commmand on initialization of DB as this flushes the database)
aiflow db init

### The Providers
- Apache Airflow 2 is built in modular way. The "Core" of Apache Airflow provides core scheduler functionality which allow you to write some basic tasks, but the capabilities of Apache Airflow can be extended by installing additional packages, called providers.
- Providers can contain operators, hooks, sensor, and transfer operators to communicate with a multitude of external systems, but they can also extend Airflow core with new capabilities.
- As you know, Airflow allows you to interact with a ton of different tools such as Spark, AWS, Databrick, etc there are existing provider for that but also we can write our own custom providers too 
- A provider is an independent python package that brings everything you need to interact with a service or a tool such as Spark or AWS.
- By default, some operators are pre installed by default such as the PythonOperator and the BashOperator but for the others you will have to install the corresponding prodiver.

## DAG Scheduling & Backfilling

### catchup parameter
- A catchup paramteter (True or False) can be passed in DAG that represents that whether the DAG needs to be run for older dates or not.
  - with DAG('user_processing', start_date=days_ago(2), schedule_interval='@daily', default_args=default_args, catchup=False) as dag:  
  - The above line will create a DAG RUN Instances for last two days as well that is called Backfilling.
- After materializing DAG run entries of a DAG, the Airflow scheduler will “backfill” all past DAG runs whose time dependency has been met if catchup is enabled. If you want that old DAG RUN Instance is not needed set the catchup to False.


## Databases and Executors

### Basics: 
- Executors configuration defined whether the task will run tasks in sequence or parallel.
- Executor Config is important for acheving scalability in Airflow for prod env.
-  Default Executor - Sequential Executor
  - The Sequential Executor is by default configured in Airflow and only support execution of events in sequence (as the name suggests)
  - The Sequential Executor is good for experimenting and debugging (as tasks run in sequence)

- For configuration of Executor two parametes are important sql alchemy connection and executor
  - To check sql alchemy connection use command 
    - airflow config get-value core sql_alchemy_conn
    - returns metastore used by default by Airflow i.e., **sqlite**
    - default value is connection to sqlite db. (SQLite does not support multiple writes at same time), only one task after another can be executed if we are using sqlite
  - To check executor use command
    -  airflow config get-value core executor
    -  By default **SequentialExecutor** is used
    -  Allows tasks execution one after another
    
#### Run tasks in Parallel
- Two items from default config needs to be changed two run tasks in paralled
  - Executor (LocalExecutor - In Local System for Testing, Celery Executor in Prod)
    - SequentialExecutor only supports task execution in sequence 
  - Database (MySQL or Postgres) 
    - As sqlite does not support multiple write at same time
    

![Screenshot 2022-03-12 at 7 14 36 PM](https://user-images.githubusercontent.com/22169012/158020426-e435af43-3eb2-49c5-bda6-d6fcd450c108.png)


### Celery Executor
- Celery Executor provides feature to execute tasks on multiple machines.
- Tasks are executed in workers (machines). The more workers, the more tasks can be executed.
- We have to use a external queue, where items would be pushed and pulled out by the worker. 
- **Recommended Queue: Redis**. To use celery Executor we need to setup and install a external Queue like Redis.
- Each worker corresponds to a Machine, so each machine has an Airflow instance running where the tasks will be executed. (All machines should share dependencies)
- worker_concurrency represents the **no. of tasks atmost** in each of worker, this is defined in configuration file of Airflow. 
  - In case there are 3 workers with worker_concurrency=4, then at most we can execute 12 tasks at a time (max 4 task for each worker).

#### Concurrency Parameters
- **parallelism**
  - In airflow.cfg there is a parameter naemd parallelism which is by default set to 32 that means at max 32 tasks in parallel entire airflow instance.
- **max_active_tasks_per_dag**
  - The maximum number of task instances allowed to run concurrently in each DAG. To calculate the number of tasks that is running concurrently for a DAG, add up the number of running tasks for all DAG runs of the DAG. This is configurable at the DAG level with `max_active_tasks`, which is defaulted as max_active_tasks_per_dag
- **max_active_runs_per_dag** 
  - The maximum number of active DAG runs per DAG. The scheduler will not create more DAG runs if it reaches the limit. This is configurable at the DAG level with ``max_active_runs``, which is defaulted as max_active_runs_per_dag.

![Screenshot 2022-03-12 at 7 37 05 PM](https://user-images.githubusercontent.com/22169012/158021125-49035496-1451-4616-9155-984776ff9d70.png)




### XComs
- XComs are used to send small packet of data from one task to another task
- If we return a value from a python_callable function that value is stored in a XCOM (it is automatically pushed into a XCOM.)

### BranchPythonOperator (If Else condition in task execution)
- BranchPythonOperator is used to choose a specific path in our DAG, (Like choosing a task path on the basis of if else condition) 
- When we use branching, the skipped tasks are considered as failed tasks and so if we run again the DAG and the condition follows a previously skipped path, it won't be executed.

### Trigger Rules
- Trigger Rule to alert Error Cases
  - Use trigger rule **one_failed** to alert the error in any task ()
- Other trigger rules
  - **all_success**: (default) all parents have succeeded
  - **all_failed**: all parents are in a failed or upstream_failed state
  - **all_done**: all parents are done with their execution
  - **one_failed**: fires as soon as at least one parent has failed, it does not wait for all parents to be done
  - **one_success**: fires as soon as at least one parent succeeds, it does not wait for all parents to be done
  - **none_failed**: all parents have not failed (failed or upstream_failed) i.e. all parents have succeeded or been skipped
  - **none_skipped**: no parent is in a skipped state, i.e. all parents are in a success, failed, or upstream_failed state
  - **dummy**: dependencies are just for show, trigger at will




### Important Links
- Airflow Providers Packages:
https://airflow.apache.org/docs/apache-airflow-providers/packages-ref.html
 

