---
layout: post
title: Microsoft Azure Data Warehouse
---
Pick a region, choose source and create a server. BOMB, you have a data warehouse you scale up and down at any time on Microsoft Azure.

Then, we should connect to our server by server name and your authentication. Dont forget to set up firewall if you want to connect to the server. Now, we can run query. 
~~~
select @@version
~~~
Lets try powershell to create our warehouse
~~~
#setup your account
Login-AzureAccount

#verfiy your subscriptions
Get-AzureRmSubscription

#create a new datawarehouse
New-AzureRmSqlDatabase -RequestedServiceObjectiveName "DW100"
-Databasename ""
-ServerName ""
-ResourceGroupName ""
-Edition ""
~~~
Next, we are gonna dig into atual design. Consideration for fact table and dimension table. We use Hash Distribution to hash the product into different nodes. 
 In this case, we want evenly distribution with a good hash key. 

Data Types, choose data types wisely to save space. The most common table type is clustered B-Tree Index, we use the column as the clustering key.  Heap provides has no index on the data. Table Partitioning is very common. A partition is a small piece of a database table. It allows tables, indexes, or index-organized tables to be subdivided into smaller pieces. 

For Fact Tables, Large ones are better as Columntores. Distributed through Hash key as much as possible as long as it is even. Dimension tables are usually small, we can just use Heap for small dimensions. We dont recommend partition for dimention table. 

Here is an sample of SQL 
~~~
SELECT 
    p.productkey + (a.number * 1000) AS ProductKey
    p.EnglishProductName + CONVERT(VARCHAR, (a.number*1000)) AS EngishProductName,
    p.ProductAlternateKey + '-' + COVERT(VARCHAR, (a.number*1000)) AS PPP
    p.Color
From table zmq
~~~ 
select cp.[distribution],count(*) distributionRecords from (
select row_number() over(order by (select null)) rowNum from FactTransaction) subq 
cross apply (select rowNum%60 [distribution]) cp
group by [distribution]
order by [distribution];

select cs.name,tt.name from sys.columns cs inner join sys.types tt
on cs.system_type_id=tt.system_type_id where object_id = OBJECT_ID('Fact');

select count(distinct ProductKey)
from FactTransactionHistory;
~~~
Loading data in data warehouse. There are numerous methods for it. The first one is MPP. Another thing is to avoid ordered data. It can introduce hot spot that slow down the process. We can load csv into temporary table.

Different loading methods include single-client loading methods AND parellel readers loading methods. Control nodes receives connections and start the query.

big data pipelines, we start from loading data, we can see we create table struture by define the name and data type(length for varchar). Loading with PolyBase . Imagine we have csv in Azure Blob storage. Dont forget to format txt file into csv style and do some hash to the ProductKey. 
