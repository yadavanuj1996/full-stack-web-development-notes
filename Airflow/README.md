


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
