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
map reduce hadoop data cluster node worker task job
data pipeline data processing hadoop cluster worker node
map phase map function map task key value pair
shuffle and sort shuffle sort partition transfer network
reduce phase reduce function reduce task aggregate summary count
hadoop distributed file system hdfs block storage replica
data node name node master worker cluster scale
map reduce job map reduce task map reduce framework
input split record reader key value key value
mapper emits key value intermediate key intermediate value
reducer receives key list values reduce output record
hadoop hadoop hadoop cluster cluster cluster data data data
process batch process big data batch analytics pipeline
node failure fault tolerance heartbeat reschedule task attempt
speculative execution straggler task duplicate worker node
yarn resource manager node manager application master container
map reduce map reduce map reduce hadoop hadoop hadoop
shuffle phase transfers map output to reduce input
sort phase orders keys for reduce task aggregation
count words count frequency count occurrences summarize metrics
worker node executes map task worker node executes reduce task
data locality compute near data hdfs block location
map output spilled to disk buffer memory threshold partition
combiner function mini reducer local aggregation network savings
reduce task writes final output to hdfs data storage
hadoop streaming python mapper python reducer standard input output
docker container docker network hadoop master hadoop worker
test job word count benchmark cluster verification end to end"
```

### The output the job produced

Paste the contents of your output file here.

```
reduce	15
map	13
hadoop	12
data	11
task	10
node	9
cluster	7
worker	7
key	6
value	5
output	5
count	5
phase	4
job	3
function	3
sort	3
hdfs	3
shuffle	3
network	3
master	3
reducer	3
input	3
partition	2
process	2
manager	2
end	2
intermediate	2
block	2
container	2
executes	2
aggregation	2
batch	2
docker	2
pipeline	2
record	2
storage	2
mapper	2
python	2
benchmark	1
transfers	1
attempt	1
pair	1
savings	1
location	1
disk	1
for	1
reader	1
keys	1
and	1
words	1
distributed	1
standard	1
buffer	1
fault	1
name	1
occurrences	1
test	1
heartbeat	1
big	1
list	1
aggregate	1
frequency	1
speculative	1
transfer	1
system	1
failure	1
reschedule	1
execution	1
metrics	1
yarn	1
split	1
replica	1
verification	1
final	1
mini	1
compute	1
threshold	1
summary	1
values	1
duplicate	1
file	1
analytics	1
framework	1
spilled	1
word	1
local	1
combiner	1
processing	1
writes	1
scale	1
receives	1
orders	1
summarize	1
emits	1
near	1
memory	1
straggler	1
tolerance	1
locality	1
streaming	1
application	1
resource	1
```

---

## What I observed

A few sentences on what happened while the job was running. Pick whatever you actually
noticed. Some things worth looking at:

- How long the map phase took compared with the reduce phase?
Even though both the map and reduce phases took almost the same amount of time, the reduce phase took longer to complete because it only started after the map phase was fully complete.
- How many DataNodes showed as live at <http://localhost:9870>?
It showed 3 live DataNodes, with 0 dead and 0 in maintenance.
- What the ResourceManager at <http://localhost:8088> showed during the run?
The ResourceManager showed 2 active nodes. The physical utilization showed 67% memory used, and the allocated resources showed 1 container, 1 vCore, and 2048 MB (2 GB) of memory (accounting for 12.5% of the cluster).
- Whether the output ordering matched what you expected?
Yes, the output aligned with expectations. I intentionally used a synthetic dataset with deliberate word frequencies to clearly validate the aggregation and sorting behavior of the MapReduce pipeline.


---

## Problems and fixes

The only issue encountered during this exercise occurred while executing within GitHub Codespaces. After transitioning to a local environment, all steps ran without issue and completed successfully.


