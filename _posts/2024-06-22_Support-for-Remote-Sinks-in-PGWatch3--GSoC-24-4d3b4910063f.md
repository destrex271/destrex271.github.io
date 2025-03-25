Support for Remote Sinks in PGWatch3: GSoC’24

Support for Remote Sinks in PGWatch3: GSoC’24
=============================================

PgWatch3 is the successor of pgwatch2, a monitoring tool designed specifically to be used with PostgreSQL and its variants like Patroni…

---

### Support for Remote Sinks in PGWatch3: GSoC’24

![](https://cdn-images-1.medium.com/max/800/0*H46rvjuEIVIy9Ojd.png)

PgWatch3 is the successor of pgwatch2, a monitoring tool designed specifically to be used with PostgreSQL and its variants like Patroni etc.. . PgWatch3 comes with a large number of features and improvements over its predecessor.

One of these features is the ability to select specific remote nodes as ‘sinks’ to store all the measurements taken by pgwatch3. These remote sinks can range from simple CSV files to storage in OLAP systems like DuckDB and even for AI workloads.

### What is a Sink?

A sink can be understood as a storage for all the measurements that pgwatch3 takes from your source database. Now it depends on the design of that sink whether to store those measurements or do some kind of processing on them.

### Why do we need to have ‘Remote Sinks’?

Well lets assume that your sink is just a PostgreSQL Database. In that case you can just provide the connection string for it and viola, all the work is done, but lets say that you have an LLM running on a machine and you want to parse your measurements via that LLM and get some insights out of it, or maybe you want to derive some sort of analysis based on the measurements that requires a separate model .

To do this you would basically have to create your own interfaces to make it interact with pgwatch3. To get rid of this manual labor and allow for an easier an innovative way to add your own customized sinks we decided to create a common interface for the users. This completely removed the need for pgwatch3 to know what type of sink is on the other end and its only job is to send the measurements.

### The Architecture

To enable this we are going to use a concept known as *Remote Procedure Calls.* RPC’s can be understood as calling a function defined in a program that is not running on the same machine/ is not part of the same program.

RPC’s allow for smooth data transfer with minimum overhead and are one of the most widely used methods to enable service-to-service interaction. Since pgwatch3 is written in Go, we will be using the native ‘net/rpc’ package that is available in the language. We could have used frameworks like [*gRPC*](https://github.com/grpc/grpc-go) and [*Twirp*](https://github.com/twitchtv/twirp) but they seemed to be an overkill for our purpose.

The new feature will follow the given visualization:

![](https://cdn-images-1.medium.com/max/800/0*Jy-P9_I8DvyJ8Hys)

***pgwatch3: Remote Sinks Architecture***

### Progress So Far

For now the primary receiver has already been designed and you can check it out [*here*](https://github.com/destrex271/pgwatch3_rpc_server). Work is being done on [*integrating the RPC sink mechanism*](https://github.com/cybertec-postgresql/pgwatch3/pull/465) into pgwatch3. Once it is complete we’ll be focusing our energy into developing various sink formats so stay tuned!

By [Akshat Jaimini](https://medium.com/@destrex271) on [June 22, 2024](https://medium.com/p/4d3b4910063f).

[Canonical link](https://medium.com/@destrex271/support-for-remote-sinks-in-pgwatch3-gsoc24-4d3b4910063f)

Exported from [Medium](https://medium.com) on March 25, 2025.