# Hadoop 3.3.6 Docker Setup and Usage Guide for Beginners

This guide provides a step-by-step tutorial on setting up and using Hadoop 3.3.6 with Docker. It is tailored for beginners and students, with detailed explanations and examples to make the learning process easier.

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


## Setup

Follow these steps to set up the Hadoop environment using Docker:

1. Clone the repository:
   - Open a terminal or command prompt.
   - Run the following command to clone the repository containing the Hadoop Docker setup:
     ```bash
     git clone <repository-url>
     ```
   - Navigate to the cloned repository directory:
     ```bash
     cd <repository-directory>
     ```

2. Start the Hadoop cluster:
   - In the terminal, run the following command to start the Hadoop cluster using Docker Compose:
     ```bash
     docker compose up -d
     ```
   - This command will download the necessary Docker images and start the Hadoop containers in detached mode (`-d` flag).

3. Verify the containers are running:
   - To check the status of the running containers, use the following command:
     ```bash
     docker compose ps
     ```
   - This command will display a list of the running containers, including their names, states, and ports.

4. Stopping the cluster:
   - When you're done using the Hadoop cluster, you can stop it using the following command:
     ```bash
     docker compose down
     ```
   - This command will stop and remove the containers, but it will preserve the data stored in `hadoop_data` directory.

## Basic Hadoop Operations

Now that the Hadoop cluster is up and running, let's explore some basic Hadoop operations.

### Accessing the Hadoop Environment

To interact with the Hadoop environment, you need to access the resourcemanager container:

```bash
docker compose exec resourcemanager bash
```

This command will open a bash shell inside the resourcemanager container, allowing you to run Hadoop commands.

### HDFS Commands

HDFS (Hadoop Distributed File System) is the primary storage system used by Hadoop. Here are some basic HDFS commands:

1. List the contents of the root directory:
   ```bash
   hdfs dfs -ls /
   ```
   This command will display the files and directories in the HDFS root directory.

2. Create a new directory:
   ```bash
   hdfs dfs -mkdir -p /user/root/input
   ```
   This command creates a new directory called `input` under the `/user/root/` path. The `-p` flag ensures that parent directories are created if they don't exist.

3. Upload a local file to HDFS:
   - Create a local file:
     ```bash
     echo "Hello Hadoop World" > local_file.txt
     ```
     This command creates a file named `local_file.txt` with the content "Hello Hadoop World".
   - Upload the local file to HDFS:
     ```bash
     hdfs dfs -put local_file.txt /user/root/input/
     ```
     This command uploads the `local_file.txt` file from the local filesystem to the `/user/root/input/` directory in HDFS.

4. View the contents of a file:
   ```bash
   hdfs dfs -cat /user/root/input/local_file.txt
   ```
   This command displays the contents of the `local_file.txt` file stored in HDFS.

5. Remove a file or directory:
   ```bash
   hdfs dfs -rm -r /user/root/input
   ```
   This command removes the `input` directory and all its contents from HDFS. The `-r` flag is used for recursive removal.

6. Copying a file from Hadoop to the local filesystem:
   ```bash
   hdfs dfs -get /user/root/input/local_file.txt ./local_file2.txt
   ```
   This command retrieves the file `local_file.txt` from the `/user/root/input/` directory in HDFS and copies it to the specified local path.

7. Copying multiple files from the local filesystem to Hadoop:
   ```bash
   hdfs dfs -put hadoop_data/file1.txt hadoop_data/file2.txt /user/root/input/
   ```
   This command copies multiple files (`file1.txt` and `file2.txt`) from the local filesystem to the `/user/root/input/` directory in HDFS.

8. Merging multiple files in Hadoop:
   ```bash
   hdfs dfs -getmerge /user/root/input/ hadoop_data/merged.txt
   ```
   This command merges all the files in the `/user/root/input/` directory in HDFS into a single file named `merged.txt` on the local filesystem.

9. Checking the size of a file in Hadoop:
   ```bash
   hdfs dfs -du -h /user/root/input/local_file.txt
   ```
   This command displays the size of the file `local_file.txt` in a human-readable format (`-h` option) in the `/user/root/input/` directory in HDFS.

10. Renaming a file in Hadoop:
    ```bash
    hdfs dfs -mv /user/root/input/old_name.txt /user/root/input/new_name.txt
    ```
    This command renames the file `old_name.txt` to `new_name.txt` within the `/user/root/input/` directory in HDFS.

11. Deleting a file in Hadoop:
    ```bash
    hdfs dfs -rm /user/root/input/local_file.txt
    ```
    This command deletes the file `local_file.txt` from the `/user/root/input/` directory in HDFS.

12. Creating an empty file in Hadoop:
    ```bash
    hdfs dfs -touchz /user/root/input/empty.txt
    ```
    This command creates an empty file named `empty.txt` in the `/user/root/input/` directory in HDFS.

13. Displaying the contents of a file in Hadoop:
    ```bash
    hdfs dfs -cat /user/root/input/local_file.txt
    ```
    This command displays the contents of the file `local_file.txt` located in the `/user/root/input/` directory in HDFS.

14. Counting the number of directories, files, and bytes in Hadoop:
    ```bash
    hdfs dfs -count /user/root/
    ```
    This command counts the number of directories, files, and bytes under the `/user/root/` directory in HDFS.

15. Checking the disk space usage of a directory in Hadoop:
    ```bash
    hdfs dfs -du -s -h /user/root/
    ```
    This command displays the disk space usage of the `/user/root/` directory in HDFS in a summary format (`-s` option) and in a human-readable format (`-h` option).

## Running MapReduce Jobs

MapReduce is a programming model and processing technique for big data sets. Let's look at a couple of examples of running MapReduce jobs in Hadoop.

### Example 1: Word Count

The Word Count example counts the occurrences of each word in a given input file.

1. Create an input file:
   - Create a local file with some text:
     ```bash
     echo "Hello World Bye World" > input.txt
     ```
   - Upload the file to HDFS:
     ```bash
     hdfs dfs -put input.txt /user/root/input/
     ```

2. Run the Word Count job:
   ```bash
   hadoop jar $HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-examples-*.jar wordcount /user/root/input /user/root/output
   ```
   This command runs the Word Count example job using the `hadoop` command. It takes the input file from `/user/root/input` and stores the output in `/user/root/output`.

3. View the results:
   ```bash
   hdfs dfs -cat /user/root/output/*
   ```
   This command displays the contents of the output files generated by the Word Count job.

4. Removing the output directory:
   - If you want to run the job again with the same output directory, you need to remove the existing output directory first:
     ```bash
     hdfs dfs -rm -r /user/root/output
     ```
     This command removes the `output` directory and its contents from HDFS.

### Example 2: Pi Estimation

The Pi Estimation example estimates the value of Pi using a Monte Carlo method.

Run the Pi Estimation job:
```bash
hadoop jar $HADOOP_HOME/share/hadoop/mapreduce/hadoop-mapreduce-examples-*.jar pi 10 100
```
It uses 10 maps and 100 samples per map to estimate the value of Pi.

### Example 3: Customizing Hadoop Configuration

- You can customize the Hadoop configuration by modifying the `config` file in your project directory.

- Restart the Hadoop cluster to apply the changes:
   ```bash
   docker compose down
   docker compose up -d
   ```

## Troubleshooting

If you encounter any issues while running Hadoop, you can view the Hadoop logs for debugging purposes.

View the logs of the resourcemanager container:
```bash
docker compose logs resourcemanager
```

View the logs of the namenode container:
```bash
docker compose logs namenode
```

These commands will display the logs of the respective containers, which can help in identifying and resolving any issues.

## References

For more detailed information and advanced topics, refer to the following resources:

- Apache Hadoop Documentation: https://hadoop.apache.org/docs/r3.3.6/
- Hadoop Docker Image: https://hub.docker.com/r/apache/hadoop
- MapReduce Tutorial: https://hadoop.apache.org/docs/r3.3.6/hadoop-mapreduce-client/hadoop-mapreduce-client-core/MapReduceTutorial.html

These resources provide comprehensive documentation, tutorials, and examples to further enhance your understanding of Hadoop.

---