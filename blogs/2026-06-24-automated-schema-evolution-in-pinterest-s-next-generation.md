---
title: "Automated Schema Evolution in Pinterest’s Next-Generation DB Ingestion Framework"
url: "https://medium.com/pinterest-engineering/automated-schema-evolution-in-pinterests-next-generation-db-ingestion-framework-36c5c07070de?source=rss----4c5a5f6279b6---4"
date: "2026-06-24"
author: "Pinterest Engineering"
feed_url: "https://medium.com/feed/pinterest-engineering"
---
Yisheng Zhou | Software Engineer II Liang Mou | Sr Staff Software Engineer Gabriel Raphael Garcia Montoya | Staff Software Engineer Istvan Podor | Staff Software Engineer Introduction In the first post of this series , we introduced Pinterest’s next-generation CDC-based ingestion platform built on Kafka, Flink, Spark, and Iceberg. In production, upstream schemas are constantly evolving, and in a distributed CDC pipeline, schema is not just metadata — it is a cross-system contract spanning ingestion, transformation, storage, and historical backfill. A schema change that is not handled carefully
