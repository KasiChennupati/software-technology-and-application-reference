# Apache Airflow Installation

Let's visit and see the space we are working with
<a href="https://airflow.apache.org/docs/apache-airflow/stable/start.html" target="_blank" rel="noopener">Official Airflow Quick Start Page</a>

Apache Airflow is an awesome tool created by Airbnb to solve their data engineering pipeline problems.

When setup and managed properly airflow can solve all of the enterprise data engineering problems surrounding data dependencies and pipeline maintenane.

Let's see how to install the Apache Airflow in Docker Environment.

## From Airflow Quick Start Page

<a href="https://airflow.apache.org/docs/apache-airflow/stable/start.html" target="_blank" rel="noopener">Official Airflow Quick Start Page</a>

As of 13-May-2023 airflow requires Python3 environment and starting from Airflow version 2.3.0 all versions are tested on **Python 3.7, 3.8, 3.9, 3.10**

And only installation via **pip** is **officially supported** and recommended other tools like **poetry** or **pip-tools** are currently **not supported/recommended** officially.

The installation is fairly easy but would need a basic knowledge on linux command line and python package installation.

The use of constraints file is recommended and the following is provided to us as a code block.

```bash
# Airflow needs a home. `~/airflow` is the default, but you can put it
# somewhere else if you prefer (optional)
export AIRFLOW_HOME=~/airflow

# Install Airflow using the constraints file
AIRFLOW_VERSION=2.6.0
PYTHON_VERSION="$(python --version | cut -d " " -f 2 | cut -d "." -f 1-2)"
# For example: 3.7
CONSTRAINT_URL="https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-${PYTHON_VERSION}.txt"
# For example: https://raw.githubusercontent.com/apache/airflow/constraints-2.6.0/constraints-3.7.txt
pip install "apache-airflow==${AIRFLOW_VERSION}" --constraint "${CONSTRAINT_URL}"

# The Standalone command will initialise the database, make a user,
# and start all components for you.
airflow standalone

# Visit localhost:8080 in the browser and use the admin account details
# shown on the terminal to login.
# Enable the example_bash_operator DAG in the home page
```

Now looking at the above file code block a few things are clear the developers of airflow have gone out of their way to provide with commands that will automatically detect and install the software for us.

## Code Block Explanation

Now, let's dissect the installation code block and understand what each line is trying to do.

```bash
1   # Airflow needs a home. `~/airflow` is the default, but you can put it
2   # somewhere else if you prefer (optional)
3   export AIRFLOW_HOME=~/airflow
4   
5   # Install Airflow using the constraints file
6   AIRFLOW_VERSION=2.6.0
7   PYTHON_VERSION="$(python --version | cut -d " " -f 2 | cut -d "." -f 1-2)"
8   # For example: 3.7
9   CONSTRAINT_URL="https://raw.githubusercontent.com/apache/airflow/constraints-${AIRFLOW_VERSION}/constraints-${PYTHON_VERSION}.txt"
10  # For example: https://raw.githubusercontent.com/apache/airflow/constraints-2.6.0/constraints-3.7.txt
11  pip install "apache-airflow==${AIRFLOW_VERSION}" --constraint "${CONSTRAINT_URL}"
12  
13  # The Standalone command will initialise the database, make a user,
14  # and start all components for you.
15  airflow standalone
16  
17  # Visit localhost:8080 in the browser and use the admin account details
18  # shown on the terminal to login.
19  # Enable the example_bash_operator DAG in the home page
```

### How to know if it's linux code block

Now, the fist thing to know in the earlier section we mentioned this code block is for linux. But, how do we know these instructions are for linux environment and not for windows.

- The *line(7)* ``` PYTHON_VERSION="$(python --version | cut -d " " -f 2 | cut -d "." -f 1-2)" ``` these are the lines that give away the references to the linux command line since it looks a lot like bash script than powershell script.
- The command at *line(3)* ```
export AIRFLOW_HOME=~/airflow``` The export command is used in linux for setting the environment variables
- You see the *line(3)* with ```/``` with them as directory Linux uses forward slashes ```/``` as path seperator where as windows uses backward slash ```\``` as path seperator.

### Line by Line

In the code block the *lines(1-3)*

```bash
# Airflow needs a home. `~/airflow` is the default, but you can put it
# somewhere else if you prefer (optional)
export AIRFLOW_HOME=~/airflow
```

we are taking about the default location of the airflow location by setting an environment variable **AIRFLOW_HOME**. The value for this variable is set to ```~/airflow``` meaning the folder airflow is going to be present in users home directory if you are using linux then this can also be understood as ```/home/{username}/airflow``` the part ```~/``` is telling the os that it's users home directory if you install the airflow as sudo its still in users directory but if you install this as root user then this will be in ```/root/airflow``` installing as root is not recommended for any application in linux. if you are installing this in windows then the value for AIRFLOW_HOME would be ```\Users\{username}\airflow```

## Contributing

Do you wnat to contribute?

The best way is to raise a Github Issue !

Thank You!
