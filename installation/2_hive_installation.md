#    Steps for installing Hive 


To install Hive, you need to have Hadoop installed and SSH server running. To know more refer the link [ Hadoop Installation steps](../installation/2_java_hadoop_ssh_installation.md) for installation.

1. Open the WSL [Ubuntu] terminal and navigate to your individual user.[ hdoop ] 

    ```
    su - hdoop
    ```
    
2. Download Hive by using wget command in a specified location.
 
   ```
   wget https://downloads.apache.org/hive/hive-3.1.2/apache-hive-3.1.2-bin.tar.gz
   ```
  
2. Extracting the downloaded tar file in Linux machine by using tar command.
 
   ```
   tar xzf apache-hive-3.1.2-bin.tar.gz 
   ```
   
3. Run the below command to open bashrc file.
  
   ```
   sudo nano .bashrc
   ```
   
4.	Add the below lines to configure Hive path at the end. Save[CTRL + S] the file and Quit[CTRL + X]. Also make sure HIVE_HOME path is correctly given

    ```
    export HIVE_HOME=/home/hdoop/apache-hive-3.1.2-bin
    export PATH=$PATH:$HIVE_HOME/bin
    ```

5.	Reload the modified code.
  
    ```
    source .bashrc
    ```
    
6.	Run the below command to edit ``hive-config.sh`` file.
  
    ```
    sudo nano $HIVE_HOME/bin/hive-config.sh
    ```
    
7.   Add the below lines to configure Hadoop path.

     ```
     export HADOOP_HOME=/home/hdoop/hadoop-3.3.4
     ```
     
7.  Create the tmp directory to store the result of query in directory 

    ```
    hdfs dfs -mkdir /tmp
    ```
 
8.  Grant permission to temporary directory

    ```
    hdfs dfs -chmod g+w /tmp
    ```
 
9.  Create warehouse directory to store all the hive tables.
 
    ```
    hdfs dfs -mkdir -p /user/hive/warehouse 
    ```
    
10. Grant permission to warehouse directory
 
    ```
    hdfs dfs -chmod g+w /user/hive/warehouse  
    ```
    
11. Initiating the derby database
    
    ```
    schematool -initSchema -dbType derby
    ```
    
12. Enter into hive interface

    ```
    hive
    ```
    
13. Run the command to show existing databases.
 
    ```
    Show databases;
    ```
14.	Command to create table.

    ```
    create table Employee(id int);
    ```
    
15.	Command to use default database 

    ```
    use default; 
    ```
    
16.	Command to show list of tables

    ```
    show tables; 
    ```

