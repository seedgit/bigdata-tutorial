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

# Install HIVE
