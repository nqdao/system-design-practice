# Scalability Topics

## Vertical Scaling

## Horizonal Scaling

## Caching
Cach ei sa simple key-value store that sits between your application and data storage. When application tries to read data, it should try retrieving from cache first. If it is not in cache then it tries to get data from the database.

Cache improves performance by reducing reading data from database. Cach should always be in-memory caches like Memcached or Redis.
- Redis can do several hundreds of thousands of read operations per second.

2 Patterns of caching data:
1. **Cached Database queries** - Whenever there is a query to the database, store the result dataset in cache. Hashed version of query is the cache key. Next time you run the query, check if the result is already in cache.
  - Challenges: It's hard to delete cached results. When a piece of data change, all cached queries containing that change need to be deleted.
2. **Cached Objects** - Store complete instance of the class or property of the class in the cache. When the property changes, it's easier to get rid of the entire object.
  - Enable asynchronous processing. Multiple applications can consume the latest cached object without reading from database.
  - Example objects: User sessions, activity streams.

Redis offers extra database-features like persistence and built-in data structures like lists and sets.
Memcached is easy to scale.

## Load Balancing
- Every server contains the same codebase and does not store user-related data locally - When a user interacts with your service, he may be served requests on different servers. He should always get the same results of the requests back, regardless of which server is serving.
- Sessions need to be sotred in a centralized data store accessible to all application servers. Can be external database or external persistent cache (Redis).
  - Persistent cache has better perforamnce than database.

## Asynchronism
- Preprocess things that take a long time in advance, like building static HTML files on every change.
  - Pros: Fast response time. Easy scalability. Basically result is already available and can be cached.
  - Cons: Not customizable or dynamic. Does not work well with unexpected, unusual requests.
- Use job queue:
  - Frontend inserts new request into the job queue and returns a response to user.
  - Workers watch job queue for job to be done. Once job is done, worker sends a signal.
  - Frontend watches for job done signal to notify the user.
  - Example: RabbitMQ.

## Database Replication
- Master-slave replication

- Denormalization

- Sharding

- SQL tuning

## Database Partitioning

# Performance vs Scalability

# Latency vs throughput

# Availability vs Consistency (CAP Theorem)
