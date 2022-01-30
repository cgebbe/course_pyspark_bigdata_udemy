# Spark Streaming Lecture

## Introduction

### SparkStreaming

- ...enables processing of streams from different sources such as ...

  - TCP Sockets
  - Kafka
  - Kinesis
  - Flume
- ... can push out processed data to filesystems, databases and dashboards.
- ... is explained more at https://spark.apache.org/docs/latest/streaming-programming-guide.html.

![Spark Streaming](spark_streaming.assets/streaming-arch.png)

### Structured Streaming

- ... is SparkStreaming run on top of the Spark SQL engine
- ... allows to access and modify data using the dataframe API. This is much easier!
- ... was not stable as of pyspark 2.1, but should be probably preferred by now ?
- ... is explained more at https://spark.apache.org/docs/latest/structured-streaming-programming-guide.html

![Stream as a Table](spark_streaming.assets/structured-streaming-stream-as-a-table.png)

## Documentation example

- is taken directly from https://spark.apache.org/docs/latest/streaming-programming-guide.html#a-quick-example
- streams from a local TCP socket
- counts words per line

## Twitter example

- is effectively an extension of the documentation example.
- also parses a stream from a local TCP socket.
- uses the [tweepy library](https://pypi.org/project/tweepy/) to access twitter, which
  - receives tweets using `tweepy.Stream()`
  - filters them by a word
  - creates a port for forwarding using `client_socket=socket.socket().bind((host,port))`
  - sends / forwards tweets using `client_socket.send(msg)`
- parses the TCP socket stream using Spark by 
  - splitting into words
  - filtering by words starting with a hashtag `#`
  - counts the filters words
  - plots the count per filtered word
