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


>>>>>
#####  hadoop cluster location:

hdfs dfs -df -h /location/of/your/file

output (example): hdfs://hdp01:8020 

>>>>
path of the hdfs directory can be found out making a directory and delting it. It will point to the path of the hdfs


>>>>>
#####  In order for spark to see the files we need to add:

export HADOOP_CONF_DIR=$SPARK_HOME/spark-env.sh

>>>>>
#####  Error:

import xlsxwriter
Traceback (most recent call last):
  File "<stdin>", line 1, in <module>
ImportError: No module named xlsxwriter

Solution:

python -m pip install --user xlsxwriter


##### Transfer files from desktop/local computer to server:

1. sftp user@server
2. Password:
3. put -r "path\to\file"

#### merge csv files
cat *.csv >merged.csv

#### submitting a python file from spark

spark-submit --master spark://Nodename:port location/of/python file/on hdfs/ 1000


### get file names from a hdfs path


cmd = 'hdfs dfs -ls hdfs/path/'.split()
files = subprocess.check_output(cmd).strip().split('\n')
for path in files:
  print(path) 

### - core-site.xml path
go to the hadoop editor and type
ls /etc/hadoop/conf


### hadoop-env.sh path
ls /etc/hadoop/conf

### install a particular version of pyspark
pip install pyspark==2.1.3
