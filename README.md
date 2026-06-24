# 📖 PySpark Tutorial

## Introduction

PySpark is the Python API for Apache Spark, a distributed computing framework used for large-scale data processing and analytics.

### Key Features

- Distributed data processing
- Fault tolerance
- In-memory computation
- SQL support
- Machine Learning (MLlib)
- Streaming analytics
- Graph processing

---

### 📌 Run 00_SparkBasics_Databricks.ipynb, in Databricks platform and upload both files there

`Bigmart Sales.csv and drivers.json` in catalogue.


# 🏛️ Architecture

```text
+-------------------+
|   Driver Program  |
+-------------------+
          |
          v
+-------------------+
|   Cluster Manager |
+-------------------+
          |
          v
+-------------------+
|     Executors     |
+-------------------+
```

### Components

#### Driver Program

- Creates Spark Session
- Coordinates execution
- Maintains metadata

#### Executors

- Execute tasks
- Store data in memory
- Return results to Driver

#### Cluster Manager

- Allocates resources
- Manages worker nodes

---

# 📌 Installing PySpark

## Using pip

```bash
pip install pyspark
```

## Verify Installation

```python
import pyspark

print(pyspark.__version__
```



### 🔑 NOTE: **If you get any Java Error, run this command after activating the conda env.**

 > `conda install -c conda-forge openjdk=11`

#### For OS X try `brew install openjdk@17`

---

# Creating Spark Session

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder \
    .appName("PySpark Tutorial") \
    .getOrCreate()

spark
```

---

```python
df.write \
  .format("delta") \
  .mode("overwrite") \
  .save("output_delta")
```

---

# Caching

```python
df.cache()
```

```python
df.unpersist()
```

---

# Performance Optimization

## Repartition

```python
df = df.repartition(4)
```

## Coalesce

```python
df = df.coalesce(2)
```

## Broadcast Join

```python
from pyspark.sql.functions import broadcast

df1.join(
    broadcast(df2),
    "id"
)
```

---

# Common Actions

## Show

```python
df.show()
```

## Count

```python
df.count()
```

## Collect

```python
df.collect()
```

## Take

```python
df.take(5)
```

---

# Common Transformations

## Select

```python
df.select("name")
```

## Filter

```python
df.filter(df.salary > 50000)
```

## GroupBy

```python
df.groupBy("dept")
```

## Join

```python
df1.join(df2)
```

---

# ✨ PySpark Interview Questions

### Difference between Transformation and Action

| Transformation    | Action         |
| ----------------- | -------------- |
| Lazy              | Executes Job   |
| Returns DataFrame | Returns Result |

Examples:

Transformations:

- select()
- filter()
- join()
- groupBy()

Actions:

- show()
- count()
- collect()

---

### What is Lazy Evaluation?

Spark does not execute transformations immediately. It builds a DAG and executes only when an action is called.

---

### What is DAG?

Directed Acyclic Graph used by Spark to optimize execution plans.

---

### Difference Between Repartition and Coalesce

| Repartition                  | Coalesce        |
| ---------------------------- | --------------- |
| Shuffle                      | Minimal Shuffle |
| Increase/Decrease Partitions | Mostly Decrease |
| Expensive                    | Faster          |

---

# 🔑 Using Databricks Online (Free Community Edition)

## Step 1: Create Account

Visit:

https://www.databricks.com

Click:

```text
Try Databricks Free
```

Create an account using email.

---

## Step 2: Create Workspace

After login:

```text
Home
 └── Create Workspace
```

Wait for workspace creation.

---

## Step 3: Create Cluster

```text
Compute
 └── Create Compute
```

Choose:

```text
Single Node Cluster
Runtime: Latest LTS
```

Click:

```text
Create Compute
```

Wait until status becomes Running.

---

## Step 4: Create Notebook

```text
Workspace
 └── Create
      └── Notebook
```

Choose:

```text
Language = Python
```

Attach notebook to cluster.

---

## Step 5: Run PySpark Code

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.getOrCreate()

data = [
    (1, "John"),
    (2, "Alice")
]

df = spark.createDataFrame(
    data,
    ["id", "name"]
)

df.show()
```

---

## Step 6: Upload Files

```text
Catalog
 └── Browse
      └── Upload Data
```

Upload:

- CSV
- JSON
- Parquet
- Delta files

---

## Step 7: Read Uploaded File

```python
df = spark.read.csv(
    "/FileStore/tables/employees.csv",
    header=True,
    inferSchema=True
)

df.show()
```

---
