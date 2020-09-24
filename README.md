
# Kafka-software-installation
We will learn to install kafka and zookeeper. Then we will learn to use the produce and consumer of kafka after lunching it.
### Install of Prerequisite software Maven & OpenJDK

Install (or upgrade) Maven and OpenJDK and verify.  (If you already have them, you might run choco upgrade all -y instead. )
choco install maven -y
choco install openjdk -y
refeshenv
choco list -l
java --version
mvn -v

### Install Kafka (comes with ZooKeeper)

Go to Kafka Quickstart, download the current source tgz file to C:\.
Un-tar it (using Bash) and change into the directory.  The $ indicates a Bash prompt.
tar -xzf <filename>
cd <folder>
What subfolders are there? You must be able to view file extensions.
Explore: What types of files are in:
bin
bin/windows
config (view some of the properties files)
libs
What files do we modify to configure our installation?

### Install Environment Variables

Windows + Edit the System Environment Variables / Environment Variables / System variables (bottom half). Note:  Use the version you installed in the following. 
JAVA_HOME = C:\Program Files\OpenJDK\jdk-version folder
KAFKA_HOME =  C:\kafka-version folder
M2_HOME = C:\ProgramData\chocolatey\lib\maven\apache-maven-version
Path - must include (make sure you have only one JDK location in your path!)
%JAVA_HOME%\bin OR C:\Program Files\OpenJDK\jdk-version\bin (or similar, NOT both!)
%M2_HOME%\bin
%KAFKA_HOME%\bin
%KAFKA_HOME%\bin\windows
## Starting services through kafka
Use a different PowerShell as Administrator window for each process.  You can minimize windows, but dont close them. They must remain  open to keep the processes running.
The topic I created is my-bucketlist. Replace my-bucketlist with your topic.
### Window 1 - Run Zookeeper Service  (keep window open)

.\bin\windows\zookeeper-server-start.bat .\config\zookeeper.properties

### Window 2 - Run Kafka Service (keep window open)

.\bin\windows\kafka-server-start.bat .\config\server.properties

### Window 3 (temporary) - Execute One-Time Commands - create, list, delete topics 

.\bin\windows\kafka-topics.bat --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --create --topic my-bucketlist
.\bin\windows\kafka-topics.bat --zookeeper localhost:2181 --list

### Window 4 - Run Kafka Producer (will provide a > prompt for writing messages)

.\bin\windows\kafka-console-producer.bat --broker-list localhost:9092 --topic my-bucklist

### Window 5 - Run Kafka Consumer (to show messages from the beginning)

.\bin\windows\kafka-console-consumer.bat --bootstrap-server localhost:9092 --topic my-bucketlist --from-beginning

### >>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>>
