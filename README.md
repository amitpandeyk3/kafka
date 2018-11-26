# Kafka installation

There are two ways to install kafka, one is directly on linux, another easier way is to use docker and docker-compose on
any platform for which I have added docker-compose file with project

# Installation on debian based linux
1. Update the package repository cache and install JDK
   - sudo apt-get update
   - sudo apt-get install openjdk-8-jdk
2. Install maven
   - cd /opt
   - wget http://www-eu.apache.org/dist/maven/maven-3/3.5.3/binaries/apache-maven-3.5.3-bin.tar.gz
   - tar -xf apache-maven-3.5.3-bin.tar.gz
   - mv apache-maven-3.5.3/ apache-maven/
3. Install zookeeper
  - sudo apt-get install zookeeperd 
4. Download kafka
  - wget http://www-eu.apache.org/dist/kafka/1.0.0/kafka_2.12-1.0.0.tgz
5. Create a directory 
  - sudo mkdir /opt/Kafka
6. Extract archive
  - sudo tar xvzf kafka_2.12-1.0.0.tgz -C /opt/Kafka
7. Add it to path
  - cd /etc/profile.d/
  - vim kafka.sh
8. Add followingn lines to kafka.sh 
   - export KAFKA_HOME="/opt/kafka/kafka_2.12-1.0.0"
   - export M2_HOME=/opt/apache-maven
   - export MAVEN_HOME=/opt/apache-maven
   - JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
   - export PATH=${M2_HOME}/bin:${KAFKA_HOME}/bin:${PATH}
9. Now make it executable and apply configuration
  - chmod +x kafka.sh
  - source kafka.sh
10. Make a symbolic link of Kafka server.properties file  
  - sudo ln -s $KAFKA_HOME/config/server.properties /etc/kafka.properties
11. Reboot the system
12. Start zookeeper
   - sudo systemctl start zookeeper
13. Check status
   - sudo systemctl status zookeeper
14. Start kakfa
   - sudo kafka-server-start.sh /etc/kafka.properties

# Testing installation
1. Create test topic
  - sudo kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1
    --partitions 1 --topic testing
2. Send some test messages by running below command and than pressing enter to get promt(>) to enter messages
  - sudo kafka-console-producer.sh --broker-list localhost:9092 --topic testing
3. Open another terminal to run consumer to fetch messages from same topic
   -  sudo kafka-console-consumer.sh --zookeeper localhost:2181 --topic testing --from-beginning