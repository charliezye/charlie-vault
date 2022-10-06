# Caching Data Access Strategies

**_Read Through / Lazy Loading:_** Load data into the cache only when necessary. If application needs data for some key **x**, search in the cache first. If data is present, return the data, otherwise, retrieve the data from data source, put it into the cache & then return.

**Advantages:**

1.  It does not load or hold all the data together, it’s on demand. Suitable for cases when you know that your application might not need to cache all data from data source in a particular category.
2.  If there are multiple such cache nodes & a node fails, it does not harm the application although in such situation, the application faces increased latency. As new cache node comes up online, more & more request flows through it & it keeps populating required data with every cache miss.

**Disadvantages:**

1.  For cache miss, there are 3 network round trips. Check in the cache, retrieve from database, pour the data into the cache. So cache causes noticeable delay in the response.
2.  Stale data might become an issue. If data changes in the database & the cache key is not expired yet, it will throw stale data to the application.

**_Write Through:_** While inserting or updating data in the database, upsert the data in the cache as well. So both of these operations should occur in a single transaction otherwise data staleness will be there.

**Advantages:**

1.  No stale data. It addresses the staleness issue of Read Through cache.
2.  Suitable for read heavy systems which can’t much tolerate staleness.

**Disadvantages:**

1.  It’s a write penalty system. Every write operation does 2 network operations — write data to data source, then write to cache.
2.  _Cache churn:_ If most of the data is never read, cache will unnecessarily host useless data. This can be controlled by using TTL or expiry.
3.  In order to maintain the consistency between cache & data source, while writing a data, if any of your cache node goes missing, the write operation fails altogether.

**_Write Behind Caching:_** In this strategy, the application writes data directly to the caching system. Then after a certain configured interval, the written data is asynchronously synced to the underlying data source. So here the caching service has to maintain a queue of ‘write’ operations so that they can be synced in order of insertion.

**Advantages:**

1.  Since the application writes only to the caching service, it does not need to wait till data is written to the underlying data source. Read and write both happens at the caching side. Thus it improves performance.
2.  The application is insulated from database failure. If database fails, queued items can be retried or re-queued.
3.  Suitable for high read & write throughput system.

**Disadvantages:**

1.  Eventual consistency between database & caching system. So any direct operation on database or joining operation may use stale data.

**Application design constraints with write-behind strategy:**

1.  Since in this strategy cache is written first & then database — they are not written in a transaction, if cached items can not be written to the database, some rollback process must be in-place to maintain consistency over a time window.
2.  Write-behind caching may allow out of order database updates, so database have to be able to relax foreign key constraints. Also if the database is a shared database, other apps may also use it, hence no way to know whether write-behind cache updates will conflict with other external updates. This has to be handled manually or heuristically.

**_Refresh Ahead Caching:_** It’s a technique in which the cached data is refreshed before it gets expired. Oracle coherence uses this technique.

> The refresh-ahead time is expressed as a percentage of the entry’s expiration time. For example, assume that the expiration time for entries in the cache is set to 60 seconds and the refresh-ahead factor is set to 0.5. If the cached object is accessed after 60 seconds, Coherence will perform a _synchronous_ read from the cache store to refresh its value. However, if a request is performed for an entry that is more than 30 but less than 60 seconds old, the current value in the cache is returned and Coherence schedules an _asynchronous_ reload from the cache store.

So what refresh ahead caching does is it essentially refreshes the cache at a configured interval just before the next possible cache access although it might take some time due to network latency to refresh the data & meanwhile few thousand read operation already might have happened in a very highly read heavy system in just a duration of few milliseconds.

**Advantages:**

1.  It’s useful when large number of users are using the same cache keys. Since the data is refreshed periodically & frequently, staleness of data is not a permanent problem.
2.  Reduced latency than other technique like Read Through cache.

**Disadvantages:**

1.  Probably a little hard to implement since cache service takes extra pressure to refresh all the keys as and when they are accessed. But in a read heavy environment, it’s worth it.

The point of discussing the strategies is that — while designing the system, you know what kind of system you are designing — whether it’s a read heavy, write heavy or mix of both at a very high scale. Different systems will have different requirements, so it’s very hard to come up with some solid use cases & full-proof strategy. You can choose one or a combination of more strategies as described above according to your use case.