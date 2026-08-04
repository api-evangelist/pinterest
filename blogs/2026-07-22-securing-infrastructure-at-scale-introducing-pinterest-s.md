---
title: "Securing Infrastructure at Scale: Introducing Pinterest’s Resource Provisioner Pipeline (RPP)"
url: "https://medium.com/pinterest-engineering/securing-infrastructure-at-scale-introducing-pinterests-resource-provisioner-pipeline-rpp-8283bb12cbe5?source=rss----4c5a5f6279b6---4"
date: "2026-07-22"
author: "Pinterest Engineering"
feed_url: "https://medium.com/feed/pinterest-engineering"
---
Ammar Ekbote | Senior Software Engineer Chan Kim | Senior Software Engineer Managing Infrastructure as Code (IaC) across a massive organization comes with a unique set of security and logistical challenges, particularly when operating within a distributed, multi-repository architecture. At Pinterest, we designed the Resource Provisioner Pipeline (RPP) , our specialized, proprietary Terraform execution engine to safely manage both critical and non-critical infrastructure changes. In this post, we will look under the hood of the first iteration of the RPP system.
