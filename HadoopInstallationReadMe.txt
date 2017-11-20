Before installing Hadoop into the Linux environment, we need to set up Linux using ssh (Secure Shell). Follow the steps given below for setting up the Linux environment.
Creating a User:
Open the root using the command “su”.
Create a user from the root account using the command “useradd username”.
Now you can open an existing user account using the command “su username”
Open the Linux terminal and type the following commands to create a user.

$ su 
   password: 
# useradd hadoop 
# passwd hadoop 
   New passwd: 
   Retype new passwd 
   
Generate ssh keys in the following way:

$ ssh-keygen -t rsa 
$ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys 
$ chmod 0600 ~/.ssh/authorized_keys    

Download and extract Hadoop 2.4.1 from Apache software foundation using the following commands.

$ su 
password: 
# cd /usr/local 
# wget http://apache.claz.org/hadoop/common/hadoop-2.4.1/ 
hadoop-2.4.1.tar.gz 
# tar xzf hadoop-2.4.1.tar.gz 
# mv hadoop-2.4.1/* to hadoop/ 
# exit 

Once you have downloaded Hadoop, to start hadoop in standalone mode:

Local/Standalone Mode : After downloading Hadoop in your system, by default, it is configured in a standalone mode and can be run as a single java process.

Set up Hadoop environment variables by appending the following commands to ~/.bashrc file.

export HADOOP_HOME=/usr/local/hadoop 

Once hadoop is installed you can check it by typing
Hadoop version

Run a sample program which will be already there in hadoop folder

$HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-examples-2.2.0.jar 

we will run a word count program which is already there in jar we just need to provide the input.

Create an wordcountinputfile file with different words inside it once create run the following command for wordcount program.

$ hadoop jar $HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduceexamples-2.2.0.jar  wordcount wordcountinputfile result 

the output of the program is stored in result

$cat result 

this will have all the words in the file

To run Hadoop in distributed mode psuedo
open bashrc file and add hadoop home in it

To do hadoop configuration:

find all the Hadoop configuration files in the location “$HADOOP_HOME/etc/hadoop”. 

To develop hadoop program in java resest java environment variable hadoop-env.sh file by replacing JAVA_HOME value .

Edit core-site.xml which contains port number used for hadoop instance
Edit hdfs-site.xml which contains information of  datanode paths namenode paths.
Edit yarn-site.xml and add the below inside configuration tag
<property>
      <name>yarn.nodemanager.aux-services</name>
      <value>mapreduce_shuffle</value> 
   </property>

 Edit mapred-site.xml contains which mapreduce we are using Add the following between configuration tag
  <property> 
      <name>mapreduce.framework.name</name>
      <value>yarn</value>
   </property>

Setup name node with “hdfs namenode -format”
verify by hadoop dfs with start-dfs.sh 
verfy yarn script with start-yarn.sh 
TO access hadoop from browser follow the below url default port for hadoop is 50070
http://localhost:50070/