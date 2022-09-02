# Basic Hadoop and Spark config files

- This simple setup is for Spark with Hadoop YARN

- Other environment variables set in `/etc/environment` 

```sh
## NOTE: /etc/environment dose not support `$` expantion. 

JAVA_HOME=/usr/lib/jvm/default-java/
HADOOP_HOME=/soft/APP/hadoop
SPARK_HOME=/soft/APP/spark
HADOOP_CONF_DIR=/soft/APP/hadoop-spark-conf/hadoop/etc/hadoop
SPARK_CONF_DIR=/soft/APP/hadoop-spark-conf/spark/conf

PATH=/soft/APP/hadoop/bin:/soft/APP/spark/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```
