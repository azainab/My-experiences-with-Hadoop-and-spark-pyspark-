# My-experiences-with-Hadoop-and-spark-pyspark-


To access a file from hdfs it expects the same file to be on both local system and the hdfs system.

Read a python file from spark:

PYTHONSTARTUP=tmp/input/dfa.py pyspark



>>>>>

Spark can be run independent of Hadoop, using the Mesos framework. Spark was explicitly designed to overcome the inefficiency of the MapReduce model in performing interactive and iterative computations.

Languages such as Java and C++ aren’t very useful for exploratory analysis, because they lack a REPL (read-evaluate-print loop) environment for working interactively with data


>>>>>>>>
In hadoop - spark location

ls etc/spark


>>>>>>>>>>>>>

There are two types of operations you can perform with RDDs:

Image Actions: Operations in this category just return a value from an RDD, such as the count() operation, for example, which returns the count of some data element.

Image Transformations: These operations define a new RDD based on the RDD you’re operating on.


