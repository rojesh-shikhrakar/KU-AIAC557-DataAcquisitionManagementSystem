# KU-AIAC557 Data Acquisition Management System

Kathmandu University Department of Computer Science and Engineering

Subject: Data Acquisition Management Systemto 

Course Code: AIAC 557

Level: MTech in AI 1 year II semester

Credit Hours: 3

Type: Optional [Theory + Practical]

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

- Python Programming
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

Pre-requisites review
- Important Python Libraries: Numpy, Pandas, Matplotlib, Seaborn to perform EDA
- Text processing, extraction and classification
- Data Science
- Git and github
- Linux and Shell Scripting
- Docker
- Distributed Systems


### Chapter 2: [Data Handling](C2-Data-Handling/README.md) [12 Hr]

- Data Discovery and acquisition
  - Scraping: Scrapy and BeautifulSoap
- Data Ingestion
- Data Quality
- Data Wrangling and Cleaning
- Data Handling Ethics
- Data Governance
- Data Storage
  - GFS & HDFS
  - HBase
- Data Processing
  - Hadoop and MapReduce
  - Apache Spark: RDDs, DAtaFrames, SQL, MLLib, Streaming, GraphX
- Data Streams
  - Apache Kafka: Topics, Parititions, Producer,Consumer, Kafka Connects
  - Apache Flume
- YARN and Zookeeper
- Cloud Services provided by AWS, GCP, Azure
  - AWS EC2, AMI, EVS, S3,RDS, Athena, Redshift, Lambda, CloudWatch, Glue for ETL jobs and EMR
  - GCP Cloudstorage, DataFusion, BigQuery, Data-proc and Data Flow
  - Azure data factory, SQL DB, Blob Storage, HDInsight, Databricks,


### Chapter 3: [Data Modeling and Design](C3-Data-Modeling-Design/README.md) [15 Hr]

- Database Schema and Notations
- Relational Database Management System (RDMS)
  - Relationship
- Object-oriended DB and UML Notations
- Document Database: MongoDB
- Columnar Database
- Key-Value Pair DB
- Graph Database
- Multi-support, multi-paradigm database: Search DB, time-series DB
- Cloud Data Warehouse
- Data Lake and Data Mesh
  - SnowFlake: ETL and ELT pipeline, Star schema and Snowflake Schema
  

### Chapter 4: [Data Architecture and Orchestration](C4-Data-Architecture-Orchestration/README.md)

- Importance of Data Architecture
- Data Architecture concepts and practices
- Data Engineering Architectures and Pipelines
- Orchestration
  - Apache Airflow
- Model Deployment
- Model Monitoring


### Chapter 5:[Data Governance](C5-Data-Governance/README.md)

- Data Security
- Data Integration and Interoperability
- Context Management
- Meta-data Management
- Data Management Maturity
- Organizational Change Management


### Reference

- DAMA-DMBOK2
- Fundamentals of Data Engineering by Joe Reis, Matt Housley
- Data Pipelines Pocket Reference by James Densmore
- Streaming Systems The What, Where, When, and How of Large-Scale Data Processing. by Akidau, Tyler Chernyak, Slava Lax, Reuven
- Designing Data-Intensive Applications The Big Ideas Behind Reliable, Scalable, and Maintainable Systems by Martin Kleppmann
