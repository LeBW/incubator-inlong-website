---
Quick Start - Apache InLong-sort
---

## Set up flink environment
Currently inlong-sort is based on flink, before you run an inlong-sort application,
you need to set up flink environment.

<a href="https://ci.apache.org/projects/flink/flink-docs-release-1.9/ops/deployment/cluster_setup.html" target="_blank">how to set up flink environment</a>

Currently, inlong-sort relys on flink-1.9.3. Chose `flink-1.9.3-bin-scala_2.11.tgz` when downloading package.

Once your flink environment is set up, you can visit web ui of flink, whose address is stored in `/${your_flink_path}/conf/masters`.

## Prepare installation files
All installation files at `inlong-sort` directory.

## Starting an inlong-sort application
Now you can submit job to flink with the jar compiled.

<a href="https://ci.apache.org/projects/flink/flink-docs-release-1.9/ops/deployment/yarn_setup.html#submit-job-to-flink" target="_blank">how to submit job to flink</a>

Example：

- `./bin/flink run -c org.apache.inlong.sort.flink.Entrance inlong-sort-core-1.0-SNAPSHOT.jar --cluster-id my_application --zookeeper.quorum 127.0.0.1:2181 --zookeeper.path.root /inlong-sort --source.type tubemq --sink.type hive`

Notice：

- `-c org.apache.inlong.sort.flink.Entrance` is the main class name

- `inlong-sort-core-1.0-SNAPSHOT.jar` is the compiled jar

## Necessary configurations
- `--cluster-id ` which is used to represent a specified inlong-sort application
- `--zookeeper.quorum` zk quorum
- `--zookeeper.path.root` zk root path
- `--source.type` source of the application, currently "tubemq" and "pulsar" are supported
- `--sink.type` sink of the application, currently "clickhouse" and "hive" are supported

Configurations above are necessary, you can see full configurations in

`~/Inlong/inlong-sort/common/src/main/java/org/apache/inlong/sort/configuration/Constants.java`

**Example**

`--cluster-id my_application --zookeeper.quorum 192.127.0.1:2181 --zookeeper.path.root /zk_root --source.type tubemq --sink.type hive`

##  All configurations
|  name | necessary  | default value  |description   |
| ------------ | ------------ | ------------ | ------------ |
|cluster-id   |  Y | NA  |  used to represent a specified inlong-sort application |
|zookeeper.quorum   | Y  | NA  | zk quorum  |
|zookeeper.path.root   | Y  | "/inlong-sort"  |  zk root path  |
|source.type   | Y | NA   | source of the application, currently "tubemq" and "pulsar" are supported  |
|sink.type   | Y  | NA  | sink of the application, currently "clickhouse" and "hive" are supported  |
|source.parallelism   | N  | 1  | parallelism of source  |
|deserialization.parallelism   | N  |  1 | parallelism of deserialization  |
|sink.parallelism   | N  | 1  | parallelism of sink  |
|tubemq.master.address | N  | NA  | tube master address used if absent in DataFlowInfo on zk  |
|tubemq.session.key |N |"inlong-sort" | session key used when subscribing to tubemq |
|tubemq.bootstrap.from.max | N | false | whether consume from max or not when subscribing to tubemq |
|tubemq.message.not.found.wait.period | N | 350ms | The time of waiting period if tube broker return message not found |
|tubemq.subscribe.retry.timeout | N | 300000 | The time of subscribing tube timeout, in millisecond |
|zookeeper.client.session-timeout | N | 60000 | The session timeout for the ZooKeeper session in ms |
|zookeeper.client.connection-timeout | N | 15000 | The connection timeout for ZooKeeper in ms |
|zookeeper.client.retry-wait | N | 5000 | The pause between consecutive retries in ms |
|zookeeper.client.max-retry-attempts | N | 3 | The number of connection retries before the client gives up |
|zookeeper.client.acl | N | "open" | Defines the ACL (open/creator) to be configured on ZK node. The configuration value can be set to “creator” if the ZooKeeper server configuration has the “authProvider” property mapped to use SASLAuthenticationProvider and the cluster is configured to run in secure mode (Kerberos) |
|zookeeper.sasl.disable | N | false | Whether disable zk sasl or not |
