# Data-Modelling-with-Apache-Cassandra-in-Docker
Modelling data to specific queries with Apache Cassandra in a Docker env.

## Introduction
A startup called Sparkify wants to analyze the data they've been collecting on songs and user activity on their new music streaming app. The analysis team is particularly interested in understanding what songs users are listening to. Currently, there is no easy way to query the data to generate the results, since the data reside in a directory of CSV files on user activity on the app.

This project's goal is to create an Apache Cassandra database which can create tables on song play data to answer the specific song analysis questions.

## Apache Cassandra and Jupyter Notebook with Docker

In this project, all the scripts are run in an Jupter Notebook. A python wrapper/python driver called cassandra was used to connect with Apache Cassandra and run queries. In order to create a stable env for Jupter Notebook and Cassandra connection, this composed docker image could help to run the project easily.

The `docker-compose.yml` script creates the container with Cassandra and Jupter Notebook installed. Please be aware, the Cassandra service was named 'mycassandra' and a local directory named 'notebooks' was mounted to the container , these names could be changed to your own choices.

The `Jupyter` folder include two files: `Dockerfile` and `requirement.txt`. These files are used to fecth the jupyter notebook image from dockerhub, and install required python packages including cassandra and sql wrappers.

To make this container work, first make sure Docker Desktop was installed in your local computer, and then run

    docker-compose up

After the container is running, in the Terminal, look for a line like this:

> http://127.0.0.1:8888/?token=42fbb2bc379cf699026acd0540dee32d2fb57fd5d1f65690

And open in your browser, then the familar jupyter note will appear.

## ETL pipeline and Queries

The `data_modelling_with_apache_cassandra.ipynb` file contains two parts.

In section Part I of the notebook, using python csvreader, iterate through each event file in *event_data* directory to process and create a new CSV file. Here, *even_data* contains a series of csv event logs, are omitted in the repo due to copyright.

In Part II of the notebook, I use CREATE and INSERT statements to load processed records into relevant tables in  Apache Cassandradata Keyspace. There are total 3 data analysis questions to answer, and for each query, a corresponding table with customized Partition Key and Clustering Columns was created along with other relevant columns.

Finally, for each query, the table was tested by running SELECT statements after running the queries on the database.

