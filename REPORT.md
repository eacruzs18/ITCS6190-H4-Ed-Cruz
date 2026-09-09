# Hands-on L4 — Report

**Name: Ed Cruz**
**Student ID: 801337361**
**Email: ecruz13@charlotte.edu**

---

## What I ran

The commands you used, in the order you used them. If you deviated from the steps in the
README, say where and why.

1. To start the Cluster via docker compose:
```bash
docker compose up -d
```
2. To build the project:
```bash
mvn clean package
```
3. To copy the generated jar into the Resource Manager container:
```bash
docker cp target/WordCountUsingHadoop-0.0.1-SNAPSHOT.jar resourcemanager:/tmp/
```
4. To copy the dataset into the container:
```bash
docker cp shared-folder/input/data/input.txt resourcemanager:/tmp/
```
5. To open a shell in the container and move to tmp directory:
```bash
docker exec -it resourcemanager bash
cd /tmp
```
7. To create directory, load the data into HDFS and list the file:
```bash
hadoop fs -mkdir -p /input/data
hadoop fs -put ./input.txt /input/data
hadoop fs -ls /input/data
```
8. To run the job and execute the Map Reduce functions on the input text.
```bash
hadoop jar /tmp/WordCountUsingHadoop-0.0.1-SNAPSHOT.jar \
  com.example.controller.Controller /input/data/input.txt /output
```
9. To see the results:
```bash
hadoop fs -cat /output/*
```
10. To copy the results into machine from the container.
```bash
hdfs dfs -get /output /tmp/
exit
docker cp resourcemanager:/tmp/output/. shared-folder/output/
```
11. To stop the cluster:
```bash
docker compose down
```

---

## Input and output

### My input dataset

```

```

### The output the job produced

Paste the contents of your output file here.

```

```

---

## What I observed

A few sentences on what happened while the job was running. Pick whatever you actually
noticed. Some things worth looking at:

- How long the map phase took compared with the reduce phase
- How many DataNodes showed as live at <http://localhost:9870>
- What the ResourceManager at <http://localhost:8088> showed during the run
- Whether the output ordering matched what you expected



---

## Problems and fixes

Anything that went wrong and what resolved it. Paste the actual error message. If nothing
went wrong, say so.


