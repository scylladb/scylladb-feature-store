# Integrate ScyllaDB and Feast
Feast is a popular open-source feature store for production ML. You can use several different online stores when you use Feast, including ScyllaDB. ScyllaDB, being a low-latency and high-performance database, serves perfect as an online store. In this section you'll see how you can get started with integrating your ScyllaDB Cloud database into Feast as an online store. 

If you want to learn more specifically about Feast, head over to the [Feast documentation](https://docs.feast.dev/).

## Feast + ScyllaDB online store configuration example
To set up ScyllaDB as a Feast online store you need to edit the configuration file of Feast and add your ScyllaDB credentials. ScyllaDB is Cassandra-compatible hence you can use the built-in Cassandra connector of Feast. 

```yaml
# feature_store.yaml
project: scylla_feature_repo
registry: data/registry.db
provider: local
online_store:
    type: cassandra
    hosts:
        - node-0.aws_us_east_1.xxxxxxxx.clusters.scylla.cloud
        - node-1.aws_us_east_1.xxxxxxxx.clusters.scylla.cloud
        - node-2.aws_us_east_1.xxxxxxxx.clusters.scylla.cloud
    keyspace: feast
    username: scylla
    password: password

```
