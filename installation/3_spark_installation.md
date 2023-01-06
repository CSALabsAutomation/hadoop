#    Steps for installing Spark

    
1.  In your Bastion, create a folder ``spark``.

    ```
    mkdir spark
    ```
    
2.  Navigate to the spark folder

    ```
    cd spark
    ```
    
3.  Downloading Spark by using wget command in a specified location.

    ```
    wget https://dlcdn.apache.org/spark/spark-3.3.1/spark-3.3.1-bin-hadoop3.tgz
    ```
    
4.  Extracting the downloaded tar file in Linux machine by using tar command.

    ```
    tar -xvf spark-3.3.1-bin-hadoop3.tgz
    ```

5.  Come out of spark folder by typing `cd` and run the below command to open bashrc file.	

    ```
    sudo nano .bashrc
    ```
    
6.  Add the below lines to configure Spark path at the end. Save[CTRL + S] the file and Quit[CTRL + X]. Also make sure SPARK_HOME path is correctly given.

    ```
    export SPARK_HOME=/home/hdoopuser/spark/spark-3.3.1-bin-hadoop3
    export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin
    ```

7.  Reload the modified code.
	
    ```
    source  ~/.bashrc
    ```
    
8.  Download the CData JDBC Driver for PostgreSQL installer, unzip the package, and run the JAR file to install the driver.

    ```
    wget https://jdbc.postgresql.org/download/postgresql-42.5.1.jar
    ```
    
9. Start the spark shell with the CData JDBC Driver for PostgreSQL JAR file as the jars parameter.

    ```
    spark/spark-3.3.1-bin-hadoop3/bin/pyspark --jars /home/hdoopuser/postgresql-42.5.1.jar

    ```

