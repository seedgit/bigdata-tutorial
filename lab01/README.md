# Lab 01

1. Download sp500.zip to your virtual machine
2. Extract file 
```
  $cd /home/ubuntu/Downloads/
  $unzip sp500.zip
```
3. Upload 
4. Import specific file to hive table
- Go to hive console
```
  $cd /home/ubuntu/hive
  $bin/beeline -u jdbc:hive2://
```
- create table "all_stock_1"
```
CREATE EXTERNAL TABLE IF NOT EXISTS all_stock_1
(`date` date,open float,high float,low float,close float, volume int,Name string)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
STORED AS TEXTFILE;
```
- load data from local drive to hive table (put file to hdfs + mapping file to hive table)
```
LOAD DATA LOCAL INPATH '/home/ubuntu/Download/all_stocks_5yr.csv' overwrite into table all_stock_1;
```

- test by query to table all_stock_1. e.g.,
```
select * from all_stock_1 limit 100;
```
6. Import folder to hive table
- create table "all_stock_2"
```
CREATE EXTERNAL TABLE IF NOT EXISTS all_stock_2
(`date` date,open float,high float,low float,close float, volume int,Name string)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
STORED AS TEXTFILE;
```
- load data from local drive to hive table (put file to hdfs + mapping file to hive table)
```
LOAD DATA LOCAL INPATH '/home/ubuntu/Download/' overwrite into table all_stock_1;
```

- test by query to table all_stock_1. e.g.,
```
select * from all_stock_1 limit 100;
```

hive -e 'select CONCAT_WS(',',cola,colb,colc...,coln) from Mytable' > /home/user/Mycsv.csv
