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

