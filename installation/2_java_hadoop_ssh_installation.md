#    Steps for installing Java, Hadoop and SSH

##	Java Installation 

1. Open the WSL \[Ubuntu] terminal and update the package repository to ensure you download the latest software version.

    ```
    sudo apt update  
    ```
     
 2. Install openJDK
 
    ```
    sudo apt install openjdk-8-jdk -y
    ```
    
 3. Verify the version of the JDK
 
    ```
    java -version    
    ```
 
##    Create and setup SSH certificates

1. Installing SSH for creating connection between Hadoop and Linux Machine.

    ```
    sudo apt install openssh-server openssh-client -y  
    ```

2. Adding a new individual user as `hdoop` and this user will use the Hadoop in the system. 

    ```
   sudo adduser hdoop 
    ```
    
   > Make sure you set the password as **`hadoop123`** and you will be using same password whenever you login to `hdoop` user. 

3. Login to the new user `hdoop` and enter password when it promts for it.

    ```
    su - hdoop
    ```

4. Generating the SSH key for the connection between local machine and Hadoop

    ```
    ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
    ```
    
    

5. Authorizing the key for connecting new user to the Hadoop.

    ```
    cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
    ```
    
6. Changing permissions of the authorized key file by using chmod.

    ```
    chmod 0600 ~/.ssh/authorized_keys
    ```
    
7. Connect to SSH localhost by creating connection to the local host so that the system works on server.

    ```
    ssh localhost
    ```

8. Navigate to existing user.

    ```
    su - hadoopuser  
    ```
    
    > Enter password when it prompts .
    
9. Adding new user `hdoop` to sudo group.

    ```
    sudo adduser hdoop sudo
    ```
    
10. Login to individual `hdoop` user :  

    ```
    su - hdoop
    ```
    > Enter password when it prompts .

    
##	Hadoop Installation

1. Downloading Hadoop by using wget command in a specified location.

    ```
    wget https://downloads.apache.org/hadoop/common/hadoop-3.3.4/hadoop-3.3.4.tar.gz 
    ```
    
2. Extracting the downloaded tar file in Linux machine by using tar command.

    ```
    tar -xvzf hadoop-3.3.4.tar.gz 
    ```
    
##	Setup configuration files 

- There are 6 modifications to be done.


#### Modification 1 
  
 1. Run the below command to open bashrc file.
           
    ```
    sudo nano .bashrc
    ```
       
 2. Add the below lines at the end. Save[CTRL + S] the file and Quit[CTRL + X]. Also make sure HADOOP_HOME path is correctly given.
	
     ```
     export HADOOP_HOME=/home/hdoop/hadoop-3.3.4
     export HADOOP_INSTALL=$HADOOP_HOME
     export HADOOP_MAPRED_HOME=$HADOOP_HOME
     export HADOOP_COMMON_HOME=$HADOOP_HOME
     export HADOOP_HDFS_HOME=$HADOOP_HOME
     export YARN_HOME=$HADOOP_HOME
     export HADOOP_COMMON_LIB_NATIVE_DIR=$HADOOP_HOME/lib/native
     export PATH=$PATH:$HADOOP_HOME/sbin:$HADOOP_HOME/bin
     export HADOOP_OPTS="-Djava.library.path=$HADOOP_HOME/lib/native"
     ```
	
 3. Reload the modified code.
	
     ```
     source  ~/.bashrc 
     ```
	       
 4. To check whether code is commited or not.
	  
     ```
     cat .bashrc
     ```
     	
#### Modification 2

 1. Run the below command to edit the hadoop-env.sh file.

     ```
     sudo nano $HADOOP_HOME/etc/hadoop/hadoop-env.sh
     ```
	
 2. Add the below lines for adding the Java path, save it and exit .
	
     ```
     export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
     ```
	
#### Modification 3 

 1. Run the below command to edit the core-site.xml file. 

     ```
     sudo nano $HADOOP_HOME/etc/hadoop/core-site.xml
     ```
		
 2. Add the following code within configuration tags, save it and exit .	
	
     ```
     <property>
     <name>hadoop.tmp.dir</name>
     <value>/home/hdoop/tmpdata</value>
     <description>A base for other temporary directories.</description>
     </property>
     <property>
     <name>fs.default.name</name>
     <value>hdfs://localhost:9000</value>
     <description>bla bla</description>
     </property>
     ```
																		
#### Modification 4
																				
1. Run the below command to edit the hdfs-site.xml file. 
	
     ```
     sudo nano $HADOOP_HOME/etc/hadoop/hdfs-site.xml
     ```
2. Add the following code within configuration tags, save it and exit .
		
     ```
     <property>
     <name>dfs.data.dir</name>
     <value>home/hdoop/dfsdata/namenode</value>
     </property>
     <property>
     <name>dfs.data.dir</name>
     <value>home/hdoop/dfsdata/datanode</value>
     </property>
     ```
		
#### Modification 5 

1. Run the below command to edit the mapred-site.xml file. 
	
     ```
     sudo nano $HADOOP_HOME/etc/hadoop/mapred-site.xml
     ```
		
2. Add the following code within configuration tags, save it and exit .
		
     ```
     <property>
     <name>mapreduce.framework.name</name>
     <value>yarn</value>
     </property>
     ```
		
#### Modification 6 

1. Run the below command to edit the yarn-site.xml  file. 
	
   ```
   sudo nano $HADOOP_HOME/etc/hadoop/yarn-site.xml
   ```
		
2. Add the following code within configuration tags, save it and exit .
		
   ```		
   <property>
   <name>yarn.nodemanager.aux-services</name>
   <value>mapreduce_shuffel</value>
   </property>
   <property>
   <name>yarn.nodemanager.aux-services.mapreduce_shuffel.class</name>
   <value>org.apache.hadoop.mapred.ShuffleHandler</value>
   </property>
   <property>
   <name>yarn.resourcemanager.hostname</name>
   <value>127.0.0.1</value>
   </property>
   <property>
   <name>yarn.acl.enable</name>
   <value>0</value>
   </property>
   <property>
   <name>yarn.nodemanager.env-whitelist</name>
   <value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME</value>
   </property>
   ```

After all 6 modifications, follow the below instrutions.

1. Logout from your individual user.

   	```
	logout
	```
	
2. Navigate to your existing user ( hadoopuser).

	```
	su - hadoopuser
	```
	
4. Start the SSH 

	```
	sudo service ssh start 
	```

3. To check the status of localhost 

	```
	sudo service ssh status
	```
	
4. Now navigate into individual user

	```
	su - hdoop
	```

5. Check if localhost works or not

	```
	ssh localhost 
	```

6. To Format the New Hadoop File system

	```
	hdfs namenode -format
	```
	
7. Navigate to /sbin.

	```
	cd ~/hadoop-3.3.4/sbin
	```
	
8. Starting dfs

	```
	./start-dfs.sh
	```
	
9. Starting YARN.

	```
	./start-yarn.sh
	```
10. Checking daemons

	```
	jps
	```

12. Checking HDFS Web UI on any browser.

	```
	http://localhost:9870
	```
	
13. Checking whether hadoop commands are running or not.

	```
	hdfs dfs -ls /
	```

14. Navigate to your group user.

	```
	su - hadoopuser
	```

15. Create an empty file inside ``/home/hadoopuser/``

	```
	mkdir example.txt
	```

16. Again login to ``hdoop`` user 

	```
	su - hdoop
	```
	
18. Now try copying the file from local to hdfs path. 

	```
	hdfs dfs -put /home/hadoopuser/example.txt / 
	```
	
15. Check if the file is copied or not .

	```
	hdfs dfs -ls /
	```



    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
    
  
 
 
