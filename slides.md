ElasticSearch at ViaSat

Xavier Lange <xavier.lange@viasat.com>/<xrlange@tureus.com>

Hunter Marshall <hunter.marshall@viasat.com>

---

About Xavier

  * Independent software consultant
  * Years of DevOps experience
  * A year of ElasticSearch experience

---

The Project

  * Enterprise Log Aggregation
  * Gather information from
    * Network equipment
    * Application servers
    * Self-service logging for other users

---

Initial Architecture

  * VMWare ESXi
    * Manually installed ElasticSearch
    * zen discovery
    * Basic puppet for config installation

  * Had performance issues
  * Lack of monitoring

---

Today's Architecture

  * OpenStack
    * Wealth of new resources
    * Used familiar tooling (chef/knife/fog)
    * Static discovery
    * Era of architecture but growing pains of OpenStack installation

---

Many, many iterations

    * Data loss from bad base images
    * Change installed JVM
    * Change ElasticSearch versions
    * Bad reactions to shard storms
    * Exploring opensource monitoring tools
    * Significant effort on metrics
    * Changed memory profile of instances
    * Changed block devices, host to cinder
    * Provisioning and config automation, new node in < 5 minutes

---

Data loss from bad base images

  * Test out restarting your servers, one at a time, just to make sure you can

---

Change installed JVM

The Oracle JVM 1.8 is the best, hands down. Best use of the heap and best handling of memory pressure.

---

Change ElasticSearch versions

Upgraded to 1.7.1 for unprecendented reliability

  * Cluster used to take forever to stabilize
  * Issues ingesting data when shard copying was underway

---

Bad reactions to shard storms

Wanted to intervene manually and disable behavior, etc. Just have to be patient and let it settle down on its own.

---

Exploring opensource monitoring tools

  * CollectD: CPU/Memory/Disk/Network metrics
  * Graphite: metric storage and querying
  * Grafana2: graphing and dashboards
  * es2graphite: metrics in grapite format
  * Free NewRelic monitoring for nice graphs and notifications
 
---

Significant effort on metrics

  * Answers all the questions of
    * What's happened in the last 5 minutes
    * Which host is acting up

---

Changed memory profile of instances

  * Started with multiple 8GB instances
    * OOM killer
  * Went to 16GB instances
    * Less OOM killer
  * Went to 32GB instances
    * No more OOM killer

We also changed ES/JVM versions through this. Not definitive proof of anything in particular but now part of our mythos.

---

Changed block devices, host to cinder

  * Slow host disks caused high IOWAIT
    * One bad disk affected data ingestion across cluster
  * Cinder gave access to larger partitions
    * More retention
    * Higher latency
    * Most consistent performance and no IOWAIT storms

---



---

Provisioning and config automation, new node in < 5 minutes

---