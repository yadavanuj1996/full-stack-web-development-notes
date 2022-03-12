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



## Dag Commands:
#### Start Airflow by running the start.sh script
./start.sh

#### Examine the version of Airflow
airflow version

#### List all the DAGs available.
airflow dags list

#### Examine the DAG. Tasks are listed with dependencies
airflow dags show your_dag_name

#### List the tasks for DAG 
airflow tasks list your_dag_name

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
airflow tasks test dag_id task_id date_prev_than_today

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





### Important Links
- Airflow Providers Packages:
https://airflow.apache.org/docs/apache-airflow-providers/packages-ref.html
 

