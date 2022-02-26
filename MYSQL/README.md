# MYSQL INSTALLATION - WINDOWS 10
MySQL version used in this tutorial: MySQL Community Server 8.0.28

---

## DOWNLOAD THE FILES
1. Download MySQL zip file from [here](https://dev.mysql.com/downloads/mysql/)

2. Extract the content of the zip file and paste it in a new folder named mysql under the C drive
- ![download](/images/mysql/mysql_1.png)
3. Create a folder where the data will be stored, for example `C:\mysqldata`
- ![download](/images/mysql/mysql_2.png)
---
## SPECIFY FILE APPLICATION AND DATA FOLDERS
1. Create a my.ini file in `C:\mysql`
- ![download](/images/mysql/mysql_3.png)

2. Edit the file with the following text that will specify the application and data folders:
```
[mysqld]
# installation path
basedir=C:/mysql
# data directory
datadir=C:/mysqldata
```
- ![download](/images/mysql/mysql_4.png)
---
## INITIALIZE DATA FOLDER AND root USER

1. Open the command prompt as administrator 
2. run the following command to initialize the data folder and root user:  
```
C:\mysql\bin\mysqld.exe --initialize-insecure --user=mysql
```
- ![download](/images/mysql/mysql_5.png)
---
## MYSQL AS AUTO STARTING WINDOWS SERVICE
1. Install MySQL as an auto starting Windows service by running the following command:
```
C:\mysql\bin\mysqld.exe –install
```
- ![download](/images/mysql/mysql_6.png)

2. Start the services from the services console.
- ![download](/images/mysql/mysql_7.png)
---
## TEST
1. Open the command prompt
2. Type the following command.
```
C:\mysql\bin\mysql.exe -u root
```
3. Onece mysql shows type the following SQL command:
```
show databases;
```
4. If everything is working you should see a screen similar to this one:
- ![download](/images/mysql/mysql_8.png)
---