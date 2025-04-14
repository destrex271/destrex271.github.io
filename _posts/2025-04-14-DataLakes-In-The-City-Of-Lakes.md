# Data Lakes and PostgreSQL in The City of Lakes

Hello Everyone!

I recently had the chance to visit Hyderabad, the "City of Lakes"—ironically, to talk about a different kind of lakes! The PostgreSQL Group Hyderabad has taken an amazing initiative by organizing local meetups every month. They even recently hosted PgDay Hyderabad at the beautiful IIIT campus in 2024, thanks to the efforts of some incredible PostgreSQL enthusiasts and evangelists.

## What was I doing in Hyderabad?

Well, for context, I currently reside in the "beautiful" city of Noida. With the intent to connect with more PostgreSQL contributors and enthusiasts across India, I submitted a proposal for the 11th PostgreSQL meetup in Hyderabad.

This time, instead of presenting one of my personal projects, I wanted to explore a use case that's been gaining traction in the PostgreSQL community: eliminating ETL for migrating data to Data Lake platforms and formats. I’ve recently started exploring pg_duckdb and was excited to share my learnings with the wider community.

Meetups turned out to be the perfect platform for these. To my surprise, my rather basic proposal was
accepted enthusiastically by the organizers. Although my content was quite simplistic, I’m deeply 
grateful to <a href="https://www.linkedin.com/in/hari-kiran-pg/">Mr. Hari Kiran</a> for accepting my proposal, and to <a href="https://www.linkedin.com/in/marodia">Mr. Mukesh Marodia</a> for his uplifting 
words at the end of the meetup! Special thanks to <a href="https://www.linkedin.com/in/bshahakash/">Mr Akash Shah</a> for the awesome support at the meetup!

## Why pg_duckdb?

pg_duckdb is a PostgreSQL extension that embeds DuckDB within Postgres. This allows you to directly interface with platforms like Amazon S3, Iceberg tables, Parquet files, and other components foundational to OLAP platforms—leveraging the DuckDB query engine while retaining PostgreSQL’s powerful and familiar SQL interface.

During my presentation, I was asked about the relative performance of this extension compared to vanilla PostgreSQL with indexes. I wasn’t able to fully answer this at the time, but I’ve since had a chance to reflect. When you consider the very reason Iceberg and similar technologies were invented, it becomes clear why relying solely on indexes in PostgreSQL doesn't quite cut it.

In Data Lake environments, we're often talking about datasets in the order of petabytes. Using indexes alone to query such massive data volumes can cause significant performance bottlenecks during analytical queries. Although I don’t (yet!) have access to such large datasets to validate this theory, I plan to dig deeper into this phenomenon and share my findings soon.
Other components that I think have really great applications include:
 - combining pg_duckdb with timescale db for really powerful real time analytics
 - Utilizing pg_duckdb and pgvector to possibly execute RAG on Data Lake scale environments
 - Scaling pg_duckdb with the Citus PostgreSQL extension.

Moreover, I am firm believer that in the era of AI and Analytics, PostgreSQL already has an upper hand.
As quoted at the meetup as well, You don't need to reinvent the wheel, rather you have all the components to directly construct the entire Car.
Extensions are a huge part of this revolution and I am really hopeful for the times ahead in the PostgreSQL world.

## Conclusion

Hyderabad, to be honest, holds a special place in my heart. The infrastructure, the thriving IT landscape,
the people, the natural beauty, and the essence of Vedic teachings echoing through its picturesque temples—there's a lot to admire.
Blending this atmosphere with the PostgreSQL community was an experience I truly enjoyed, and I’m hopeful to reconnect with the amazing PostgreSQL User Group in Hyderabad again soon!
