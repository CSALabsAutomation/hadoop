#    Steps for installing Kafka

1. Open the WSL [Ubuntu] terminal and navigate to your individual user.[ hdoop ] 

    ```
    su - hdoop
    ```
    
2.  Create a folder named as kafka

    ```
    mkdir kafka
    ```
    
3.  Navigate to the kafka folder

    ```
    cd kafka
    ```
    
4.  Downloading Spark by using wget command in a specified location.

    ```
    wget https://downloads.apache.org/kafka/3.3.1/kafka_2.13-3.3.1.tgz
    ```
    
5.  Extracting the downloaded tar file in Linux machine by using tar command.

    ```
    tar -xvf kafka_2.13-3.3.1.tgz
    ```
    
6.  Come out of spark folder by typing `cd` and run the below command to open bashrc file.

    ```
    sudo nano .bashrc
    ```
    
7.  Add the below lines to configure Kafka path at the end. Save[CTRL + S] the file and Quit[CTRL + X]. Also make sure SPARK_HOME path is correctly given.

    ```
    export KAFKA_HOME=/home/hdoop/kafka/kafka_2.13-3.3.1
    ```

8.  Reload the modified code.
	
    ```
    source  ~/.bashrc
    ```

9.  Navigate to the kafka folder by running the below command

    ```
    cd $KAFKA_HOME
    ```
    

### Start Kafka environment

1.  Start ZooKeeper services by running this command. 

    ```
    $KAFKA_HOME/bin/zookeeper-server-start.sh $KAFKA_HOME/config/zookeeper.properties
    ```
    
2.  Start Kafka server 

    > Open another WSL terminal and run the following command:

    ```
    $KAFKA_HOME/bin/kafka-server-start.sh $KAFKA_HOME/config/server.properties

    ```
    
    Once all the services are launched, you will have a Kafka environment ready to use.
    

3.  You can verify by running jps command in a third WSL terminal (You should have Hadoop installed in your environment)
 
    ```
    jps -ml
    ```

### Testing Kafka 

1.  Create a Kafka topic
    
    In the third terminal window, run the following command:

    ```
    $KAFKA_HOME/bin/kafka-topics.sh --create --topic kontext-events --bootstrap-server localhost:9092
    ```

    > The command will create a topic named kontext-events as the above screenshot shows.

2.  Describe Kafka topic

    Run the following command to describe the created topic.

    ```
    $KAFKA_HOME/bin/kafka-topics.sh --describe --topic kontext-events --bootstrap-server localhost:9092
    ```
    

3.  Write some events into the topic

    Let's start to write some events into the topic by running the following command:

    ```
    $KAFKA_HOME/bin/kafka-console-producer.sh --topic kontext-events --bootstrap-server localhost:9092
    ```

    > Each line represents an event. Let's type into some events.


     ```
     This is the first event.
     This is the second event.
     This is the third event.
     ```

     > Press Ctrl + C to terminate this Console producer client. 

4.   Read the events in the topic

     Let's read the events by running the following command:

     ```
     $KAFKA_HOME/bin/kafka-console-consumer.sh --topic kontext-events --from-beginning --bootstrap-server localhost:9092
     ```














