# hadoop_spark_jupyter

This README provides instructions for setting up a Hadoop, Spark, and Jupyter environment using Docker containers.

## Setup Instructions

1. Pull the Docker image:
   ```
   docker pull lokmaneabd/hadoop_spark_jupyter
   ```

2. Create a Docker network with a subnet:
   ```
   docker network create --subnet 172.26.0.0/16 hadoop
   ```

3. Start the first container (`m1`):
   ```
   docker run -it -d --privileged --name m1 --network hadoop -p 4040:4040 -p 8080:8080 -p 8888:8888 -p 9870:9870 --hostname m1 --ip 172.26.0.2 lokmaneabd/hadoop_spark_jupyter/
   ```

4. Start the second container (`m2`):
   ```
   docker run -it -d --privileged --name m2 --network hadoop --hostname m2 --ip 172.26.0.3 lokmaneabd/hadoop_spark_jupyter/
   ```

5. Start the third container (`m3`):
   ```
   docker run -it -d --privileged --name m3 --network hadoop --hostname m3 --ip 172.26.0.4 lokmaneabd/hadoop_spark_jupyter/
   ```

6. Access the first container's shell:
   ```
   docker exec -it m1 bash
   ```

7. Inside the container (`m1`), update the hosts file to include the IP addresses and hostnames of all containers:
   ```
   echo "172.26.0.2 m1" >> /etc/hosts
   echo "172.26.0.3 m2" >> /etc/hosts
   echo "172.26.0.4 m3" >> /etc/hosts
   ```

8. Execute the script to start services:
   ```
   bash start_services.sh
   ```

Now, your Hadoop, Spark, and Jupyter environment should be set up and running. You can access services such as Spark UI, Hadoop NameNode UI, and Jupyter notebooks using the specified ports. Enjoy your data processing and analytics environment!
