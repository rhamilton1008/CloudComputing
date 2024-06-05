# Running Hadoop

1. Make a working directory somewhere

  ```
  mkdir running-hadoop
  cd running-hadoop
  ```

2. Clone the big-data-europe fork for commodity hardware

  ```
  git clone https://github.com/big-data-europe/docker-hadoop
  cd docker-hadoop
  ```

3. Make sure docker is running. You can test it by running the following line of code

  ```
  docker run hello-world
  ```

4. Bring the Hadoop containers up

```
docker-compose up -d
```

5. Look through the containers uning "docker ps"and choose the one named "name node"

```
CONTAINER ID   IMAGE                                                    COMMAND                  CREATED          STATUS                    PORTS                                            NAMES
87cbbc44b45a   bde2020/hadoop-nodemanager:2.0.0-hadoop3.2.1-java8       "/entrypoint.sh /run…"   10 minutes ago   Up 10 minutes (healthy)   8042/tcp                                         nodemanager
da5b86021c83   bde2020/hadoop-namenode:2.0.0-hadoop3.2.1-java8          "/entrypoint.sh /run…"   10 minutes ago   Up 10 minutes (healthy)   0.0.0.0:9000->9000/tcp, 0.0.0.0:9870->9870/tcp   namenode
316569f1a114   bde2020/hadoop-datanode:2.0.0-hadoop3.2.1-java8          "/entrypoint.sh /run…"   10 minutes ago   Up 10 minutes (healthy)   9864/tcp                                         datanode
c00f5558bcac   bde2020/hadoop-historyserver:2.0.0-hadoop3.2.1-java8     "/entrypoint.sh /run…"   10 minutes ago   Up 10 minutes (healthy)   8188/tcp                                         historyserver
86485d34995a   bde2020/hadoop-resourcemanager:2.0.0-hadoop3.2.1-java8   "/entrypoint.sh /run…"   10 minutes ago   Up 10 minutes (healthy)   8088/tcp                                         resourcemanager
```

I ran this code to access the container

```
docker exec -it namenode /bin/bash
```

6. Make a directory called app and three directories within app (data, res, and jars)

```
mkdir app
mkdir app/data
mkdir app/res
mkdir app/jars
```

7. Fetch data to app/data
I got three books from gutenburg to populate the data dir

```
cd /app/data
curl https://www.gutenberg.org/cache/epub/1342/pg1342.txt -o austen.txt
curl https://www.gutenberg.org/cache/epub/84/pg84.txt -o shelley.txt
curl https://www.gutenberg.org/cache/epub/768/pg768.txt -o bronte.txt
```

Check that there are substancial files in the data directory

```
ls -al
```
My result
```
total 1884
drwxr-xr-x 2 root root   4096 May 30 02:01 .
drwxr-xr-x 5 root root   4096 May 30 01:59 ..
-rw-r--r-- 1 root root 772420 May 30 02:00 austen.txt
-rw-r--r-- 1 root root 693877 May 30 02:01 bronte.txt
-rw-r--r-- 1 root root 448937 May 30 02:01 shelley.txt
```

8. We are using WordCount.jar which luckily is in the repo so we can curl it again

```
cd /app/jars
curl https://github.com/wxw-matt/docker-hadoop/blob/master/jobs/jars/WordCount.jar -o WordCounter.jar
```

9. After I curled the WordCounter.jar this is the step that I coundn't get past.
