# kafka installation
1) Update the package repository cache
   - sudo apt-get update
1) Install jdk
  - sudo apt-get install openjdk-8-jdk
2) Install zookeeper
  - sudo apt-get install zookeeperd 
3) Download kafka
  - wget http://www-eu.apache.org/dist/kafka/1.0.0/kafka_2.12-1.0.0.tgz
4) Create a directory 
  - sudo mkdir /opt/Kafka
5) Extract archive
  - sudo tar xvzf kafka_2.12-1.0.0.tgz -C /opt/Kafka
6) Add it to path
  - cd /etc/profile.d/
  - vim kafka.sh
7) Add followingn lines to kafka.sh 
   export KAFKA_HOME="/opt/kafka/kafka_2.12-1.0.0"
   JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64
   export PATH=${KAFKA_HOME}/bin:${PATH}
8) Now make it executable and apply configuration
  - chmod +x kafka.sh
  - source kafka.sh
9) Make a symbolic link of Kafka server.properties file  
  - sudo ln -s $KAFKA_HOME/config/server.properties /etc/kafka.properties
10) Reboot the system
11) Start zookeeper
   - sudo systemctl start zookeeper
12) Check status
   - sudo systemctl status zookeeper
    zookeeper system start up file is located at /etc/systemd/system/multi-user.target.wants/zookeeper.service
13) Start kakfa
    -sudo kafka-server-start.sh /etc/kafka.properties