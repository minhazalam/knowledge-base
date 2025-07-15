### ==What is Apache Spark?==

![Pasted image 20231124134358.png](https://publish-01.obsidian.md/access/2948681fa29a77abab215fc5482133de/Images/Spark%20Course/Pasted%20image%2020231124134358.png)


Spark is designed to support a wide range of data analytics tasks, ranging from simple data loading and SQL queries to machine learning and streaming computation, over the same computing engine and with a consistent set of APIs.

- Spark provides consistent, composable APIs that you can use to build an application out of smaller pieces or out of existing libraries.
- Spark’s APIs are also designed to enable high performance by optimizing across the different libraries and functions composed together in a user program

For example, if you load data using a SQL query and then evaluate a machine learning model over it using Spark’s ML library, the engine can combine these steps into one scan over the data. The combination of general APIs and high- performance execution, no matter how you combine them, makes Spark a powerful platform for interactive and production applications.

#### Computing engine

Spark handles loading data from storage systems and performing computation on it, not permanent storage as the end itself. You can use Spark with a wide variety of persistent storage systems, including cloud storage systems such as Azure Storage and Amazon S3, distributed file systems such as Apache Hadoop, key-value stores such as Apache Cassandra, and message buses such as Apache Kafka.

Data is expensive to move so Spark focuses on performing computations over the data, no matter where it resides

Hadoop included both a storage system (the Hadoop file system, designed for low-cost storage over clusters of commodity servers) and a computing system (MapReduce), which were closely integrated together. However, this choice makes it difficult to run one of the systems without the other.

#### Libraries

Spark’s final component is its libraries, which build on its design as a unified engine to provide a unified API for common data analysis tasks. Spark supports both standard libraries that ship with the engine as well as a wide array of external libraries published as third-party packages by the open source communities.

### ==**Frequently Asked Questions**==
### 1. **What is PySpark?**

PySpark is the Python API for Apache Spark, an open-source, distributed computing system known for its speed and ease of use in handling large-scale data processing.

### 2. **Explain the differences between Hadoop and Spark.**

- **Hadoop:** Uses disk-based storage for data processing, which can be slower.
- **Spark:** Uses in-memory processing, making it much faster for many tasks.
- **Hadoop:** Best for batch processing.
- **Spark:** Suitable for both batch and real-time processing.

### 3. **What are RDDs in Spark?**

RDD stands for Resilient Distributed Dataset, which is Spark's fundamental data structure. It is an immutable distributed collection of objects that can be processed in parallel.

**Example:**
```python
from pyspark import SparkContext

sc = SparkContext("local", "example")
data = [1, 2, 3, 4, 5]
rdd = sc.parallelize(data)
```

### 4. **How does Spark handle distributed data processing?**

Spark uses a master-slave architecture where the master node (driver) coordinates the tasks and the slave nodes (executors) perform the computations. Data is distributed across the nodes, and tasks are run in parallel on these partitions.

### 5. **What are the different cluster managers available in Spark?**

- **Standalone:** A simple cluster manager included with Spark.
- **YARN:** Resource manager in Hadoop.
- **Mesos:** A general-purpose cluster manager.
- **Kubernetes:** An open-source system for automating deployment, scaling, and operations of application containers.

### 6. **What is a DataFrame in PySpark?**

A DataFrame is a distributed collection of data organized into named columns, similar to a table in a relational database.

**Example:**
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("example").getOrCreate()
data = [("John", 30), ("Jane", 25)]
columns = ["Name", "Age"]
df = spark.createDataFrame(data, schema=columns)
df.show()
```

### 7. **Explain the use of the `map` and `flatMap` transformations.**

- **map:** Transforms each element of the RDD individually.
- **flatMap:** Similar to `map`, but each input item can be mapped to zero or more output items (flattening the result).

**Example:**
```python
rdd = sc.parallelize([1, 2, 3])
mapped_rdd = rdd.map(lambda x: (x, x * 2))
flat_mapped_rdd = rdd.flatMap(lambda x: (x, x * 2))
```

### 8. **What is a Spark action? Give an example.**

An action triggers the execution of transformations and returns a value or writes data to external storage.

**Example:**
```python
rdd = sc.parallelize([1, 2, 3])
sum_result = rdd.sum()
```

### 9. **How can you read and write data in PySpark?**

You can use the `read` and `write` methods provided by the `DataFrameReader` and `DataFrameWriter` classes.

**Example:**
```python
# Reading data
df = spark.read.csv("path/to/file.csv", header=True, inferSchema=True)

# Writing data
df.write.csv("path/to/output.csv")
```

### 10. **Explain the concept of lazy evaluation in Spark.**

Lazy evaluation means that Spark does not immediately execute the transformations when they are called. Instead, it builds a logical execution plan. The execution starts only when an action is called.

### 11. **What is the difference between `persist()` and `cache()`?**

- **cache():** Persists the RDD/DataFrame in memory.
- **persist():** Provides control over the storage level, allowing you to specify whether to store data in memory, disk, or both.

### 12. **How do you handle missing data in PySpark DataFrames?**

You can use methods like `dropna()` and `fillna()`.

**Example:**
```python
df = df.na.drop()  # Drops rows with any null values
df = df.na.fill({"column_name": 0})  # Fills null values in a column with 0
```

### 13. **What is a SparkContext?**

SparkContext is the entry point to any Spark functionality. It's used to create RDDs, accumulators, and broadcast variables.

### 14. **What are accumulators in Spark?**

Accumulators are variables that are only “added” to through an associative and commutative operation and can be used to implement counters or sums.

**Example:**
```python
acc = sc.accumulator(0)
rdd = sc.parallelize([1, 2, 3, 4])
rdd.foreach(lambda x: acc.add(x))
print(acc.value)
```

### 15. **What is the difference between `transformations` and `actions` in Spark?**

- **Transformations:** Lazy operations that define a new RDD from an existing one, e.g., `map`, `filter`.
- **Actions:** Trigger the execution of transformations and return a result, e.g., `collect`, `count`.

### 16. **How do you join two DataFrames in PySpark?**

Using the `join` method.

**Example:**
```python
df1 = spark.createDataFrame([(1, "John"), (2, "Jane")], ["id", "name"])
df2 = spark.createDataFrame([(1, "USA"), (2, "UK")], ["id", "country"])
joined_df = df1.join(df2, on="id")
joined_df.show()
```

### 17. **What are broadcast variables in Spark?**

Broadcast variables are read-only variables that are cached on each machine rather than shipped with tasks, useful for data that is shared across multiple stages.

**Example:**
```python
broadcast_var = sc.broadcast([1, 2, 3])
rdd = sc.parallelize([4, 5, 6])
result = rdd.map(lambda x: x + broadcast_var.value[0])
result.collect()
```

### 18. **What is the use of the `groupByKey` and `reduceByKey` transformations?**

- **groupByKey:** Groups data with the same key.
- **reduceByKey:** Aggregates data with the same key using a specified associative and commutative function.

**Example:**
```python
rdd = sc.parallelize([("a", 1), ("b", 1), ("a", 1)])
grouped = rdd.groupByKey().mapValues(list).collect()
reduced = rdd.reduceByKey(lambda a, b: a + b).collect()
```

### 19. **How do you use window functions in PySpark?**

Window functions operate over a window specification and allow you to perform operations like ranking and cumulative sums.

**Example:**
```python
from pyspark.sql.window import Window
from pyspark.sql.functions import rank

window_spec = Window.partitionBy("department").orderBy("salary")
df = df.withColumn("rank", rank().over(window_spec))
```

### 20. **How can you debug a PySpark application?**

- Use Spark's web UI to monitor and debug jobs.
- Enable logging for detailed output.
- Use `print` statements for local debugging.
- Use Spark’s `explain` method to understand the execution plan.

---
### ==**Conceptual Questions**==

### 1. **What is the architecture of Apache Spark?**

**A cluster,** or group, of computers, pools the resources of many machines together, giving us the ability to use all the cumulative resources as if they were a single computer.

Now, a group of machines alone is not powerful, you need a framework to coordinate work across them. Spark does just that, managing and coordinating the execution of tasks on data across a cluster of computers.  

![Pasted image 20231127200109.png](https://publish-01.obsidian.md/access/2948681fa29a77abab215fc5482133de/Images/Spark%20Course/Pasted%20image%2020231127200109.png)

Apache Spark follows a master-slave architecture where:
- **Driver Program:** The main program that creates the SparkContext and coordinates the execution.
- **Cluster Manager:** Manages the resources and schedules the jobs (e.g., Standalone, YARN, Mesos, Kubernetes).
- **Worker Nodes:** Execute the tasks assigned by the driver. Each worker has its own executor.
- **Executors:** Run individual tasks and store data in memory or disk storage as needed.
- **Tasks:** Basic units of work sent to an executor by the driver.

### 2. **Explain the role of the DAG (Directed Acyclic Graph) in Spark.**

**Answer:**
A DAG in Spark represents a sequence of computations performed on data. When an action is called, Spark constructs a DAG of stages and tasks:
- **Stages:** Represent a set of tasks that can be executed in parallel.
- **Tasks:** Represent the unit of work that gets executed on a partition of data.
The DAG helps Spark optimize and execute the workflow efficiently, minimizing data shuffling and ensuring fault tolerance.

### 3. **How does Spark achieve fault tolerance?**

**Answer:**
Spark achieves fault tolerance through:
- **Lineage:** Each RDD maintains information about how it was derived from other datasets (its lineage). If a partition of an RDD is lost, Spark can recompute it from the original data.
- **Checkpointing:** For long lineage chains, Spark can persist an RDD to a reliable storage like HDFS, breaking the lineage chain and improving fault tolerance.

### 4. **What are the advantages of using DataFrames over RDDs in Spark?**

**Answer:**
- **Optimization:** DataFrames allow Spark to perform optimizations like predicate pushdown, vectorized execution, and bytecode generation, which improve performance.
- **Ease of Use:** DataFrames have a more expressive API and are similar to data manipulation in SQL or pandas.
- **Integration:** DataFrames integrate seamlessly with Spark SQL, enabling the use of SQL queries and optimizations.

### 5. **What are Spark SQL's Catalyst Optimizer and Tungsten Execution Engine?**

**Answer:**
- **Catalyst Optimizer:** A query optimization framework in Spark SQL that automatically optimizes logical plans to generate efficient physical plans. It includes rule-based and cost-based optimizations.
- **Tungsten Execution Engine:** Enhances Spark's execution by improving memory management, code generation, and CPU efficiency. It includes techniques like whole-stage code generation and cache-aware computation.

### 6. **What is the difference between narrow and wide transformations in Spark?**

**Answer:**
- **Narrow Transformations:** Operations where each partition of the parent RDD is used by at most one partition of the child RDD. Examples include `map`, `filter`, and `mapPartitions`.
- **Wide Transformations:** Operations where multiple child partitions may depend on a single parent partition, often involving shuffling of data across the network. Examples include `reduceByKey`, `groupByKey`, and `join`.

### 7. **How does Spark handle data shuffling, and why is it important to minimize it?**

**Answer:**
Data shuffling is the process of redistributing data across the cluster, usually during wide transformations. Spark handles shuffling by writing intermediate data to disk and transferring it over the network to the required nodes. Minimizing shuffling is crucial because it involves expensive operations like disk I/O and network communication, which can significantly impact performance.

### 8. **What are broadcast variables and accumulators in Spark?**

**Answer:**
- **Broadcast Variables:** Used to efficiently distribute large read-only data to all worker nodes. They reduce the overhead of sending large data with each task.
- **Accumulators:** Variables used to aggregate information across tasks, typically for counters and sums. They are write-only from the worker’s perspective and can only be read on the driver side.

### 9. **Explain the concept of Spark’s in-memory computation model.**

**Answer:**
Spark’s in-memory computation model allows it to cache intermediate data in memory, reducing the need for repeated disk I/O operations. This significantly speeds up iterative algorithms and interactive data analysis tasks by keeping frequently accessed data in memory, thereby avoiding the overhead of disk read/write operations.

### 10. **What strategies would you use to optimize a PySpark job?**

**Answer:**
- **Data Partitioning:** Ensure data is partitioned optimally to balance the workload across the cluster and reduce shuffling.
- **Caching:** Cache intermediate RDDs or DataFrames that are reused multiple times in memory.
- **Avoid Wide Transformations:** Minimize the use of wide transformations that cause shuffling.
- **Broadcast Variables:** Use broadcast variables to efficiently distribute large read-only data.
- **Efficient Data Formats:** Use efficient data formats like Parquet or ORC with compression.
- **Tuning Spark Configurations:** Adjust Spark configurations like executor memory, cores, and parallelism to suit the workload.
- **Predicate Pushdown:** Leverage predicate pushdown and column pruning in DataFrames to reduce the amount of data read.

---
### **==PySpark Coding Questions==**

### 1. **Read a CSV file and show the first few rows**

**Question:** Write a PySpark script to read a CSV file named `data.csv` and display the first 5 rows.

**Answer:**
```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("example").getOrCreate()
df = spark.read.csv("data.csv", header=True, inferSchema=True)
df.show(5)
```

### 2. **Filter DataFrame based on a condition**

**Question:** Filter the DataFrame to show only rows where the column `age` is greater than 30.

**Answer:**
```python
filtered_df = df.filter(df.age > 30)
filtered_df.show()
```

### 3. **Group by and aggregate**

**Question:** Group the DataFrame by the column `department` and calculate the average salary.

**Answer:**
```python
avg_salary_df = df.groupBy("department").agg({"salary": "avg"})
avg_salary_df.show()
```

### 4. **Join two DataFrames**

**Question:** Join two DataFrames `df1` and `df2` on the column `id`.

**Answer:**
```python
joined_df = df1.join(df2, on="id")
joined_df.show()
```

### 5. **Add a new column**

**Question:** Add a new column `bonus` to the DataFrame where the value is 10% of the `salary` column.

**Answer:**
```python
from pyspark.sql.functions import col

df_with_bonus = df.withColumn("bonus", col("salary") * 0.1)
df_with_bonus.show()
```

### 6. **Drop duplicates**

**Question:** Remove duplicate rows based on the `id` column.

**Answer:**
```python
df_no_duplicates = df.dropDuplicates(["id"])
df_no_duplicates.show()
```

### 7. **Handle missing values**

**Question:** Fill missing values in the `salary` column with the average salary.

**Answer:**
```python
from pyspark.sql.functions import mean

mean_salary = df.select(mean(df.salary)).collect()[0][0]
df_filled = df.na.fill({"salary": mean_salary})
df_filled.show()
```

### 8. **Write DataFrame to Parquet**

**Question:** Write the DataFrame to a Parquet file named `output.parquet`.

**Answer:**
```python
df.write.parquet("output.parquet")
```

### 9. **Perform window function**

**Question:** Use a window function to add a rank column to the DataFrame partitioned by `department` and ordered by `salary`.

**Answer:**
```python
from pyspark.sql.window import Window
from pyspark.sql.functions import rank

window_spec = Window.partitionBy("department").orderBy("salary")
df_with_rank = df.withColumn("rank", rank().over(window_spec))
df_with_rank.show()
```

### 10. **Calculate word count**

**Question:** Write a PySpark script to calculate the word count from a given text file `text.txt`.

**Answer:**
```python
from pyspark import SparkContext

sc = SparkContext("local", "word_count")
text_file = sc.textFile("text.txt")

word_counts = text_file.flatMap(lambda line: line.split(" ")) \
                       .map(lambda word: (word, 1)) \
                       .reduceByKey(lambda a, b: a + b)

word_counts.collect()
```

### 11. **Filter and map RDD**

**Question:** Create an RDD from a list of numbers, filter out even numbers, and then square the remaining numbers.

**Answer:**
```python
numbers = sc.parallelize([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])
odd_squared = numbers.filter(lambda x: x % 2 != 0).map(lambda x: x * x)
odd_squared.collect()
```

### 12. **Union of two RDDs**

**Question:** Create two RDDs and perform a union operation on them.

**Answer:**
```python
rdd1 = sc.parallelize([1, 2, 3])
rdd2 = sc.parallelize([4, 5, 6])
union_rdd = rdd1.union(rdd2)
union_rdd.collect()
```

### 13. **Broadcast variable**

**Question:** Use a broadcast variable to distribute a lookup table to all nodes.

**Answer:**
```python
lookup_data = {"a": 1, "b": 2, "c": 3}
broadcast_var = sc.broadcast(lookup_data)

rdd = sc.parallelize(["a", "b", "c", "a"])
mapped_rdd = rdd.map(lambda x: (x, broadcast_var.value[x]))
mapped_rdd.collect()
```

### 14. **Calculate distinct values**

**Question:** Calculate the distinct values in an RDD.

**Answer:**
```python
rdd = sc.parallelize([1, 2, 3, 4, 3, 2, 1])
distinct_values = rdd.distinct()
distinct_values.collect()
```

### 15. **Save DataFrame as a table**

**Question:** Save a DataFrame as a Hive table named `employee`.

**Answer:**
```python
spark.sql("CREATE DATABASE IF NOT EXISTS example_db")
df.write.mode("overwrite").saveAsTable("example_db.employee")
```

### 16. **Calculate the top N values**

**Question:** Find the top 3 salaries in the DataFrame.

**Answer:**
```python
top_salaries = df.orderBy(col("salary").desc()).limit(3)
top_salaries.show()
```

### 17. **Explode a column**

**Question:** Explode an array column `tags` in the DataFrame to create a new row for each element.

**Answer:**
```python
from pyspark.sql.functions import explode

exploded_df = df.withColumn("tag", explode(col("tags")))
exploded_df.show()
```

### 18. **Pivot data**

**Question:** Pivot the DataFrame to show the average salary for each department.

**Answer:**
```python
pivot_df = df.groupBy("department").pivot("gender").agg({"salary": "avg"})
pivot_df.show()
```

### 19. **Rename a column**

**Question:** Rename the column `name` to `full_name` in the DataFrame.

**Answer:**
```python
renamed_df = df.withColumnRenamed("name", "full_name")
renamed_df.show()
```

### 20. **Compute correlation between two columns**

**Question:** Compute the correlation between `salary` and `age` columns in the DataFrame.

**Answer:**
```python
correlation = df.stat.corr("salary", "age")
print(f"Correlation between salary and age: {correlation}")
```

---