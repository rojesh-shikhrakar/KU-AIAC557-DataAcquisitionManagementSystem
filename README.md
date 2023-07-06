# KU-AIAC557 Data Acquisition Management System

Kathmandu University Department of Computer Science and Engineering

Subject: Data Acquisition Management System

Course Code: AIAC 557

Level: MTech in AI, Year 1, Semester II

Credit Hours: 3

Type: Elective [Theory + Practical]

## Course Description

### Course Objective

After completiton of the course, students should be able to

- acquire data from various sources and ingest them to a data store( data lake, eDW ,data mart, delta lakes)
- work on cloud ecosystem and be able to complete a certification in on cloud provider (AWS, Google, Azure)
- Create ETL and ELT pipelines through various data processing (in SQL, DBT, DataFoam (part of bigquery), Spark) for different applications including data visualization and reporting (understand BI concepts)
- demonstrate understanding of data management issues, data quality, data governance
- Perform Basics of ML Operations: deploying model in production (batch/). Monitoring the performance the model (DataDrift/ ModelDrift)
  - Orchestration (airflow) and creation of pipeline and be able to handover the pipeline to the operation team taking care of data management aspect such as incident management and such
  - Data governance: creating data catalogue, lineage of data, identifying personal information from data, standard data models, using Open APIs.
- pull requirement from business stakeholder to build high level design by enterprise architect, solution architect design mid level, data engineer build solution architect

### Prerequisites

- Python Programming : Numpy, Pandas, Matplotlib, REST API, Web Scraping,
- Linux
- Git and Github
- Basic Data Science

### Course Evaluation

In-Semester evaluation - 60 marks
End-Semester Evaluation - 40 marks

## Chapters

### Chapter 1: [Introduction Data Science, Engineering and Management](C1-Intro/README.md) [4 Hr]

- Introduction to Data Science, Data Engineering and Data Management
- DIKW Pyramid and its issues
- Big Data and Big Data Ecosystem
- Data Lifecycle
- Data Management Principles and Challenges
- Data Management Strategy and Frameworks
- Data Engineering in Data Science (or ML) Lifecycle

[Pre-requisites review](/C0-Prerequisites/)

- Important Python Libraries: Numpy, Pandas, Matplotlib, Seaborn to perform EDA
- REST API, Request and Web Scraping
- Text processing, extraction and classification
- Data Science
- Git and github
- Linux and Shell Scripting
- Docker
- Distributed Systems

### Chapter 2: [Data Handling](C2-Data-Handling/README.md) [12 Hr]

- [Data Acquisition and Ingestion](/C2-Data-Handling/Data-Acquisition/README.md)
  - [Data Formats](/C2-Data-Handling/Data-Acquisition/Data-Formats/README.md)
  - [Web Scraping](/C2-Data-Handling/Data-Acquisition/Web-Scraping/README.md): Scrapy and BeautifulSoap
- Data Quality
- [Data Wrangling and Cleaning](/C2-Data-Handling/Data-Wrangling/README.md)
- Data Handling Ethics
- Data Governance
- [Data Processing](/C2-Data-Handling/Data-Processing/README.md)
  - Hadoop and MapReduce
  - [Apache Spark](/C2-Data-Handling/Data-Processing/ApacheSpark/README.md): RDDs, DAtaFrames, SQL, MLLib, Streaming, GraphX
- [Data Streams](/C2-Data-Handling/Data-Streams/README.md)
  - [Apache Kafka](/C2-Data-Handling/Data-Streams/ApacheKafka/README.md): Topics, Parititions, Producer,Consumer, Kafka Connects
  - Apache Flume
- YARN and Zookeeper
- Cloud Services provided by AWS, GCP, Azure
  - AWS EC2, AMI, EVS, S3,RDS, Athena, Redshift, Lambda, CloudWatch, Glue for ETL jobs and EMR
  - GCP Cloudstorage, DataFusion, BigQuery, Data-proc and Data Flow
  - Azure data factory, SQL DB, Blob Storage, HDInsight, Databricks,

### Chapter 3: [Data Modelling, Design and Storage](C3-Data-Modelling-Design-Storage/README.md) [15 Hr]

- [Data Storage](/C3-Data-Modelling-Design-Storage/README.md)
- Distributed Storage: GFS & HDFS
- Database Schema and Notations
- [Relational Database Management System (RDMS)](/C3-Data-Modelling-Design-Storage/RelationalDB/README.md)
  - Relationship and Entity Relationship Diagram
- Object-oriented DB and UML Notations
- [Document Database](/C3-Data-Modelling-Design-Storage/DocumentDB/readme.md): [MongoDB](/C3-Data-Modelling-Design-Storage/DocumentDB/MongoDB/readme.md)
- [Columnar Database](/C3-Data-Modelling-Design-Storage/ColumnarDB/readme.md): [Cassandra](/C3-Data-Modelling-Design-Storage/ColumnarDB/Cassandra/readme.md), HBase
- [Key-Value Pair DB](/C3-Data-Modelling-Design-Storage/KeyValueDB/readme.md): [Redis](/C3-Data-Modelling-Design-Storage/KeyValueDB/Redis/readme.md)
- [Graph Database](/C3-Data-Modelling-Design-Storage/GraphDB/readme.md): [Neo4J](/C3-Data-Modelling-Design-Storage/GraphDB/Neo4J/readme.md)
- Multi-support, multi-paradigm database:
  - [Search DB](/C3-Data-Modelling-Design-Storage/SearchDB/README.md): [ElasticSearch](/C3-Data-Modelling-Design-Storage/SearchDB/Elastic-Search/README.md)
  - Time-series DB
- Cloud Data Warehouse
- Data Lake and Data Mesh
  - SnowFlake: Star schema and Snowflake Schema
- ETL and ELT pipeline

### Chapter 4: [Data Architecture and Orchestration](C4-Data-Architecture-Orchestration/README.md)

- Importance of Data Architecture
- Lambda and Kappa Architectures
- Data Architecture concepts and practices
- Data Engineering Architectures and Pipelines
- [Orchestration](/C4-Data-Architecture-Orchestration/Data-Orchestration/README.md)
  - [Apache Airflow](/C4-Data-Architecture-Orchestration/Data-Orchestration/ApacheAirflow/README.md)
- Streaming Pipelines
- Model Deployment
- Model Monitoring

### Chapter 5:[Data Management Concepts](C5-Data-Management/README.md)

- Data Governance
- Data Security
- Data Integration and Interoperability
- Context Management
- Meta-data Management
- Data Management Maturity
- Organizational Change Management

## Optional: [System Design](C6-System-Design/README.md)

- System Design System Components
- System Design System Components
- Scaling Data Systems
- Distributed System Design
- System Design Patterns for distributed systems
- Case Studies

### Reference

- [DAMA-DMBOK2 Data Management Book of Knowledge](https://www.dama.org/cpages/body-of-knowledge)
- Fundamentals of Data Engineering by Joe Reis, Matt Housley
- Data Pipelines Pocket Reference by James Densmore
- Streaming Systems The What, Where, When, and How of Large-Scale Data Processing. by Akidau, Tyler Chernyak, Slava Lax, Reuven
- Designing Data-Intensive Applications The Big Ideas Behind Reliable, Scalable, and Maintainable Systems by Martin Kleppmann
