Why should you choose Postgres as your first Database?

Why should you choose Postgres as your first Database?
======================================================

A love letter to PostgreSQL and a brief on why ‘little knowledge is a dangerous thing’

---

### **Why should you choose Postgres as your first Database?**

![](https://cdn-images-1.medium.com/max/800/0*JS1sWt_T-jDHx1by.png)

***Soruce****:* [*https://kinsta.com/wp-content/uploads/2022/03/what-is-postgresql.png*](https://kinsta.com/wp-content/uploads/2022/03/what-is-postgresql.png)

> Little knowledge is a dangerous thing — Alexander Pope

Hello Everyone!

I use PostgreSQL for most of my projects that require a database, and I’ve been asked a recurring question about it by my colleagues and juniors over the past year. For many new engineers — especially those who’ve just *mastered engineering* by *‘creating their first React/Express’* app or *learned to “print hello world”* — database is like a black box that’s taken for granted. I’ve even heard comments like, *“Why PostgreSQL? Isn’t that just SQL? :) :) :)*”(For God’s sake there is a vast difference in SQL and a Database!)

Such misunderstandings have inspired me to write this “love letter” to PostgreSQL and the relational model. I want to explain why new engineers should take the time to explore and understand it.

The goal of this blog post is to encourage people, especially students, to make technology choices based on a solid understanding of the fundamentals rather than just following trends. I hope it helps prevent people from making uninformed claims about any technology stack.

### Why do you even need a Database?

Well this is the first question that I’d like to answer, because believe me I have even heard this phrase from some people :). We’ll try to keep this as simple and short as possible.

Imagine you create a *groundbreaking* expense management app for yourself, but you don’t believe in databases. So, you decide to use a text file instead, with a neat format to store all your financial data.

This looks awesome, right? You can store all your financial data within this file! You even ended up ‘securing the file’ by only allowing some users to perform R/W operations on it.

A few days later, you realize that you want to calculate the average money spent per month. You write a script to read the text file, group the data by month, and compute the average. Then you decide you want fancy graphs showing daily expenses, so you write another script to parse, arrange, and analyze the data. Even a simple task like splitting expenses among multiple users becomes a major headache.

As your app gains users, handling concurrent access, race conditions, data consistency, synchronization, and correctness becomes a nightmare. What was once a fun experiment quickly turns into a complex problem.

In the end, if you’re serious about building an application that delivers real value, you’ll need a database. Even if you stick with text files, you’ll find yourself reinventing many features of a database management system.

### “NoSQL is Clearly Superior to SQL” — (Not That I Heard That from a YouTuber or Anything)

Whenever someone hears that I’m using PostgreSQL as my database, one of the most annoying things they often say is that you should use NoSQL databases *in modern era, instead of writing SQL(For God’s sake just read about ORMs!!!!)*.

First off, “NoSQL” doesn’t mean there’s no SQL at all. For example, MongoDB — which a lot of students get into these days (thanks to the *MERN epidemic*) — is labeled as a NoSQL database. But really, “NoSQL” just means “Non-Relational.”!!

Some people even have the nerve to say that NoSQL is better because it avoids writing “complex, old, and ancient SQL.” While NoSQL has its perks, like flexibility and scalability for certain applications, this viewpoint doesn’t fully appreciate the strengths and versatility of SQL.

**PS:** *If you believe that SQL is dead, please come out from under the rock you’ve been living in.*

It is important to understand that databases roughly vary on the following parameters:

1. **Storage Engines*:*** At the core of Database Management Systems is the way they actually store data. Whether they persist it on disk(like most of the OLTP and OLAP systems out their) or do they keep it in memory. What representation/file format is used to store the data. Whether they are stored in row or columnar formats etc etc... Basically anything that has to do with the way data is being stored comes under storage engines.
2. **Internal Data Structures**: Anyone who has attended a data structures course knows that it is impossible to work with data by just using arrays or single variables. We need to structure our data according to the operations that we are performing on them to get the most optimized results. This is also a part where database systems differ. For example MongoDB uses LSM trees to hold data in memory while Postgres uses concepts of Pages and Buffer Pools to hold data in memory and BTrees(a variation of the actual implementation) for indexes. We can go on and on discussing this topic but it would be better to have a separate article for this.
3. **Query Engines & Optimizes**: This is another aspect where databases end up differing. The primary usage of any database system, whether analytical or transactional, is to retrieve and store data. Therefore its essential that its done in the most efficient way possible.

There are other factors too that differentiate various databases but to make a claim like ‘NoSQL is better than SQL’, you should be aware of the actual meanings of these terms and what are the problems with each one of them.

Relational databases, which are often called SQL databases, use structured tables to organize data. They’re great because they have a clear schema that makes it easier to model and work with data.

On the flip side, NoSQL databases like MongoDB take a more flexible approach with a schema-less design. This means the structure of the data can change from one record to the next.

In a nutshell, NoSQL databases offer flexibility and can sidestep some of the complexities of SQL. But each type of database has its own strengths and fits different needs. So, saying ‘NoSQL is better than SQL’ doesn’t quite cover the whole picture — you need to understand the details and benefits of both to make a fair comparison.

### Why should I start with a relational database?

There’s no hard and fast rule that you must start with a relational database. For example, I started out with MongoDB. However, to fully understand the role of a database in your application, it’s crucial to grasp how it works under the hood — how it handles data, executes queries, and any quirks you might encounter. Starting with a non-relational database can sometimes abstract away these foundational concepts, which may lead to challenges when working with more complex systems later on. As you progress in your software engineering journey, you’ll find that understanding the basics of data management is crucial, far beyond just writing simple programs or designing websites.

The relational model is excellent for building a strong foundation in data modeling and application design. It’s intuitive and helps you visualize the structure of your data clearly. Additionally, learning SQL, which is fundamental in relational databases, provides essential skills that are valuable even if you later work with non-relational databases.

The relational model also introduces you to ACID fundamentals which stand for:

1. **Atomicity**: Ensures that a transaction is an all-or-nothing operation. If a transaction is interrupted or fails, none of its changes are applied, meaning that the effects of the transaction are not visible until it completes successfully.
2. **Consistency**: Guarantees that after a transaction, the database remains in a valid state, adhering to all predefined rules and constraints. This ensures that data remains accurate and conforms to the database’s integrity constraints.
3. **Isolation**: Ensures that each transaction is executed as if it were the only transaction in the system. This prevents transactions from interfering with each other and ensures that intermediate states of a transaction are not visible to other transactions.
4. **Durability**: Guarantees that once a transaction is committed, its changes are permanently recorded in the database. This means that even if the system crashes, the changes made by the committed transaction are not lost.

These principles are crucial when working with a database system. If your database does not support durability, it becomes your responsibility to handle any potential data losses at the application level.

If you treat your database management system as a black box without understanding the basics of how and why data is stored and managed in a particular way and what your interaction actually provide, you might encounter difficulties when dealing with more advanced concepts and features.

### Why PostgreSQL?

Now that we’ve talked about relational databases and why they’re a great starting point, let’s get to the main question: Why should you use PostgreSQL? Why not go with Oracle, MySQL, or another option when starting out?

First off, if Oracle is on your radar, it’s a solid choice with tons of features. But let’s focus on PostgreSQL for now.

PostgreSQL is primarily an Object-Relational Database management system. It follows all the rules laid down by the relational model but at the same it also employs some concepts from the object oriented world. As I mentioned earlier, it is essential to understand ACID. With PostgreSQL you get a database that is fully ACID compliant. The extensive documentation and the amazing community makes it so much easier to understand how and why PostgreSQL ensures maximum ACID compliance out of all the relational database management systems out there, making it perfect for students who are just starting out with Database Management Systems or learning the basics of development.  
Another feature that I really like about PostgreSQL is that it is extensible. You can add extensions just like you do with browser add-ons. If you feel that you require some feature from your database without handling too much at the application layer, you can find an extension or even write one yourselves. For example, you can run LLMs from within PostgreSQL by using extensions like [pg\_vectorize](https://github.com/tembo-io/pg_vectorize) and even use the database as a drop in replacement for message queues by using extensions like [pgmq](https://github.com/tembo-io/pgmq)(or even write it yourself).

PostgreSQL in itself has such a solid foundation that products like [ParadeDB](https://www.paradedb.com/)(which is based on PostgreSQL and Apache Tantivy) have been rivaling domain giants like Elasticsearch.

You can argue that Oracle supports all of this but seriously do you want to spend thousands of Rupees or using a limited cracked version while experimenting and learning? With PostgreSQL not only do you get a free to use implementation but also a system that you can modify according to your learning needs!

To start out you can:

1. Either install PostgreSQL locally(which is very easy to do)
2. Use PostgreSQL from online services like [NeonDB](https://console.neon.tech/), [Tembo](https://tembo.io/) etc…
3. Use it via docker/podman

To conclude, the open source nature of PostgreSQL, its strong alignment with Relational Database Concepts and the amazing ecosystem allows you to have a great learning experience which prepares you to tackle more advanced systems in future.

By [Akshat Jaimini](https://medium.com/@destrex271) on [September 13, 2024](https://medium.com/p/17ece86988ab).

[Canonical link](https://medium.com/@destrex271/why-should-you-choose-postgres-as-your-first-database-17ece86988ab)

Exported from [Medium](https://medium.com) on March 25, 2025.