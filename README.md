# Group Project Information

## Login to SDSC Expanse
Go to [portal.expanse.sdsc.edu](portal.expanse.sdsc.edu) and login with your "access-ci.org" or "ucsd.edu" credentials.

<br>
<br>

## Portal Navigation
Once you are logged in, you will see the following SDSC Expanse Portal, along with several Pinned Apps. 

![Portal Navigation](images/portal-navigation.png "Portal Navigation")

We will be working with the following apps:
1. **expanse Shell Acess**: To access Terminal.
2. **Jupyter**: To setup Jupyter notebook and run JupyterLab.
3. **Active Jobs**: To check jobs' status.

<br>
<br>

## 1. expanse Shell Acess and First Time Login
Click on the "expanse Shell Access" app in the SDSC Expanse Portal. Once you are in the Terminal, please run the following commands: 
```shell
# Create a new folder with your username and add symbolic link
ln -sf /expanse/lustre/projects/uci150/$USER

# Add symbolic link to `esolares` folder where the singularity
# images are stored
ln -sf /expanse/lustre/projects/uci150/esolares

# (Optional)
# To see your group members folders, do the following for each 
# group member's usernames
ln -sf /expanse/lustre/projects/uci150/GROUPMEMBERUSERNAME
```
>Note that you need to run the above instructions only once when accessing the Portal for the first time. 

<br>
<br>

## 2. Jupyter
Click on the "Jupyter" app in the SDSC Expanse Portal. 

![Jupyter Portal App](images/jupyter-icon.png "Jupyter Portal App")

It will allow you to request a new Jupyter Session as shown below:

![Jupyter Session](images/jupyter-config.png "Jupyter Session")

You will need to fill out the following fields: 
- **Account**: `TG-CIS240277`

- **Partition**: `shared`

- **Time limit (min)**: Enter an integer value denoting the number of minutes you want to work on your notebook environment.

- **Number of cores**: Enter an integer value denoting the number of cores your pyspark session with need. Enter a value between 2 and 8.

- **Memory required per node (GB)**: Enter an integer value denoting the memory required per executor (worker nodes). Initially, start with a value of `2`, i.e., 2GB. You may increase it if you get issues where you need more than 2GB per executor in your Spark Session (Spark will let you know about the amount of RAM being too low when loading your datasets).

- **Singularity Image File Location**: `~/esolares/spark_py_latest_jupyter_dsc232r.sif`

- **Environment Modules to be loaded**: `singularitypro`

- **Working Directory**: `home`

- **Type**: `JupyterLab`

Once you have filled out the above fields, go ahead and click "Submit".

![Jupyter Config](images/jupyter-config2.png "Jupyter Config")

<br>
<br>

### 2.1. JupyterLab
After clicking "Submit", the SDSC Expanse Portal will put your job request in a Queue. Based on the availability of resources, this might take some time. Once the request is processed, it will open a JupyterLab session. Here you can navigate around and create your own Python3 Jupyter notebooks. 

![JupyterLab](images/jupyterlab.png "JupyterLab")

<br>
<br>

### 2.2. Spark Session Builder
Based on the configurations provided in **Jupyter** above, you need to update the following code to build your `SparkSession`:
```py
sc = SparkSession.builder \
    .config("spark.driver.memory", "8g") \
    .config("spark.executor.memory", "2g") \
    .config('spark.executor.instances', 1) \
    .getOrCreate()
```

>Driver memory (i.e., the memory required by the master node) should be set to ≤ Number of cores * Memory required per node (GB). In other words, driver memory should be similar to the total executor memory.

![Spark Session](images/spark-session.png "Spark Session")

Example Spark notebooks are available at `~/esolares/spark_notebooks`.

<br>
<br>

## 3. Active Jobs
Click on the "Active Jobs" app in the SDSC Expanse Portal. Please use this while debugging Spark jobs. Note the job `Status` and `Reason`. If the job was recently run and is dead, you will see the reason why it died under the `Reason` field. 

![Active Jobs](images/active-jobs.png "Active Jobs")


<br>
<br>

## Support
If you are having trouble, please submit a ticket to https://support.access-ci.org/.
