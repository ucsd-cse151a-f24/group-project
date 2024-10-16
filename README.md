# Group Project Information

## Login to SDSC Expanse
Go to [portal.expanse.sdsc.edu](portal.expanse.sdsc.edu) and login with your "ucsd.edu" credentials (2), **Note: if this is your first time, you will need to link your NSF ACCESS "access-ci.org" credentials (3)**

### PLEASE READ THE DIRECTIONS THOROUGHLY so you do not have issues!!!

<br>
<br>

## First Time Log In
If you are logging in to Expanse for the first time, there are some extra steps you have to take to log in.

1. Make sure you have a NSF Access ID set up (this is taken care of by the professor if you have filled out the proper forms)
   
<br>
<br>

2. Go to [portal.expanse.sdsc.edu](portal.expanse.sdsc.edu) and you will most likely see the following screen
![First page](images/first-page.png)
Make sure you select the University of California San Diego choice as seen in the image

<br>
<br>

3. After you log in through UCSD, it will ask you to link an account, the page should look like this:
![Linking](images/linking.png)
Choose the option that says "link an identity with **ACCESS CI**"

**NOTE: If you do not do this, you will NOT have access to SDSC**

<br>
<br>

4. This will take you to the Access log in page
![Login](images/login.png)
If you have Access credentials already, use that to log in. However, since you probably have it set up that you logged in through UCSD credentials, you may not currently have a password set up for Access. If that is the case, click "forgot password" and follow the process to reset the password. **Note:** It will also have you set up the Duo connection in some form, be prepared for that

<br>
<br>

5. This should lead to your account being connected. If you see the following page, you should be good to go!
![Complete](images/connected.png)

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

- **Number of cores**: Enter an integer value denoting the number of cores your pyspark session with need. Enter a value between `2` and `128`.

- **Memory required per node (GB)**: Enter an integer value denoting the total memory required. Initially, start with a value of `2`, i.e., 2GB. You may increase it if you get issues where you need more than 2GB per executor in your Spark Session (Spark will let you know about the amount of RAM being too low when loading your datasets). The maximum value allowed is `250`, i.e., 250GB. 

  > For example, if you have 128GB of total memory and 8 cores, each core gets 128/8 = 16GB of memory.

- **Singularity Image File Location**: `~/esolares/tensorflow.2.16.1_jupyterlab.sif`

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

### 2.2 JupyterLab environments
Note that you will have access to various jupyterlab notebook environments that give you access to other things such as scipy, tensorflow and pytorch as well as yolov8.
Here are the list of notebook files in `~/uci150/esolares/*.sif`
```
# tf 2.16.1 + jupyterlab
~/uci150/esolares/tensorflow.2.16.1_jupyterlab.sif

# torch 2.2.2 CUDA 12.1 + jupyterlab
~/uci150/esolares/pytorch2.2.2cuda12.1_jupyterlab.sif

# spark 3.5.0 + jupyterlab
~/uci150/esolares/spark_py_latest_jupyter.sif

# yolov8 + torch 2.2.2 CUDA 12.1 + jupyterlab
~/uci150/esolares/yolov8pytorch2.2.2cuda12.1_jupyterlab.sif
```

### 2.2.optional Spark Session Builder
Based on the configurations provided in **Jupyter** above, you need to update the following code to build your `SparkSession`. 
> For example, if you have 128GB of total memory and 8 cores, each core gets 128/8 = 16GB of memory. The driver can take 1 or more cores and executors can take the remaining cores (7 or less).
```py
sc = SparkSession.builder \
    .config("spark.driver.memory", "16g") \
    .config("spark.executor.memory", "16g") \
    .config('spark.executor.instances', 7) \
    .getOrCreate()
```

>Driver memory is the memory required by the master node. This can be similar to the executor memory as long as you are not sending a lot of data to the driver (i.e., running collect() or other heavy shuffle operation).

![Spark Session](images/spark-session.png "Spark Session")

Example Spark notebooks are available at `~/esolares/spark_notebooks`.

<br>
<br>

## 3. Active Jobs
Click on the "Active Jobs" app in the SDSC Expanse Portal. Please use this while debugging Spark jobs. Note the job `Status` and `Reason`. If the job was recently run and is dead, you will see the reason why it died under the `Reason` field. 

![Active Jobs](images/active-jobs.png "Active Jobs")


<br>
<br>


## FAQs
[FAQs](FAQs.md "FAQs")

<br>
<br>

## Support
If you are having trouble, please submit a ticket to https://support.access-ci.org/.
