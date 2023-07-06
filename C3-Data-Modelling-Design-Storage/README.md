# Data Storage and Data Modeling

Data needs to be stored or recorded for future references and processing.  In 1986, approximately 1% of the world's capacity to store information was in digital format; this grew to 3% by 1993, to 25% by 2000, and to 97% by 2007. Data is growing in volume, variety and velocity than ever before. According to Forbes 2019, 90% of the world's data was generated in the last two years with 2.5 quintillion bytes data being created each day.

A modern digital computer represents data (numbers, text, images, audio, etc) using strings of binary numbers through different encodings like ASCII, UTF-8 for characters, JPEG for image encoding, MPEG-4 for video encoding and so on. A cosmic ray striking computer memory at just the right time can flip a bit, turning a 0 into a 1 or vice versa. This error is easily caught as its in power of 2, which happened in Belgian election 2003 where the votes were recounted and it showed that the person in question got exactly 4096 $2^12$ votes. By adding bits to each encoded unit, redundancy allows the computer to both detect errors in coded data and correct them based on mathematical algorithms and correct such bugs upon detection.

The Von Neumann machines stores operating instruction and data into memory. There's also a hierarchy of memory (storage). The memory or the primary storage is typically referred to as stored in Random-Access Memory while storage is considered as for long term storage devices or secondary memory. RAM memory device has a set of addresses lines and for each combination of bits applied to these lines, a set of memory cells are activated (64 cells for 64-bit microprocessors).  A 64 bit OS can theoretically address 2^64 bytes, thou no hardware yet bothers to exploit this huge range.

![ComputerMemoryHierarchy](https://upload.wikimedia.org/wikipedia/commons/0/0c/ComputerMemoryHierarchy.svg)

Data in Hard-disk and Solid State drive can be randomly read or written. Even though an OS can access data at individual byte level, the actual data is read in a fixed-length (block-size) sequence of bytes or bits called blocks (called physical record). Data thus structured are said to be blocked. While blocking (putting) or deblocking (extracting) the blocked data is stored in a data buffer. Block storage is normally abstracted by a file system or database management system (DBMS) for use by applications and end users.

Data is separated into pieces and each piece is given a name to easily isolate and identify the data. Each group of data is called a file, the structure and logic rules used to manage the groups of data and their filenames is called a file system. File system (fs) is the method and data structure that the OS uses to control how data is stored and retrieved. Most file systems (NTFS, EXT*,) are based on a block device abstraction which lead to space inefficiency due to internal fragmentation (multiple partially empty blocks). Some newer file systems like Btrfs and FreeBSD UFS2 attempts to solve this issue through block sub-allocation and tail merging, while ZFS support variable block sizes. File system manages the space, filenames, directories, metadata of files and directories along with access permissions and other file attributes, maintains file systems integrity.

Disadvantages of file-based data management system where data is stored in permanent files.

- Data redundancy: different departments stores a separate copy of the data, wastes storage space and duplicates the effort
- Data Inconsistency: the data may be store in inconsistent data format, updating one copy of the data doesn't change other copy of the data
- Data integrity problems: enforcing consistency constraints is diificult
- Data isolation: changes made by one operation might not become visible to other concurrent users and systems. it is difficult for new application to retrieve the appropriate data, which might be stored in various files.
- security issues: there are constraints regarding accessing privileges, application requirements are added to the system in an ad-hoc manner so it is difficult to enforce the constraints.
- Concurrency access: if a file is accessed its locked.

## Different File Systems

- Network File System
- Distributed Storage
  - Paper [Google File System](https://dl.acm.org/doi/pdf/10.1145/945445.945450)

Cloud Storage

- File Storage
- Block Storage
- Object Storage

## Data Modeling

Data Modeling is an abstraction that organizes elements of real world data and how they will relate to each other. We are used to create data models to manage our data in a spreadsheet, but it can't be used for operations on a large scale such as large number of sheets with millions of rows. Hence, we use a database to handle most of such data for different business process and user applications. A **database** is a structured repository or collection of (inter-related) data that is stored and retrieved under a pre-specified format and constraints for use in applications. Data can be stored, updated, or deleted from a database. Data Organization is critical for any application or business use cases. Organized data determines later data uses, if data is well organized, complicated queries can be simple. Hence, planning data organization and data modeling should start early and improved iteratively with new requirements and new data.

Evolution of Database

- 1968: File-based database: Data maintained in a flat file which can be accessed sequentially, indexed and in random fashion. eg storing in a CSV files (separate file per entity), application must parse the files for each read/update records. Scans through the whole database to find a value, scales in linear time. Has multiple issues with data integrity.
- 1968-1980s: Hierarchial Database (eg: IBM's Information Management System): files related in parent/child hierarchy, yet limited to handle many-to-many relationship, lack structural independence and complex implementation
- 1971: Network Data Model: Charles Bachman developed Integrated Data Store(IDS) at Honeywell, later Standardized by CODASYL. System was complex and difficult to design
- 1970s: Relational Database and DBMS: E.F. Codd proposed relational model with mathematical concepts.
- 1995: First Internet DBMS application was created

## Data Modeling Process

- Gather Requirements: map out what data are need to be stored and how it needs to be processed
  Some of the Requirements when a database is needed as as follows:
  - Scalability: Applications that have billions of rows or terabytes of data use DBMS.
  - Security: Applications that require a strict deposit of access to data in an organization use DBMS.
  - Consistency: Applications that require the data to remain consistent use DBMS. Data can become corrupt or inconsistent due to Lack of consistency constraints, Unsafe deletes, Overwriting, etc.  A typical DBMS provides ACID capabilities to ensure that the data remains consistent.
  - Availability: Applications that require the data to remain available throughout the lifetime use DBMS. A typical DBMS provides replication of servers to ensure the availability of data.

- Conceptual Data Modelling: Mapping the concept that we will have. Like a Giant white boarding process for managing entire data., eg entity mapping diagram
- Logical Data Modeling: Entity mapping to tables, columns and schema
- Physical Data Modeling: Transforming logical data modeling to database, table and schema with data definition language (DDL). Most database perform these operation almost the same.

## Relational Database

## Object-ORiented Databases

Contains data in form of objects and classes. Objects are treated as real-world entities and types as the category or collection of objects. Object-Oriented databases combines both relational model features with object oriented principles. OOP properties such as objects, classes, inheritance, polymorphism, encapsulation along with relational database properties such as Atomicity, consistency, integrity, durability, concurrency, query processing,

## When Not to Use a Relational Database

- Have large amounts of data: Relational Databases are not distributed databases and because of this they can only scale vertically by adding more storage in the machine itself. You are limited by how much you can scale and how much data you can store on one machine. You cannot add more machines like you can in NoSQL databases.
- Need to be able to store different data type formats: Relational databases are not designed to handle unstructured data.
- Need high throughput -- fast reads: While ACID transactions bring benefits, they also slow down the process of reading and writing data. If you need very fast reads and writes, using a relational database may not suit your needs.
- Need a flexible schema: Flexible schema can allow for columns to be added that do not have to be used by every row, saving disk space.
- Need high availability: System with very little downtime and that is always on and functioning. The fact that relational databases are not distributed (and even when they are, they have a coordinator/worker architecture), they have a single point of failure. When that database goes down, a fail-over to a backup system occurs and takes time.
- Need horizontal scalability: Horizontal scalability is the ability to add more machines or nodes to a system to increase performance and space for data.

These issues lead to  creation of NoSQL database (aka Not Only SQL, Non Relational) . NoSQL database has a simple design, simpler horizontal scaling and finer control of availability. Data structures used are different than those in Relational databases makes some operations faster. There are various types of NoSQL databases.

## Document Database

Data is stored in documents grouped into collections. Each document can be different.

- [MongoDB](/DBMS/DocumentDB/MongoDB/)
- [CouchDB]

## Key-Value Store Database

Data is stored in array of key value pairs.

- [Redis](/DBMS/KeyValueDB/Redis/)
- DynamoDB
- [voldemort]

## Columnar or wide-column Database

Instead of tables colum families are the container for rows
No need of knowing all columns upfront. Each row can have different no of columns. Enables analysis of large dataset

- [Apache Cassandra](/DBMS/ColumnarDB/Cassandra/) (Partition Row Store)
- [Apache HBase](/DBMS/ColumnarDB/HBase/)  (wide Column Store)

## Graph Database

For data that are connected to each other and best represented in graphs. Entities (nodes) with properties (information about entity) are connected via lines.

- [Neo4J](/DBMS/GraphDB/Neo4J/)

## Elastic Search

## Multi-paradigm Database

## Data Warehouse and Data Lake

- Snowflake

## When not to use a NoSQL

- When you have a small dataset: NoSQL databases were made for big datasets not small datasets and while it works it wasn’t created for that.
- When you need ACID Transactions: If you need a consistent database with ACID transactions, then most NoSQL databases will not be able to serve this need. NoSQL database are eventually consistent and do not provide ACID transactions. However, there are exceptions to it. Some non-relational databases like MongoDB can support ACID transactions.
- When you need the ability to do JOINS across tables: NoSQL does not allow the ability to do JOINS. This is not allowed as this will result in full table scans.
- If you want to be able to do aggregations and analytics
- If you have changing business requirements : Ad-hoc queries are possible but difficult as the data model was done to fix particular queries
- If your queries are not available and you need the flexibility : You need your queries in advance. If those are not available or you will need to be able to have flexibility on how you query your data you might need to stick with a relational database

## How to Pick the Right Database for your application ?

IF your business is not experiencing rapid growth or sudden changes. There are no requirements of more servers and data is structured and consistent, then there is no reason to use system design to support variety of data and high traffic.

While building a highly scalable system, choosing the right database is often the single most important decision. For an exponentially growing business, bad choice of database would lead to extended downtime, latency issues, even data loss impacting customers. When should you consider looking for a different database than the one you are already using, mostly when you have following issues.

1. When P95 Threshold (i.e 5% of transaction durations are greater than the threshold) latency is extremely high
2. Memory overflow is common
3. Even basic requests require disks I/O slowing things down

Before considering to switch make sure you cannot solve using the same database just but changing the configurations such as memory size, changing compaction strategy, garbage collection behavior and pushing it to the limit. Read the Manuals about the limits of the database. Because migrating a database is risky, costly and take a long time months to years.

- add cache
- add read replicas to offload some read load
- shard or partition the database in natural silos

Keep points to consider

- Choose a database that has been around for a long time and have been widely tested, such as used by banking and finance companies
- Learn about the database limits, and get reviews from online community
- Trade-offs: unlimited linear horizontal scalability generally comes without ACID transactional guarantees.
- Test with a representative data replicating real workload and benchmark ( with P99) and different use-cases such as up and down sharding.

When all components of system are fast -> queryin & searching for data usually becomes bottleneck. NoSQL prevent data from being bottleneck.

## ACID Compliance

- reduces anomalies
- protects integrity of the database , required for E-commerce and financial apps.


## SQL interview problems

 1- How to find duplicates in a table
2- How to delete duplicates from a table
3- Difference between union and union all
4- Difference between rank,row_number and dense_rank
5- Find records in a table which are not present in another table
6- Find second highest salary employees in each department
7- Find employees with salary more than their manager's salary
8- Difference between inner and left join
9- update a table and swap gender values.
10- Number of records in output with different kinds of join.

solutions: https://youtu.be/Iv9qBz-cyVA

## Reference

- [CMU Database Group Youtube Channel](https://www.youtube.com/@CMUDatabaseGroup) and its [Website](https://15445.courses.cs.cmu.edu/fall2021/)
  - [Intro to Database](https://www.youtube.com/watch?v=uikbtpVZS2s&list=PLSE8ODhjZXjaKScG3l0nuOiDTTqpfnWFf)
  - [Advance Database](https://www.youtube.com/watch?v=m72mt4VN9ik&list=PLSE8ODhjZXja7K1hjZ01UTVDnGQdx5v5U)
- [CMU DB Seminar](https://db.cs.cmu.edu/seminar2022/)
- [Accidental DBA](https://www.sqlskills.com/help/accidental-dba/)



https://www.sqliteonline.com
https://sqlitebrowser.org/dl/
