
# CHAPTER 1: SCALE FROM ZERO TO MILLIONS OF USERS

## Vertical scaling vs horizontal scaling

Vertical scaling, referred to as “scale up”, means the process of adding more power (CPU,
RAM, etc.) to your servers. Horizontal scaling, referred to as “scale-out”, allows you to scale
by adding more servers into your pool of resources.

## Database replication

A master database generally only supports write operations. A slave database gets copies of the data from the master database and only supports read operations. All the data modifying commands like insert, delete, or update must be sent to the master database. Most applications require a much higher ratio of reads to writes; thus, the number of slave databases in a system is usually larger than the number of master databases.
- Better performance
- Reliability
- High availability

## Cache

A cache is a temporary storage area that stores the result of expensive responses or frequently accessed data in memory so that subsequent requests are served more quickly. every time a new web page loads, one or more database calls are executed to fetch data. The application performance is greatly affected by calling the database repeatedly.The cache can mitigate this problem.

### Cache tier

The cache tier is a temporary data store layer, much faster than the database. The benefits of having a separate cache tier include better system performance, ability to reduce database workloads, and the ability to scale the cache tier independently.

### Considerations for using cache

- **Decide when to use cache**: Consider using cache when data is read frequently but modified infrequently.
- **Expiration policy**: It is a good practice to implement an expiration policy. Once cached data is expired, it is removed from the cache. When there is no expiration policy, cache data will be stored in the memory permanently
- **Consistency**: This involves keeping the data store and the cache in sync.
- **Mitigating failures**: A single cache server represents a potential single point of failure [SPOF]( defined in Wikipedia as follows: “A single point of failure (SPOF) is a part of a system that, if it fails, will stop the entire system from working” )[8]. As a result, multiple cache servers across different data centers are recommended to avoid SPOF.
- 

