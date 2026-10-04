---
title: "Partition Finalization in Pinterest’s Next-Generation DB Ingestion Framework"
url: "https://medium.com/pinterest-engineering/partition-finalization-in-pinterests-next-generation-db-ingestion-framework-4c7da6e4cc8f?source=rss----4c5a5f6279b6---4"
date: "2026-09-25"
author: "Pinterest Engineering"
feed_url: "https://medium.com/feed/pinterest-engineering"
---
Qianrui Zhang | Sr Software Engineer, Logging Platform Kanchi Masalia | Software Engineer II, Stream Processing Platform Liang Mou | Sr Staff Software Engineer, Logging Platform Yi Pan | Principal Engineer, Agent Platform Introduction This is the third post in our series on Pinterest’s next-generation database ingestion framework. Part 1 introduced the DB ingestion framework built on Kafka, Flink, Spark, and Iceberg, and Part 2 covered automated schema evolution. This post tackles another challenge in migrating downstream customers to the new ingestion framework: knowing when data is complete 
