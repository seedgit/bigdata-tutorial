# Hadoop, HIVE, Spark Installation guildline

## This guildline is specifict for
- Ubuntu 20.04
- Hadoop 3.2.2
- HIVE 3.1.2
- Sqoop 1.4.7
- Flume 1.9
- Spark 3.1.1

** If you use this tutorial virtual machine image. All software are download at ```/home/ubuntu/Downloads```, 
If you install ubuntu by yourself, you need to download requirement software by yourself.

# Install required program

1. Open Terminal
2. Install SSH
```
  $ sudo apt-get install ssh
```
3. Install OpenJDK-8 (Hadoop 3.2.2 can work with openjdk-8, if you are using different version please check [https://cwiki.apache.org/confluence/display/HADOOP/Hadoop+Java+Versions](https://cwiki.apache.org/confluence/display/HADOOP/Hadoop+Java+Versions))
```
  $ sudo apt-get install openjdk-8-jdk
```
4. Config passphraseless ssh

```  
  $ ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
  $ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
  $ chmod 0600 ~/.ssh/authorized_keys
```
If this step is success, you can try ```ssh localhost```, ssh should allow you to access without asking for password.
!Warning : if you are pass this step, make sure to exit sse by type ```exit``` in your terminal, or just re-open your terminal to make sure that your are not use ssh terminal.

# Install and test Hadoop
1. Make sure that your are at ```/home/ubuntu``` or type ```cd /home/ubuntu``` to move to this directory.
2. Extract Hadoop into ```/home/ubuntu```
```
  $ tar -xzf /home/ubuntu/Downloads/hadoop-3.2.2.tar.gz
```
3. Rename hadoop-3.2.2 to hadoop
```
  $ mv /home/ubuntu/hadoop-3.2.2 /home/ubuntu/hadoop
```
4. In ```/home/ubuntu/hadoop/etc/hadoop/hadoop-env.sh```, Open this file then search for ```# export JAVA_HOME=```

Add new line ```export JAVA_HOME=/usr/lib/jvm/java-8-openjdk-amd64``` and your file should be like
```
# export JAVA_HOME=
export JAVA_HOME=/urs/lib/jvm/java-8-openjdk-amd64
```

5. In ```/home/ubuntu/hadoop/etc/hadoop/core-site.xml```  Edit your file as follow
```
<configuration>
    <property>
        <name>fs.defaultFS</name>
        <value>hdfs://localhost:9000</value>
    </property>
</configuration>
```

6. Config ```/home/ubuntu/hadoop/etc/hadoop/hdfs-site.xml``` Edit your file as follow
```
<configuration>
    <property>
        <name>dfs.replication</name>
        <value>1</value>
    </property>
</configuration>
```
7. Format name node
```
  $bin/hdfs namenode -format
```
8. Start HDFS
```
  $cd /home/ubuntu/hadoop
  $sbin/start-dfs.sh
```

You can check result by command jps
```
  $jps
  16292 Jps
  12645 NameNode
  12076 DataNode
  12238 SecondaryNameNode
```

And you can check by go to [http://localhost:9870](http://localhost:9870). If browser show about NameNode information

# Install Resource manager (Yarn component)
1. edit ```etc/hadoop/mapred-site.xml```
```
<configuration>
    <property>
        <name>mapreduce.framework.name</name>
        <value>yarn</value>
    </property>
    <property>
        <name>mapreduce.application.classpath</name>
        <value>$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/*:$HADOOP_MAPRED_HOME/share/hadoop/mapreduce/lib/*</value>
    </property>
</configuration>
```
2. edit ```etc/hadoop/yarn-site.xml```
```
<configuration>
    <property>
        <name>yarn.nodemanager.aux-services</name>
        <value>mapreduce_shuffle</value>
    </property>
    <property>
        <name>yarn.nodemanager.env-whitelist</name>
        <value>JAVA_HOME,HADOOP_COMMON_HOME,HADOOP_HDFS_HOME,HADOOP_CONF_DIR,CLASSPATH_PREPEND_DISTCACHE,HADOOP_YARN_HOME,HADOOP_MAPRED_HOME</value>
    </property>
</configuration>
```
3. Start yarn component
```
  $sbin/start-yarn.sh
```
4. Check by ```jps``` it should show
```
  $jps
  16011 ResourceManager
  16121 NodeManager
  16292 Jps
  12645 NameNode
  12076 DataNode
  12238 SecondaryNameNode
```

# Install HIVE
1. Make sure that your are at ```/home/ubuntu```
```
  $cd /home/ubuntu
```
2. Extract hive to ```/home/ubuntu/```
```
  $tar -xzf /home/ubuntu/Downloads/apache-hive-3.1.2-bin.tar.gz
```
3. Rename apache-hive-3.1.2 to hive
```
  $mv apache-hive-3.1.2-bin hive
```
4. Set HADOOP_HOME
```
  $export HADOOP_HOME=/home/ubuntu/hadoop
```
5. Copy and update library in hive
```
  $cp /home/ubuntu/hadoop/share/hadoop/common/lib/guava-27.0.jre.jar /home/ubuntu/hive/lib
```
6. Remove old version of guava
```
  $rm /home/ubuntu/hive/lib/guava-17.0.jre.jar
```
7. Test your hive by ```bin/hive``` your terminal should show ```hive>```. You can exit hive by control+c
8. Remove exists metastore
```
  $rm -rf metastore_db
```
9. Init schema (create your metastore_db folder)
```
  $bin/schematool -dbType derby -initSchema
```
10. Run your hive
```
  $bin/beeline -u jdbc:hive2://
```
11. Create and test database table
```
  >CREATE TABLE pokes (foo INT, bar STRING);
  >SHOW TABLES;
  >INSERT INTO table pokes values(1, 'Hello world');
  >SELECT * FROM pokes;
```
