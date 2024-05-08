# FAQs

1. **How to create a Shared folder in SDSC server?**

    You would need to create a shared folder inside of `uci150/$USER` and then, run: 
    ```shell
    chmod g+w shared
    ```
    
    This is only for the `shared` folder inside `uci150/$USER`. Creating a folder inside of `home` directory is extremely slow and has a small quota comparatively. However, `uci150` is fast and on the distributed file system. 

    <br>
    <br>

2. **How do I install AWS CLI in SDSC server?**
   
    Since this is a shared resource, you cannot install packages into the operating system. Instead you need to install them local in your `$HOME/bin` folder.

    ```shell
    # first create the `bin` folder in your home directory. This is to be done without singularity
    mkdir -p $HOME/bin/aws-cli
    cd $HOME/bin/aws-cli
    curl "https://awscli.amazonaws.com/awscli-exe-linux-x86_64.zip" -o "awscliv2.zip"
    unzip awscliv2.zip
    ./aws/install --bin-dir $HOME/bin/aws-cli --install-dir $HOME/bin/aws-cli --update
    ```

    We grabbed this from the aws website and modified it for hpc install. You will need to go to https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html.

    In order to put it in your path, you will need to run:
    
    ```shell
    PATH=$HOME/bin/aws-cli:$PATH
    ```    
    You will need to do this everytime you log in.

    <br>
    <br>

3. **What is the maximum memory available?**

    You have a total of 250GB of memory available.

    <br>
    <br>


4. **What is the maximum number of executors available?**

    You can have a maximum of 128 executors. 

    <br>
    <br>


5. **Please provide an example SparkSession configuration.**

    ```py
    sc = SparkSession.builder \
        .config("spark.driver.memory", "8g") \
        .config("spark.executor.memory", "2g") \
        .config('spark.executor.instances', 1) \
        .getOrCreate()
    ```
    
    <br>
    <br>

