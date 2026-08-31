1.DROP EXTERNAL TABLE ActivityLog;

2.DROP EXTERNAL DATA SOURCE srcActivityLog;

3\.

4.CREATE MASTER KEY ENCRYPTION BY PASSWORD = **'P@ssword@123';**

5\.

6.CREATE DATABASE SCOPED CREDENTIAL sasToken

7.WITH IDENTITY = 'SHARED ACCESS SIGNATURE',

8.SECRET = '**c0py \& paste your toke**n';

9\.

10.CREATE EXTERNAL DATA SOURCE srcActivityLog

11.WITH (

12\.   LOCATION = 'https://datalake4000050.blob.core.windows.net/data',

13\.   CREDENTIAL = sasToken

14\. );

15\.

16\. CREATE EXTERNAL FILE FORMAT parquetFileFormat

17\. WITH (

18\.    FORMAT\_TYPE = PARQUET,

19\.    DATA\_COMPRESSION = 'org.apache.hadoop.io.compress.SnappyCodec'

20\.  );

21\.

22.CREATE EXTERNAL TABLE ActivityLog

23.(

24\.   \[Correlationid] varchar(200),

25\.   \[Operationname] varchar(300),

26\.   \[Status] varchar(100),

&#x20;  \[Eventcategory] varchar(100),

&#x20;  \[Level] varchar(100),

&#x20;  \[Time] varchar(100),

&#x20;  \[Subscription] varchar(200),

&#x20;  \[Eventinitiatedby] varchar(1000),

&#x20;  \[Resourcetype] varchar(300),

&#x20;  \[Resourcegroup] varchar(1000),

&#x20;  \[Resource] varchar(2000))

WITH (

&#x20;   LOCATION='/ActivityLog01.csv',

&#x20;   DATA\_SOURCE=srcActivityLog,

&#x20;   FILE\_FORMAT=delimitedTxtFileFormat

)



SELECT \* FROM ActivityLog;

