# Introduction

### Topics

First part

- Spark 2.0
- Sparks Machine Learning library
- Spark SQL
- Spark DataFrames
- Spark Streaming

Then, in the second half of the course

- Introduction to ML
- linear and logistic regression
- Decision trees, random forests and gradient boosting trees
- k-means clustering, recommender system, NLP
- Spark Streaming (Local and e.g. Twitter)

### What is Spark

"Big Data" = Anything that doesn't fit your local RAM (e.g. >64GB). Then...

- use SQL to move storage onto hard drive
- use distributed system (one benefit is fault tolerance if one node crashes)

One way to distribute very large files across systems is Hadoop. It...

- stores data using Hadoop Distributed File System (HDFS). This replicates data blocks (128 MB by default) three times for fault tolerance

- accesses data using MapReduce

Spark...

- is an open source project on Apache
- was released 2013
- was created at UCBerkley
- is an alternative to MapReduce

Spark vs. MapReduce

- supports not only HDFS, but also AWS S3, Cassandra, etc.
- is up to 100x faster by keeping data in memory (if possible, else spills over to disk). In contrast, MapReduce writes most data to disk after each map and reduce operation. - Hmm... this seems wrong or overly simplified. google says:
  - Data between two operations is passed via memory with Spark but via 3x replicated HDFS with Hadoop
  - Spark introduced in-memory caching
  - Spark keeps a JVM executor running on each node while Hadoop launches one for every task
  - Spark uses lazy evaluation to form a DAG which can be optimized prior to execution
- is a core idea of Resilient Distributed Data (RDD), which are immutable, lazily evaluated and cacheable
  - Distributed Collection of Data
  - Fault-tolerant
  - parallel operation
  - ability to use many data sources

Spark has two types of operations

- Transformations = recipe to follow (e.g. take average)
- Action = execute recipe

Spark syntax exists as

- RDD syntax
- DataFrame synax <-- primary syntax since Spark 2.0

Video is from 2016 with 2.1.0 spark, now in 2020 Spark 3.0 was released with differences:

- even faster
- pandas UDF API redesign with python typie hints
- more features (adaptive query execution, dynamic partition pruning, ...)

# Setup

### Options

Setup a realistic deployment for Spark, Python and Jupyter Notebook using one of...

- Virtual Box + Ubuntu
- AWS EC2 (free micro instance under amazon 1 year trial)
- Databricks Notebook System (databricks was founded by creators of Spark)
- AWS Elastic MapReduce (EMR) Notebook (not free ~1€/h, but very quick)

### Own idea: simply use docker

```bash
# from https://hub.docker.com/r/jupyter/pyspark-notebook
docker pull $IMAGE_NAME
IMAGE_NAME=jupyter/pyspark-notebook:spark-3.2.0
SRC='/mnt/sda1/projects/git/courses/udemy_pyspark/'
DST='/home/jovyan/udemy_pyspark'
docker run -p 8888:8888 -v $SRC:$DST $IMAGE_NAME
```
