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


#### pip upgrade error
Command "python setup.py egg_info" failed with error code 1 in /tmp/pip-build-hid_iwzh/pandas/

solution:
pip3 install --upgrade pip setuptools wheel


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


### running spark
git clone git@github.com:sryza/spark-timeseries.git
cd spark-timeseries/python
spark-shell --jars target/sparkts-$VERSION-SNAPSHOT-jar-with-dependencies.jar

output:
>scala

### reading a file in spark timesereis
scala>

import java.sql.Timestamp

import java.time.{LocalDateTime, ZoneId, ZonedDateTime}

import com.cloudera.sparkts._

import com.cloudera.spartks.stats.TimeSeriesStatisticalTests

import org.apache.spark.{SparkContext, SparkConf}

import org.apache.spark.sql.{DataFrame, Row, SQLContext}

import org.apache.spark.sql.types._

def loadObservations(sqlContext: SQLContext, path:String): DataFrame = {

  val rowRdd = sqlContext.sparkContext.textFile(path).map { line=>
  
  val tokens = line.split(',');
  
  val dt = ZonedDateTime.of(tokens(10).toInt,tokens(9).toInt, tokens(8).toInt, 0, 0, 0, 0, ZoneId.systemDefault());
  
  val SUMERTIME = tokens(2).toDouble;
  
  val VAL_AI = tokens(12).toDouble;
  
  Row(Timestamp.from(dt.toInstant), ticket, open, high, low, close, volume, adjclose);
  
  }
  
  val fields = Seq(StructField("timestamp", TimestampType, true),StructField("SUMMERTIME", DoubleType, true), StructField("VAL_AI", DoubleType, True));
  
  val schema = StructType(fields);
  
  sqlContext.createDataFrame(rowRdd, schema);
  
  }

#### get configuration of spark using pyspark
sc._conf.getAll()

