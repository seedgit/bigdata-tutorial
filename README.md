# bigdata-tutorial

## This tuotrial is specifict for
- Ubuntu 20.04
- Hadoop 3.2.2
- HIVE 3.1.2
- Sqoop 1.4.7
- Flume 1.9
- Spark 3.1.1

** If you use this tutorial virtual machine image. All software are download at ```/home/ubuntu/Downloads```

# Install required program

1. Open Terminal
2. Install SSH by type 
```
  $ sudo apt-get install ssh
```
4. Install OpenJDK-8 by type 
```
  $ sudo apt-get install openjdk-8-jdk
```
6. Config passphraseless ssh

```  
  $ ssh-keygen -t rsa -P '' -f ~/.ssh/id_rsa
  $ cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
  $ chmod 0600 ~/.ssh/authorized_keys
```

# Install and test Hadoop

1. Extract Hadoop into ```/home/ubuntu```
```
  $ tar -xzf /home/ubuntu/Downloads/hadoop-3.2.2.tar.gz
```
2. Rename 
```
  $ mv /home/ubuntu/hadoop-3.2.2 /home/ubuntu/hadoop
```
3. Config etc/hadoop/hadoop-env.sh
4. Config etc/hadoop/core-site.xml
5. Config etc/hadoop/hdfs-site.xml
6. Test hadoop



# Install HIVE
