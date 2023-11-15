# Introduction to Apache Iceberg

## 1. What is Apache Iceberg?

Apache Iceberg is an open-source data table format originally developed at Netflix to overcome challenges faced by existing data lake formats like [Apache Hive](https://hive.apache.org/). Boasting capabilities such as support for ACID transactions, time-travel, in-place schema, partition evolution, data versioning, incremental processing, etc., it offers a fresh perspective on open data lakes, enabling fast and efficient data management for large analytics workloads.

Thanks to all this, and especially thanks to its ability to handle partitions and data changes so well, Iceberg is becoming more and more popular, now adopted by many of the top data platform technologies such as Cloudera, Snowflake, Dremio, and so on.

## 2. Architecture of Apache Iceberg

Apache Iceberg has a tiered metadata structure which is key to how Iceberg provides high-speed queries for both reads and writes. Apache Iceberg was built upon three distinct layers: the Iceberg Catalog, the Metadata Layer, and the Data Layer.

![Alt text](image.png)

### Iceberg Catalog

The catalog tracks a reference/pointer to the current metadata file. This is usually some store that can provide some transactional guarantees like a relational database (Postgres, etc.) or metastore (Hive, Project Nessie, Glue).

### Metadata Layer

Apache Iceberg uses three tiers of metadata files which cover three different scopes:

- **Manifest files:** A subset of the snapshot, these files track the individual files in the data layer in the subset along with metadata for further pruning.
- **Manifest lists:** Defines a snapshot of the table and lists all the manifest files that make up that snapshot with metadata on the manifest files for pruning.
- **Metadata files:** Defines the table and tracks manifest lists, current and previous snapshots, schemas, and partition schemes.

### Data Layer

The data layer holds the actual data in the table, which is made up of two types of files:

- **Data files:** Stores the data in file formats such as Parquet or ORC.
- **Delete files:** Tracks records that still exist in the data files, but that should be considered as deleted.

## 3. Key features and advantages of Apache Iceberg

Apache Iceberg offers several key features and advantages that make it a compelling choice for big data management:

1. Schema Evolution: Iceberg provides native support for schema evolution, allowing users to modify table schemas without requiring complex data migration processes. This feature enables seamless adaptation to evolving data structures and simplifies schema management.
2. Transactional Capabilities: Iceberg supports atomic commits and isolation guarantees, making it ACID-compliant. This ensures data integrity and consistency, particularly essential in real-time analytics and when dealing with concurrent data operations.
3. Time Travel: Iceberg's time travel feature allows users to query data at different points in time, providing historical perspectives and facilitating auditability. It enables analysis of past data states, compliance checks, and debugging, making it invaluable for various use cases.
4. Efficient Data Partitioning: Iceberg supports advanced data partitioning strategies, allowing users to organize data based on specific criteria. Partitioning improves query performance by reducing the amount of data scanned during analysis, leading to faster query execution.
5. Indexing Mechanisms: Iceberg provides indexing mechanisms, such as Bloom filters, which enhance query performance by accelerating data filtering. Indexing reduces the amount of data accessed during queries, improving response times and overall efficiency.
6. Centralized Metadata Management: Iceberg separates data and metadata, enabling centralized metadata management. This feature simplifies integration with different query engines and data processing frameworks, ensuring consistency and improving data governance.
7. Compatibility with Popular Data Processing Frameworks: Iceberg is compatible with widely used big data processing frameworks like Apache Spark, Apache Flink, and Presto. This compatibility allows organizations to leverage their existing data ecosystem and seamlessly incorporate Iceberg into their data pipelines.
8. Scalability and Performance: Iceberg is designed to handle large-scale data processing efficiently. It offers optimizations such as column pruning, predicate pushdown, and efficient data file management, resulting in improved performance and scalability for demanding big data workloads.
9. Active Community Support: Iceberg benefits from an active and growing community of users and contributors. This vibrant community ensures regular updates, bug fixes, and feature enhancements, making Iceberg a reliable and well-supported solution.
10. Open-Source and Vendor-Neutral: Iceberg is an open-source project under the Apache Software Foundation, ensuring transparency, flexibility, and vendor neutrality. Organizations can freely adopt and customize Iceberg to suit their specific needs without being locked into any proprietary solutions.

These features and advantages make Apache Iceberg a powerful and versatile table format for big data management. Its support for schema evolution, transactional capabilities, time travel, efficient partitioning and indexing, centralized metadata management, compatibility with popular frameworks, scalability, and active community support contribute to its growing prominence in the big data landscape.