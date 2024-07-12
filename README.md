# DSC473 Big Data Course

This repository contains materials and projects for the DSC473 Big Data Course. It includes setups for Hadoop and PySpark environments using Docker.

## Repository Structure

```
.
├── Hadoop
│   ├── README.md
│   ├── config
│   ├── docker-compose.yaml
│   └── hadoop_data
│       ├── file1.txt
│       ├── file2.txt
│       └── input.txt
├── PySpark
│   ├── README.md
│   └── dataset
│       └── example.csv
└── README.md
```

## Hadoop

The Hadoop directory contains a Docker setup for running Hadoop 3.3.6. It includes:

- A README.md with detailed instructions on setup and usage
- A `config` file for Hadoop configuration
- A `docker-compose.yaml` file for easy deployment
- Sample data files in the `hadoop_data` directory

For more details, see the [Hadoop README](./Hadoop/README.md).

## PySpark

The PySpark directory contains:

- A README.md with instructions for PySpark setup and usage
- A `dataset` directory with an example CSV file

For more details, see the [PySpark README](./PySpark/README.md).

## Getting Started

1. Clone this repository:
   ```
   git clone https://github.com/bandaralmuraykhi/DSC473-BigDataCourse
   ```

2. Navigate to the desired directory (Hadoop or PySpark)
    ```bash
    cd DSC473-BigDataCourse/Hadoop
    ```
    or
    ```bash
    cd DSC473-BigDataCourse/PySpark
    ```
    and follow the instructions in the respective README.md files.

## Prerequisites

- Docker installed on your system
- Basic understanding of Big Data concepts
- Familiarity with command-line interfaces

## Contributing

If you'd like to contribute to this project, please fork the repository and submit a pull request.

---