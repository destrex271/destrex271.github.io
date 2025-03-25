My Takeaways from the Original Google Spanner Paper

My Takeaways from the Original Google Spanner Paper
===================================================

I recently got the chance to read the original 2012 paper on Spanner. Got to learn some pretty awesome concepts!

---

### My Takeaways from the Original Google Spanner Paper

Hello There!

*(And a Happy New Year!)*

A few days back I came across a post from Google’s LinkedIn handle about Spanner. For anyone who doesn’t know what Spanner is(just like me when I read that post), it is a globally-distributed Database by Google Cloud that offers strong consistency and high availability. The paper focuses heavily on the distributed nature of Spanner, emphasizing how transactions are carried out within a system of such large scale. You can checkout the original paper [here](https://static.googleusercontent.com/media/research.google.com/en//archive/spanner-osdi2012.pdf).

### What makes Spanner Unique?

With a large number of databases and storage solutions in the market , what exactly makes Spanner different? Also even with NoSQL Database services like BigTable from Google itself, why was Spanner built at all? Most of these comparisons are from 2012 and before, when the first paper on Spanner came out.

The research paper does a great job in highlighting the need for Spanner.

#### #1 Compared to BigTable

BigTable is a NoSQL Database Service by Google, targeted for analytical & user facing workloads at scale. For specific applications, there might be a critical need to continuously evolve complex Schemas. Altering schemas in bigtable is a blocking operation and therefore not feasible.

Also BigTable supports eventual consistency i.e. it takes a certain amount of time to replicate writes from leader to read replicas. This is a big drawback for applications that want upto date data at all time.

#### #2 Compared To Megastore

Megastore is another offering by Google which unlike big table has strong consistency but it falls behind in terms of write throughput.

#### #3 True Time API

This is probably the most important factor that sets Spanner apart. TrueTime API allows Spanner to assign an accurate TimeStamp to Transactions/Commits. We’ll discuss the TrueTime API in the next section.

### Spanner Structure — Distributed Setup & Data Model

![](https://cdn-images-1.medium.com/max/800/1*cTMVKNXpFDe_-rFoUS6ubg.png)

Illustration of a single Spanner Universe

A Single deployment of Spanner is known as a Universe and a single universe contains multiple zones. Within each zone we have multiple Span Servers that contain the database, replicas etc.. Out of the thousand of Spa Servers, a single Span Server is made the Zone Master which is responsible to assign data to Span Servers while these Span Servers serve data to the clients. We have a separate unit called the placement driver which is responsible for moving data between zones in a single universe.

Similar to BigTable, Spanner also uses ‘Tablets’ as its base data structure with the following mapping:

> (key:string, timestamp:int64) -> string

As you can see, Spanner also records the timestamp for when each record was operated on/inserted.

### TrueTime API

These two form the core of how spanner ensures Global Consistency and high availability.

![](https://cdn-images-1.medium.com/max/800/0*60t3ltej6hABr6y6.jpeg)

Time Master at Google Data Center(soruce: <https://sookocheff.com/post/time/truetime/>)

The True time API provides globally consistent timestamps(time intervals to be precise) to all the spanservers, ensuring that no node relies on individual clocks. The most interesting part of TrueTime is that it utilizes two sources to measure time

1. A GPS Reference Source
2. Atmoic Clock Source — Armageddon Masters

These two references together form the Time Master. An important question is that why do we even need two time sources. This is a strategic choice which ensures that the chances of both the sources failing at the same time or because of the same reason are near zero. For example GPS receivers can fail by antenna failures, radio interference and are highly prone to spoofing while the ways in which atomic clocks fail (like in presence of a magnetic field) are different and almost mutually exclusive.

The Time Masters are responsible for accurate measurement of time which heavily influences the working of spanner since it relies on timestamps of transactions. To ensure that Time Masters always provide the most accurate time, a variant of [Marzullo’s Algorthim](http://infolab.stanford.edu/pub/cstr/reports/csl/tr/83/247/CSL-TR-83-247.pdf)(An algorithm used to maintain time in a distributed system) is used. Machine Eviction is utilized to protect the Time Masters from any broken clocks.

### Concurrency Control

As mentioned before TrueTime enables features for concurrency control within Spanner. Spanner implements the Paxos Algorithm. Each SpanServer implements a single Paxos state machine on top of each tablet. For each replica(Paxos Group) a leader is elected using the quorum method(even I don’t understand this completely yet, but its similar to a voting mechanism) for a specific period of time i.e. leasing a particular time interval to the leader. This interval is provided by the TrueTime API which are consistent across all instances of Spanner.

Each Paxos Leader is assigned a mutually exclusive lease which ensures that problems like split brain do not occur. At this point even I am not very confident in my understanding of Paxos but with the current superficial knowledge of the algorithm, its easier to understand the importance of TrueTime. The paper also goes into details of how timestamps are assigned to various types of transactions which I’ll save for another blog but there is one Transaction type that I felt was pretty awesome, Schema-Change Transactions.

As I mentioned in the comparison section before, schema evolution is a big portion of what makes Spanner better than BigTable. Unlike BigTable, Spanner implements Non-blocking Schema evolution by putting the schema change transaction at a timestamp in the future. This is pretty ingenious as when the system reaches timestamp t, all the reads and writes are automatically synchronized with the schema changes.

![](https://cdn-images-1.medium.com/max/800/1*3lOsAxy7zLlyS3930HrGyw.png)

Simple Illustration to understand Non Blocking Schema Evolution in Spanner

Again this is all thanks to the TrueTime API since with globally consistent time intervals, it becomes possible to carry out this schema evolution across nodes at various data centers.

### Conclusion

The Spanner Paper is a great read as it introduces concepts like Paxos and again.. TrueTime API*(Maybe is should rename this to TrueTime: why is it awesome?).* I personally enjoyed this read and given that I have very superficial knowledge about distributed systems, this paper provided me with things to look forward to within the coming days.

I am really excited to implement the Paxos Algorithm for replication on my own Key-Value Store implementation — [LokiKV](https://github.com/destrex271/lokiKV). I also plan on reading the BigTable & Megastore papers but for now I would like to learn more about Paxos and try to understand topics that still feel like mystery to me.

Thanks for staying with me so far!

By [Akshat Jaimini](https://medium.com/@destrex271) on [January 1, 2025](https://medium.com/p/a3b2683952fe).

[Canonical link](https://medium.com/@destrex271/my-takeaways-from-the-original-google-spanner-paper-a3b2683952fe)

Exported from [Medium](https://medium.com) on March 25, 2025.