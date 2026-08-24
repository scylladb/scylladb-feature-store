# Integrate ScyllaDB and Feast
[Feast](https://feast.dev/) is a popular open-source feature store for production ML. You can use several online stores when using Feast, including ScyllaDB. ScyllaDB, a low-latency and high-throughput database, serves perfectly as an online store. In this section, you'll see how you can integrate your ScyllaDB Cloud database with Feast as an online store.

If you want to learn more about Feast, read the [Feast documentation](https://docs.feast.dev/).

## Feast + ScyllaDB online store configuration example
Feast ships with a native ScyllaDB online store connector, built on the `scylla-driver` Python package.

To set up ScyllaDB as a Feast online store you need to

1. Install Feast with the ScyllaDB extra
1. Edit the Feast configuration file

### Install Feast with the ScyllaDB extra
```
pip install feast[scylladb]
```

### Edit the Feast configuration file
```yaml
# feature_store.yaml
project: repo
registry: data/registry.db
provider: local
online_store:
    type: scylladb
    hosts:
        - node-0.aws_us_east_1.xxxxxxx.clusters.scylla.cloud
        - node-1.aws_us_east_1.xxxxxxx.clusters.scylla.cloud
        - node-2.aws_us_east_1.xxxxxxx.clusters.scylla.cloud
    username: scylla
    password: xxxxxxx
    keyspace: feast
    local_dc: AWS_US_EAST_1
entity_key_serialization_version: 3
```

Key configuration options for the `scylladb` online store:
* `hosts`: contact-point addresses of your cluster (required)
* `port`: CQL port (default: `9042`)
* `keyspace`: target keyspace (default: `feast_keyspace`)
* `username` / `password`: authentication credentials
* `local_dc`: datacenter name used for DC-aware load balancing (required for ScyllaDB Cloud, e.g. `AWS_US_EAST_1`)
* `read_concurrency` / `write_concurrency`: number of concurrent in-flight statements (default: `100` each)
* `vector_similarity_function`: default similarity function for vector search — `COSINE`, `DOT_PRODUCT`, or `EUCLIDEAN` (default: `COSINE`)

For more information, read the [Feast documentation](https://docs.feast.dev/reference/online-stores/scylladb).
