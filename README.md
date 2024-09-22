# Hadoop WordCount Example with Docker

## Project Overview
This repository demonstrates how to run Hadoop's WordCount example within a Docker container, using a simple text file as input.

## Prerequisites
Before you begin, ensure that you have the following installed on your local machine:
- Docker

## Setup Steps

### 1. Create the Project Directory
Start by creating a directory for your project where all the files will be stored:
```bash
mkdir hadoop-wordcount-example
cd hadoop-wordcount-example
2. Create a Dockerfile
The Dockerfile will define the setup for Hadoop inside a container. Create the file:


touch Dockerfile
Add the following content to the Dockerfile:

Dockerfile

# Use a pre-configured Hadoop image
FROM sequenceiq/hadoop-docker:2.7.1

# Set the working directory
WORKDIR /home/hadoop-3.3.6

# Copy the input file to the container
COPY data.txt /home/hadoop-3.3.6/data.txt

# Run Hadoop WordCount example
CMD ["/etc/bootstrap.sh", "-bash"]
3. Create the Input File (data.txt)
This is the file that Hadoop will use as input for the WordCount example. Create it with the following command:


touch data.txt
Add the following content to data.txt:

Italy Venice
Italy Pizza
Pizza Pasta Gelato

4. Build the Docker Image
To build the Docker image with Hadoop and the input file, run the following command in your terminal:

bash
Copy code
docker build -t hadoop-wordcount .
This will create a Docker image named hadoop-wordcount using the Dockerfile.

5. Run the Docker Container
Start a Docker container from the image you built:


docker run -it hadoop-wordcount
This will open a bash shell inside the running container.

6. Run the WordCount Example
Now that you are inside the running container, execute the Hadoop WordCount example using the following command:


bin/hadoop jar share/hadoop/mapreduce/hadoop-mapreduce-examples-3.3.6.jar wordcount data.txt output
Hadoop will process the data.txt file and create the word count results in the output directory.

7. View the Output
To view the results of the WordCount program, use the cat command to read the output file:


cat output/part-r-00000
The expected output should be:


Gelato  1
Italy   2
Pasta   1
Pizza   2
Venice  1
