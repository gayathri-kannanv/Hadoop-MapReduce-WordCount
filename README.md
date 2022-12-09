# Hadoop-MapReduce-WordCount

Hadoop is a framework that uses distributed storage and parallel processing to store and manage big data. 

Hadoop has three components-
1) Hadoop HDFS - Hadoop Distributed File System (HDFS) is the storage unit.
2) Hadoop MapReduce - Hadoop MapReduce is the processing unit.
3) Hadoop YARN - Yet Another Resource Negotiator (YARN) is a resource management unit.

## Installation: 

1.	Download and install JDK 
https://www.oracle.com/in/java/technologies/downloads/#jdk19-windows 

2.	Extracting the hadoop 3.3.0 tar file- 
https://archive.apache.org/dist/hadoop/common/hadoop-3.2.1/hadoop-3.2.1.tar.gz 

3.	Adding hadoop winutils files to bin. (check same version) 
https://github.com/kontext-tech/winutils/tree/master/hadoop-3.2.1/bin 

4.	Adding the hadoop files and jdk files to a right directory.( copy paste jdk files from Program files) 

5.	Add Hadoop and jdk path to Environment VARIABLES.

6.	Also, in Path- add the paths as below:
 ![image](https://user-images.githubusercontent.com/60387180/206688365-2edbdf14-d3a0-405f-b2ec-b479ecb85bff.png)


7.	Open CMD and check Hadoop version.
 ![image](https://user-images.githubusercontent.com/60387180/206688394-82f35016-88fa-43cb-977d-e732e4251b31.png)


8.	Startup commands for running the nodes from Hadoop-3.2.1/sbin> are:
.\start-dfs.cmd 
.\start-yarn.cmd 

If you face any error, follow the below steps further.

9.	 Configuring Hadoop cluster

There are four files we should alter to configure Hadoop cluster:
1.	%HADOOP_HOME%\etc\hadoop\hdfs-site.xml
2.	%HADOOP_HOME%\etc\hadoop\core-site.xml
3.	%HADOOP_HOME%\etc\hadoop\mapred-site.xml
4.	%HADOOP_HOME%\etc\hadoop\yarn-site.xml


9.1. HDFS site configuration

Hadoop is built using a master-slave paradigm. Before altering the HDFS configuration file, we should create a directory to store all master node (name node) data and another one to store data (data node). In this example, we created the following directories:
•	E:\hadoop-env\hadoop-3.2.1\data\dfs\namenode
•	E:\hadoop-env\hadoop-3.2.1\data\dfs\datanode

Now, open “hdfs-site.xml” file located in “%HADOOP_HOME%\etc\hadoop” directory, and add the following properties within the <configuration></configuration> element:
<property><name>dfs.replication</name><value>1</value></property><property><name>dfs.namenode.name.dir</name><value>file:///E:/hadoop-env/hadoop-3.2.1/data/dfs/namenode</value></property><property><name>dfs.datanode.data.dir</name><value>file:///E:/hadoop-env/hadoop-3.2.1/data/dfs/datanode</value></property>


9.2. Core site configuration

Now, configure the name node URL by adding the following XML code into the <configuration></configuration> element within “core-site.xml”:
<property><name>fs.default.name</name><value>hdfs://localhost:9820</value></property>


9.3. Map Reduce site configuration

Now, add the following XML code into the <configuration></configuration> element within “mapred-site.xml”:
<property><name>mapreduce.framework.name</name><value>yarn</value><description>MapReduce framework name</description></property>


9.4. Yarn site configuration

Now, add the following XML code into the <configuration></configuration> element within “yarn-site.xml”:
<property><name>yarn.nodemanager.aux-services</name><value>mapreduce_shuffle</value><description>Yarn Node Manager Aux Service</description></property>


10.	 Formatting Name node

After the configuration, we’ll format the name node using the following command:
hdfs namenode -format

If you face any error, this issue will be solved within the next release. For now, you can fix it temporarily using the following steps:
1.	Download hadoop-hdfs-3.2.1.jar file from the following link- https://github.com/FahaoTang/big-data/blob/master/hadoop-hdfs-3.2.1.jar.
2.	Rename the file name hadoop-hdfs-3.2.1.jar to hadoop-hdfs-3.2.1.bak in folder %HADOOP_HOME%\share\hadoop\hdfs
3.	Copy the downloaded hadoop-hdfs-3.2.1.jar to folder %HADOOP_HOME%\share\hadoop\hdfs

11.	Start the Hadoop services now from Hadoop for running the nodes from -
Hadoop-3.2.1/sbin>
.\start-dfs.cmd 
.\start-yarn.cmd 

## Running a prebuilt example of a Map Reduce program

1.	Navigate to mapreduce directory on hadoop. 
\hadoop-3.3.0\share\hadoop\mapreduce>  hadoop jar hadoop-mapreduce-examples-3.3.0.jar 
![image](https://user-images.githubusercontent.com/60387180/206688605-8993448b-f490-440d-848c-94607033bac4.png)

  
2.	Executing word count program of map reduce. 
3.	Have a text file containing the words in multiple lines. 
Deer Rabbit Fox Dog 
Dog Rabbit Deer 
Deer Deer Fox Dog 
Rabbit Fox Rabbit 
Deer Rabbit Fox 
 
4.	Start the hadoop clusters- nodes and yarn managers from hadoop/sbin directory. 
.\start-dfs.cmd 
.\start-yarn.cmd 
 
5.	To move the input file to hdfs root, Run the command from mapreduce directory- 
\hadoop-3.3.0\share\hadoop\mapreduce> hadoop dfs -put E:/RapidData/Learning/HadoopHive/hadoop-env/hadoop-3.3.0/examples/words.txt / 
 
6.	Check and display from hdfs- 
\hadoop-3.3.0\share\hadoop\mapreduce> hadoop dfs -cat /words.txt 
![image](https://user-images.githubusercontent.com/60387180/206688655-375920ec-bc16-494e-8f6f-b3fdfaa1e78e.png)

  
7.	Run the mapreduce program. 
\hadoop-3.3.0\share\hadoop\mapreduce> hadoop jar hadoop-mapreduce-examples-3.3.0.jar wordcount /words.txt /FirstExampleOut 
  ![image](https://user-images.githubusercontent.com/60387180/206688680-8d69b2ee-28b0-446a-9008-b31ac5dfbe37.png)

8.	Check if the output file is available. 
\hadoop-3.3.0\share\hadoop\mapreduce> hadoop dfs -ls /FirstExampleOut 
  
9.	Display the output from the file. 
\hadoop-3.3.0\share\hadoop\mapreduce> hadoop dfs -cat /FirstExampleOut/part-r-00000 
 ![image](https://user-images.githubusercontent.com/60387180/206688703-5740f322-f0b5-441e-b251-df479162e28d.png)


Thus, the count of each occurences of the words in the file are done.
