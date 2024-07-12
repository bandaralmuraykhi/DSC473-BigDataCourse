# PySpark Docker Setup

## Table of Contents
- [Introduction](#introduction)
- [Prerequisites](#prerequisites)
  - [Windows](#windows)
  - [Mac and Linux](#mac-and-linux)
- [Installation](#installation)
- [Steps](#steps)
  - [Step 1: Pull the Docker Image](#step-1-pull-the-docker-image)
  - [Step 2: Run the Docker Container](#step-2-run-the-docker-container)
  - [Step 3: Access Jupyter Notebook](#step-3-access-jupyter-notebook)
- [Example](#example)
- [Additional Examples and Resources](#additional-examples-and-resources)
- [Scaling PySpark with Docker](#scaling-pyspark-with-docker)
- [Integration with Big Data Tools](#integration-with-big-data-tools)
- [Benefits of Using Docker for PySpark](#benefits-of-using-docker-for-pyspark)
- [Step 4: Stop the Docker Container](#step-4-stop-the-docker-container)
- [Troubleshooting](#troubleshooting)
- [Conclusion](#conclusion)
- [References](#references)

## Introduction
- This is a simple PySpark setup using Docker, providing a good starting point for learning PySpark.
- We'll use the official Jupyter Docker image for PySpark, which includes the Jupyter Notebook server, the Python programming language, and the PySpark library.
- We'll run the Docker container and access the Jupyter Notebook to write and execute PySpark programs.

## Prerequisites

### Windows

- Enable virtualization in the BIOS settings to run Docker on Windows:
  1. Restart your computer.
  2. Press the key to enter the BIOS settings (usually F2, F10, or Del).
  3. Look for the virtualization option in the BIOS settings.
  4. Enable virtualization and save the settings.
  5. Restart your computer.

- Install WSL 2 by following the instructions on the [Install WSL 2](https://learn.microsoft.com/en-us/windows/wsl/install)
### Mac and Linux
- Install Docker Desktop on your machine by following the instructions on the Docker website.

## Installation
Visit the [Docker website](https://docs.docker.com/get-docker/) to download and install Docker on your machine. Follow the platform-specific installation instructions provided in the documentation.

For detailed installation instructions, refer to the following guides:
- [Install Docker Desktop on Windows](https://docs.docker.com/desktop/windows/install/)
- [Install Docker Desktop on Mac](https://docs.docker.com/desktop/mac/install/)
- [Install Docker Engine on Linux](https://docs.docker.com/engine/install/)

## Steps
Follow the steps below to set up the pyspark-notebook Docker image and run the container:

### Open a Terminal or Command Prompt

### Step 1: Pull the Docker Image
```bash
docker pull quay.io/jupyter/pyspark-notebook
```

### Step 2: Run the Docker Container

- For Mac and Linux:
```bash
docker run -it --rm --name pyspark-container -p 8888:8888 -v "${PWD}":/home/jovyan/work quay.io/jupyter/pyspark-notebook
```
- for Windows
```bash
docker run -it --rm --name pyspark-container -p 8888:8888 -v %cd%:/home/jovyan/work quay.io/jupyter/pyspark-notebook
```
Explanation:
- The `-it` flag is used to run the container in interactive mode.
- The `--rm` flag is used to remove the container after it stops running.
- `--name`: Assigns a name to the container for easy reference.
- The `-p 8888:8888` flag is used to map port 8888 on the host machine to port 8888 in the container.
- The `-v "${PWD}":/home/jovyan/work` flag is used to mount the current working directory on the host machine to the `/home/jovyan/work` directory in the container.
- The `$PWD` variable (or `%cd%` on Windows) represents the current working directory.


### Step 3: Access Jupyter Notebook
1. Open a web browser and go to `http://localhost:8888`.
2. Copy the token from the terminal and paste it into the Jupyter Notebook login page.

## Example
To run a simple word count program using PySpark, follow the steps below:

```python
from pyspark.sql import SparkSession

spark = SparkSession.builder.appName("WordCount").getOrCreate()

data = ["Hello World", "Hello Hadoop", "Hello Spark", "Hello Docker"]
rdd = spark.sparkContext.parallelize(data)
words = rdd.flatMap(lambda line: line.split(" "))
wordCounts = words.map(lambda word: (word, 1)).reduceByKey(lambda a, b: a + b)
wordCounts.collect()
```
This example demonstrates a basic word count program using PySpark. It creates an RDD (Resilient Distributed Dataset) from a list of strings, splits each string into words, and counts the occurrence of each word using the `map` and `reduceByKey` transformations. The `collect` action is used to retrieve the results as a list of (word, count) tuples.


## Step 4: Stop the Docker Container
Press `Ctrl+C` in the terminal where the container is running to stop the container.


## Troubleshooting
If you encounter any issues during the setup or while running the container, consider the following:
- Ensure that Docker is properly installed and running on your machine.
- Verify that you have followed the installation instructions for your specific platform.
- Check the Docker logs for any error messages or warnings.
- Make sure that the required ports (e.g., 8888) are not being used by other applications.

If you need further assistance, please refer to the [Docker documentation](https://docs.docker.com/) or seek help from the Docker community.

## Conclusion
In this tutorial, we set up the pyspark-notebook Docker image and ran the container to access the Jupyter Notebook. We also ran a simple word count program using PySpark to verify the setup. You can now explore more PySpark programs and libraries using the Jupyter Notebook.

Using Docker for PySpark development provides portability, reproducibility, isolation, scalability, and resource efficiency. It simplifies the setup process and allows you to focus on writing and running PySpark programs without worrying about the underlying dependencies and configurations.

## Additional Examples and Resources
Here are some additional examples and resources to help you learn and explore PySpark further:

- [PySpark Documentation](https://spark.apache.org/docs/latest/api/python/index.html): Official documentation for PySpark, providing comprehensive information on PySpark APIs and usage.
- [PySpark Tutorial](https://www.tutorialspoint.com/pyspark/index.htm): A tutorial series covering various aspects of PySpark, including RDDs, DataFrames, SQL, and machine learning.
- [PySpark Examples](https://github.com/apache/spark/tree/master/examples/src/main/python): A collection of PySpark example programs provided by the Apache Spark project.
- [Spark by Examples](https://sparkbyexamples.com/pyspark/): A website dedicated to providing examples and tutorials for Apache Spark, including PySpark.
- [PySpark Docker Image](https://hub.docker.com/r/jupyter/pyspark-notebook)
- [Jupyter Docker Stacks Documentation](https://jupyter-docker-stacks.readthedocs.io/en/latest/)