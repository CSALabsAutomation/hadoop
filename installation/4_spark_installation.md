#    Steps for installing Spark

1.  Open the WSL [Ubuntu] terminal and navigate to your individual user.[ hdoop ] 

    ```
    su - hdoop
    ```
    
2.  Create a folder named as spark

    ```
    mkdir spark
    ```
    
3.  Navigate to the spark folder

    ```
    cd spark
    ```
    
4.  Downloading Spark by using wget command in a specified location.

    ```
    wget https://dlcdn.apache.org/spark/spark-3.3.1/spark-3.3.1-bin-hadoop3.tgz
    ```
    
5.  Extracting the downloaded tar file in Linux machine by using tar command.

    ```
    tar -xvf spark-3.3.1-bin-hadoop3.tgz
    ```

6.  Come out of spark folder by typing `cd` and run the below command to open bashrc file.	

    ```
    sudo nano .bashrc
    ```
    
7.  Add the below lines to configure Spark path at the end. Save[CTRL + S] the file and Quit[CTRL + X]. Also make sure SPARK_HOME path is correctly given.

    ```
    SPARK_HOME=/spark/spark-3.3.1-bin-hadoop3
    export PATH=$PATH:$SPARK_HOME/bin:$SPARK_HOME/sbin
    ```

8.  Reload the modified code.
	
    ```
    source  ~/.bashrc
    ```

9.  Now navigate to the `spark` folder.
 
    ```
    cd spark
    ```
    
11. To initiate the spark-shell, you should be in /bin. Navigate to `spark-3.3.1-bin-hadoop3/bin path`

    ```
    cd spark-3.3.1-bin-hadoop3/bin
    ```
    
10)	 Now initiate the spark shell.

     ```
     spark-shell
     ```
