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
CREATE EXTERNAL TABLE IF NOT EXISTS default.all_stock_1
(d date, open float, high float, low float, close float, name string)
ROW FORMAT DELIMITED
FIELDS TERMINATED BY ','
STORED AS TEXTFILE
LOCATION 'hdfs://user/ubuntu/all_stocks_5yr.csv';
```

6. Import folder to hive table
