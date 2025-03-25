Does your database know better? A short note on Database Latches and why they exist

Does your database know better? A short note on Database Latches and why they exist
===================================================================================

---

### Does your database know better? A short note on Database Latches and why they exist

![](https://cdn-images-1.medium.com/max/800/1*xF5KE15XiHjNXWeptiCERg.png)

I was studying about Index Concurrency Control in Databases from the online content of the ***“Intro to Database Systems”*** by Andy Pavlo at CMU where I came across the concept of latches in databases to ensure that multiple workers can work around the internal data structures to improve delivery speed and performance.

One of the things that amused me was that databases tend to implement their own versions of latches using various methods like test-and-set spin locks, Mutex etc. And to implement all of these functionalities they do not rely on the Operating System!

### Well what does the OS have to do with it?

![](https://cdn-images-1.medium.com/max/800/0*4NAt2SzgVmV1g9RN.png)

The diagram shown above is an abstract representation of all layers the Operating System has to manage. There are multiple divisions within these layers as well. Apart from communicating with the hardware an OS is also responsible for the task of resource allocation.

![](https://cdn-images-1.medium.com/max/800/0*aasBG20MKPKupi31.png)

Since there are hundreds of processes running on a single system it is essential to find the sweet spot in terms of efficiency by constantly swapping allocation in and out to avoid deadlocks.

### So Why does it matter for a database?

At the end of the day a database is just a User Application. It requires resources like memory and storage to function properly. Databases utilize Multi-Threading(Multiple Processes in case of PostgreSQL) a lot to ensure efficiency in operations by introducing multiple workers to parse the internal data structures like Hash Tables, B+ Trees etc. Therefore these workers require resources, especially the ones writing to the data structure. The order in which the workers work on a node is usually one of the following:

1. Read-Read
2. Read-Write
3. Write-Read
4. Write-Write

Out of these the Read-Read order is the safest as multiple worker nodes can read the data at the same time while in other cases there are chances of introducing inconsistency.

While allocating resources Operating Systems uses the concept of Locks which are of varying types depending on what the requirements are. For example we have mutexes where applications take on the resource one by one by acquiring this lock. On the other hand we have spin locks which if already acquired by some process requires the thread/process to wait in a queue therefore constantly trying to check if the lock is available(also known as busy waiting).

A simplified representation of busy waiting in spin-locks

Consider a scenario where a worker thread obtains a spinlock from the Operating System to write to the internal data structure in the database. Shortly thereafter, another worker intends to access the data structure to update the same value. However, during the launch of these seemingly consecutive worker tasks, a new resource-intensive application is requested by the user. This application also acquires spinlocks for the same I/O resources. Consequently, there’s a possibility that the second worker may experience a prolonged wait to write to the database because the spinlock has been acquired by the application. Similar issues are possible in case of reads. Such situations can potentially lead to issues with the database system, impacting its performance.

For this reasons most of the databases tend to implement their own versions of Operating System locks known as ‘Latches’.

### What is a ‘Latch’ then?

‘Latch’ is a term that is among a group of terms like pages, locks etc.. which have been utilized in a lot of different contexts. This means that without any proper description it is possible to interpret them in a wrong way.

A ‘latch’ in a database ensures synchronization and physical correction(i.e. the internal representation of data is correct after operations). They can be considered to be the ‘bodyguards’ of worker threads that are currently operating on the data structure in their critical section. Thus essentially stopping the other threads from bullying the database worker from acquiring the required resources.

Latches are also of different types depending upon the needs of the database and might vary across various Databases. In MySQL one such latch that I came across in my brief introduction to this topic is the lock\_sys latch which essentially allows the database to latch the lock\_sys queues. lock\_sys queues contain all the requests for acquiring table and record locks in MySQL. Although MySQL also utilized OS locks to a certain extent too. You can read more about them here: <https://dev.mysql.com/doc/dev/mysql-server/latest/lock0latches_8h_source.html>

A point to note is that latches are not used with Tables as such they are only utilized to work with the internal data structure i.e. to maintain the ‘physical correctness’. Locks are utilized with tables to maintain the ‘logical correctness’ of the data thus relating directly to transactions. Another point to remember when discussing about latches is that they works with regards to maintaining synchronization and consistency in terms of ‘Operations’ performed within a given transaction.

===============================================================

Thanks for Reading! I am relatively new to the field of databases and if you find any problems in this article or any wrong facts, feel free to utilize the comment section.

===============================================================

**References:**

**[1]** **Index Concurreny Control — Andy Pavlo**: <https://www.youtube.com/watch?v=POuQogLy3E8>

**[2]** **MySQL lock\_sys latches:** <https://dev.mysql.com/doc/dev/mysql-server/latest/lock0latches_8h_source.html>

**[3] Latches in PostgreSQL:** <https://minervadb.xyz/how-latches-are-implemented-in-postgresql/>

By [Akshat Jaimini](https://medium.com/@destrex271) on [February 3, 2024](https://medium.com/p/e19cdb613e24).

[Canonical link](https://medium.com/@destrex271/does-your-database-know-better-a-short-note-on-database-latches-and-why-they-exist-e19cdb613e24)

Exported from [Medium](https://medium.com) on March 25, 2025.