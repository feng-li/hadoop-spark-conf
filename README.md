# Basic Hadoop and Spark config files

This simple configuration is for a MapReduce framework on a Linux server including

- Apache Hadoop
- Apache Spark standalone

_If you want to quickly deploy a Spark cluster on a Slurm server as a regular user, look at [https://github.com/feng-li/spark-on-slurm](https://github.com/feng-li/spark-on-slurm)._

## Prerequisites

- Make sure necessary environment variables are set. If you have the access to `/etc/environment`, you could write there and it will take effect gloablly. Otherwise, you have to write them to a file (usually in `~/.bashrc` or `~/.zshrc`) and source it before you start the servers.


```sh
## NOTE: /etc/environment dose not support `$` expantion.

JAVA_HOME=/usr/lib/jvm/default-java/
HADOOP_HOME=/soft/APP/hadoop
SPARK_HOME=/soft/APP/spark
HADOOP_CONF_DIR=/soft/APP/hadoop-spark-conf/hadoop/etc/hadoop
SPARK_CONF_DIR=/soft/APP/hadoop-spark-conf/spark/conf

PATH=/soft/APP/hadoop/bin:/soft/APP/spark/bin:/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
```

## Tuning Spark

- **Use the Kryo library to serialize objects**. Set a faster serializer for Java serialization in the `spark-defaults.conf` could often speed up as much as 10x.

      spark.serializer                 org.apache.spark.serializer.KryoSerializer

- **Eliminate BLAS threads**. Spark running on YARN or standalone mode should avoid additional threads parallelism. Set the environment variables at the `spark-env.sh` file or set them at run time.

      MKL_NUM_THREADS=1
      OPENBLAS_NUM_THREADS=1

- **Oversubscribe resources**. If we have a small cluster but many people are using it. Note that not every time the cluster is fully loaded. We could use an _oversubscribing trick_ to improve the cluster's effciency, i.e. to allow for more jobs running simultaneously. It is often safe to set double amount of physical cores and/or total memory. Assume each worker node has **32 physical core** and **64G RAM**, we could double them in the `spark-env.sh` file.

      SPARK_WORKER_CORES=64
      SPARK_WORKER_MEMORY=128g
