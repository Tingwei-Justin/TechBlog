Ctrl + z 挂起运行的程序

jobs查询后台运行的程序

bg %id 让某任务在后台运行

fg 将后台中的命令调至前台继续运行





Installing MongoDB for Windows and OS X

- Why Mongo?
- Document-oriented data
- Exploring the Mongo shell
- Importing data into the database
- Building an application in Node.js
- Tuning Mongo queries
- Aggregation
- Replication and sharding



## Relational database vs NoSql Databases

Relational Databases:

- Powerful, flexible, constrained.
- Designed for database administrators

Nosql Daabases

- Document model more closely matches code objects
- Designed for developer
  - JSON representation
  - javascript shell commands
  - excellent drivers
  - used by companies with extensive data needs



## MongoDB Document Structure

- Documments = JSON objects
- Store data as BSON (Binary JSON)
- Easy to access related information
- Flexiable indexing capability
- Easy to adapt to common coding practices

```json
{ 
    "_id" : ObjectId("5f01855f402238f5a6a04439"), 
    "ID" : "1", 
    "Make" : "Volkswagen", 
    "Model" : "Passat", 
    "Trim" : "SE", 
    "BodyStyle" : "Sedan", 
    "Color" : "Black" 
}
```

Fields and values,

JSON 

ID Field

- required field
- unique accross a collection
- auto-assigned if not specified

Embedded Data

- Easier to work with
- Minimized coding operations
- Easier to query and index

Include by Reference

- More operations for inserting and access
- Aggregating data can be complex
- Enables consistent data

Features of Mongo

Mongo does have features to support database'scomplexity, while maintain the scalability, performance, and reliability.

- Indexing
  - indexing provides perforamence improvements
  - Ad hoc queries are expensive
  - Large datasets can lose performance
  - Indices are even useful for very simple data
- Mongo indexing features (support complex)
  - 64 indsingle field
  - compound
  - unique

- Sharding: (scalability)
  - partitions data onto different machines
  - provides scalability. Via software
  - autosharding supported by MOngo
  - challenging to set up

- Replication (Reliability)
  - reliablity 
  - Maximizes uptime
  - Replica sets
  - Automatic failover



### Explore the mongo shell

- `db`

- `use db_name`

- `show dbs` : show database

- `show collections`

- use `createIndex` to reduce execution time

- `.pretty()` : an easy-to-read *format*

  ```javascript
  for (i = 0; i < 10000; i++) {
  	db.numbers.insert(
  		{"number" : i}
  	)
  }
  ```

  ```javascript
  db.number.count() // 10000
  ```

  ```javascript
  db.numbers.find({"number" : 1})
  ```

  ```javascript
  db.numbers.find({"number" : 1}).explain()
  db.numbers.find({"number" : 1}).explain("executionStats")
  
  //For an ascending index on a field, specify a value of 1; for descending index, specify a value of -1.
  db.numbers.createIndex({number: 1})
  db.numbers.find({"number" : 1}).explain("executionStats")
  
  ```

- Import the data into the database

  ```
  mongoimport --help  // see all possible uses
  mongoimport --db learning_mongo --collection tours --jsonArray --file tours.json
  ```

- Mongo shell operations

  ```javascript
  // add a new fields
  db.tours.update({"tourName" : "..."},
  	{$set: {"tourRegion":"Central Coast"}}
   )
  
  // add a new entry without remove anything
  db.tours.update({"tourName" : "..."},
  	{$addToSet: {"tourTags":"new tag"}}
   )
  
  // remove a field
  db.tours.remove("tourName":"...")
  
  // drop a collection
  db.tours.drop()
  ```

- Mongo Index

  We don't want to check every docs when we search some data, so we use index to accelerate the speed

  ```javascript
  //For an ascending index on a field, specify a value of 1; for descending index, specify a value of -1.
  db.numbers.createIndex({number: 1})
  db.numbers.find({"number" : 1}).explain("executionStats")
  ```

  if we consistantly run the performance issue with the queries, we should consider whether the index helps the request. 

- Unique indexes

  add some constraints to the data

  db.collections.createIndex{{indexName: 1}, {unique: true}}

- text indexes for search

- aggregation

  ![image-20200707220653963](../../Library/Application Support/typora-user-images/image-20200707220653963.png)





## Replication and sharding 

- replication

  - Full copies of dataset
  - primary and secondary servers
  - automatic failover

  it works by creating a replica set

  the servers elect a primary

  if the primary goes down, a new primary is elected

  when the old primary comes up, it's brought in as a secondary

- sharding

  - partition your database 
  - More storage and greater capacity
  - multiple CPUs and memory
  - Operates as a single database for clients
  - minor performance hit

  when to implement sharding

  - storage limitations
  - Memory constraints
  - load issues
  - when cost is prohibitive for a single server