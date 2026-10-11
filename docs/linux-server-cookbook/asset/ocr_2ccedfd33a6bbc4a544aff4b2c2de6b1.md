+   - **Horizontal scaling:** Adding nodes to share the load is a simple task in *NoSQL*.

+   - **Fast queries:** Querying a *NoSQL* is faster than a relational database.

+   - **Ease of use for developers:** For developers, it is easier to use *NoSQL* to store structured or unstructured data.

Some of the popular open-source database *NoSQL* solutions available are as follows:

+   - **MongoDB**: A document database with the scalability and flexibility that you want with the querying and indexing that you need.

+   - **Apache Cassandra**: A database designed to store data for applications that require fast read and write performance.

+   - **Apache CouchDB**: A document database that collects and stores data in JSON-based document formats.

+   - **Apache Hbase**: A distributed big data store.

+   - **Redis**: An in-memory key-value data structure store that can be used as a database, cache, or message broker.

+   - **Neo4j**: A graph database management system.

# ## MongoDB databases

MongoDB is one of the most popular NoSQL databases used on Linux systems. MongoDB has the following three different editions:

+   - **Community Server**: It is free and available for Windows, Linux, and macOS.

+   - **Enterprise Server**: It is free and available for Windows, Linux, and macOS.

+   - **Atlas**: It is available as an on-demand fully managed service. MongoDB Atlas runs on AWS, Microsoft Azure, and Google Cloud Platform.

The installation of the *Community* version on Ubuntu requires the following steps:

+   1. Import the public key to use *MongoDB’s* package repository. The following command shows perform it:

```
wget -qO - https://www.mongodb.org/static/pgp/server-6.0.asc
| sudo tee /etc/apt/trusted.gpg.d/mongodb.asc
```