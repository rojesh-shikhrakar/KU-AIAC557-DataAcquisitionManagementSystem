# Data System Design

System design is the process of defining and integrating components, APIs, and data models to build large-scale systems that meet a specified set of functional and non-functional requirements. Modern systems are complex, yet maintainable, and are designed to perform reliably (handle faults, failures, and errors) and effectively (meet all requirements) at scale.

There are two approaches of software engineering system design

1. Top Down approach: aka stepwise design, decomposition,
  Splits the System (as a single entity with certain characteristics) into simpler sub-systems and components (modules) recursively until a lowest level of system is reached.
  scope the problem (Ask questions, identify constraints, functionality requirements) -> abstract design -> finding and addressing bottleneck
2. Bottom up approach:
  Design starts with lowest components and sub-systems forming higher-level components and sub-systems with increasing level of abstraction until a complete system is formed

Concepts applied

- Distributed Systems: An interconnect set of nodes that are linked by a network and share information between them.
- Parallel system
- Computer Network

Talk about the trade-offs: No Solution is perfect: Calculate the impact an system based on all the constraints and the end test cases.

## MicroServices

The micro-services architecture is design paradigm where an application is structured to collect several independent services. Each independent service, organized around a specific business capability is owned, developed, managed and deployed independently by a small separate team. Being loosely coupled with the overall system, it is easier to manage, test, maintain, and deploy at large scale.

### Caches

A cache is temporary storage that is relatively smaller in size with faster access time. Caches are used to reduce latency and reduce the load on your servers and databases. There are several levels at which caches are implemented. These are as follows:

1. Client Caching: Caches are located on the client-side like browser, file-system, servers acting as reverse-proxy.
2. CDN Caching: CDN (Content Delivery Network) is also used as a cache for serving static content (eg. HTML, CSS, Javascript, Image, Videos, etc.).
3. Web Server Caching: Web Servers also implement local caches and can retrieve, return information without contacting downstream servers.
4. Database Caching: Databases by default include some level of caching so that they do not have to run queries repeatedly. This can boost the performance of databases when they are under a lot of load.
5. Application Caching: In application caching, the cache is placed between application and data stores. These caches usually store database query results and/or objects that the application uses. Typical application caches include Memcached, Redis, DynamoDB, etc.

One of the challenges with caching is ensuring consistency of the data between the cache and the underlying data layer (i.e. server or database).

Topics:

- consistent hashing
- cap theorem
- Load balancing: scales horizontally
  - types of distribution : Random, round-robin, random weights (weights fro memory & CPU Cycle)
  - utilize full scalability and redundancy, add 3 LB

  ```mermaid
    flowchart LR
      A[User] -->B{LB1}
      B --> C[WebServer]
      B --> D[WebServer]
      C --> E{LB2}
      D --> E{LB2}
      E --> F[App/Cache Server]
      E --> G[App/Cache Server]
      F --> H{LB3}
      G --> H{LB3}
      H --> I[DB]
      H --> J[DB]
  ```

  - smart clients: takes a pool of service hosts and balances load. Detects hosts that are not responsive, recovered hosts, addition of new hosts.
  - load balancing functionality to DB (Cache server)  attractive solution, suitable even for small systems which can grow
- queues:
  efficiently manages requests in large-scale distributed systems. Async ommunication protocal.

- caching
  - locality of reference principle. used in almost every layer of computing.
    - application server cache: placing a cache directly on a request layer node. local storage of response.
    - cache on one request layer node. Memory (Very fast), nodes' local disk (Faster than network storage)
    - bottleneck: if LB distributes request randomly. same requests => different nodes. Can be overcomed by
      - distributed caches: cache divided across nodes using consistent hashing function to allow query in fast retrieval of data. Easy to increase cache space by adding more nodes but resolving a missing note becomes more complicated as we start creating copies of data on different nodes. Better to pull data from origin if node disappears.
      - global caches: Single cache spaces for all the nodes. adding a cache server/file store (faster than original store)
      - Content Distribution Network (CDN) Cache store for sites that serves large amount of static media. If the site isn't large enough to have it wn CDN for better and easy future transition serve static media using a separate subdomain (static.yourdomain.com) using a lightweight nginx server. LAter move to DNS from your server.
    - cache invalidation: cache data needs to be coherent with the database. IF data in DB modified => invalidate the cached data.  schemes
      - write-through cache: Data is written same time in both cache and DB. Complete data consistency (cache == DB). Fault Tolerance in case of failure (less data loss) high latency in writes => 2 write operations.
      - write around cache. No caching loading for writes. read request for newly writtne data => miss . higher latency.
      - write back cache:  low latency and high throughput for write intensive appn. data loss is increase.
    - Cache eviction policies: FIFO, LIFO(FILO), LRU, MRU, LFU, Random Replacement.

- redundancy & replication
  - duplication of critical data & services increasing reliability of system. For critical services & data => ensure that multiple copies/versions are running simultaneously on different servers/database.
  - secure against single node failures - provides backups if needed in crisis, server through secondary server as a failover.
  - Active data replicated to mirrored data
  - service redundancy : shared nothing architecture. 
  - every node -> independent (no central service managing state) -> helps scalability, new servers addition without special conditions -> more resilient to failures. No single point of failure.

- SQL vs No-SQL
- Indexes
  - improves speed of retrieval but increase storage overhead and slower writes (write data and update index).
  - can be created using one or more columns.
  - rapid random lookups and efficient access of ordered records
  - Data structure: column - pointer to whole row. Create different views of the same data. very good for filtering/sorting of large datasets. non ed to create additional copies.
  
- Proxies: 
  - useful under high load situations and if we have limited caching. Batches several requests in to one.

- sharding/Data Partitioning: splitting up DB/table across multiple machines => manageability, performance, availability & LB. after a certain scale point, it is cheaper and more feasible to scale horizontally by adding more machines instead of vertical scaling by adding higher capacity server.
  - horizontal partitioning: different rows into different tables. range based sharding eg storing locations by zip. different ranges in different tables.
  - vertical partitioning: 
    - features wise distribution of data in different servers. eg in instagram, DB server 1 - user info, db server 2 - followers, db-server 3 photos,... Straightforward to implement, low impact on app. If app has high growth, it would not be possible for a single server to handle all metadata queries for  10 billion photos by 140 million user.
   - directory based partitioning: a loosely coupled approach to work around above issues. Create lookup service --> current partitioning scheme and abstracts it away from the DB access code. Mapping (tuple key -> DB server) . Easy to add DB servers or change partitioning scheme.
  - Partitioning Criteria
    - Key or hash based partitioning: effectively fixes the total number of servers/partitions. If we add new server/partition change in hash function. Downtime because of redistribution which can be solved using consistent hashing.
    - List Partitioning: each partition is assigned a list of values
    - Round Robin partitioning: uniform data distribution. with 'n' partitions the 'i' tuple is assigned to partition (i mod n)
    - Composite partitioning: combination of above partitioning schemes. HAshing + List --> consistent hashing 
  - common problem of sharding
    - extra constraint on diff operations: operations across multiple tables or multiple rows in the same table. No longer running in single server
    - Joins and denormalization: joins on table on single server -> straight forward. Not feasible to perform joins on sharded tables., workaround is to denormalize the DB. so that the queries that previously required joins can be performed from a single table. perils of denormalization. Data inconsistency.
    - Referential integrity: foreign keys on sharded DB.
    - Re-balancing: reason to change sharding scheme: non-uniform distribution (data wise), non-uniform load balancing (request wise).

Web sockets: full duplex communication channel over single TCP connections. Provides persistent communication (client and server can send data at anytime). bidirectional communication in always open channel.

## Courses

- Distributed Systems: Principles and Paradigms
- Designing Data Intensive Applications
- Microservices.io
- https://github.com/donnemartin/system-design-primer
- https://www.freecodecamp.org/news/design-patterns-for-distributed-systems/ 
- System Design Interview Books
  - [Grokking Modern System Design Interview for Engineers & Managers](https://www.educative.io/courses/grokking-modern-system-design-interview-for-engineers-managers)
