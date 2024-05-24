---
marp: true
title: Short and sweet Prometheus Pushgateway Intro
description: Short and sweet Prometheus Pushgateway Intro
theme: uncover
paginate: true
_paginate: false
style: |
  section {
    font-size: 30px;
  }

---

# Short and sweet

## Intro to Prometheus Pushgateway

---

# Intro, reason & background

* Prometheus can easily scrape metrics of **running** services
* But what about batch jobs or custom metrics?

---

# Use case

## Monitoring transition project progress

---

# Limitations (1)

* [Non-goals](https://github.com/prometheus/pushgateway?tab=readme-ov-file#non-goals)
* Push gateway overwrites metrics unless a unique grouping key provided by the client for the ephemeral instances.
    * Rate of increase: Can misslead that some value is decreasing
    * Distributed counting: Unlike pull based service approach where 1000 transactions per day would have 1 metric, push based approach creates 1000 metrics for 1000 instances. This brings much higher cardinality!
---

# Limitations (2)

* Cleanup challenge: Unlike pull based approach where prometheus is smart enough to clean up the metrics when service is dead, Push Gateway exposes stale metrics forever unless deleted explicitly.
    * Time series: Time filters don't exclude stale metrics
    * Gauge: Aggregation such as "current count of an event" is inaccurate due to stale metrics.
* Histogram based http request times seem to work

---

# Solving Limitations

* The documentation suggests using “Prometheus stats-d exporter” or “prom-aggregation-gateway”
* Alternatively OpenTelemetry collector claims to solve the challenge of aggregations

--- 
# Demo

---

# Links

* https://prometheus.io/docs/introduction/overview/
* https://prometheus.io/docs/practices/pushing/
* https://prometheus.io/docs/instrumenting/pushing/
* https://github.com/prometheus/pushgateway
* https://github.com/prometheus/node_exporter
* https://github.com/zapier/prom-aggregation-gateway
* https://grafana.com/oss/graphite/
* https://graphite.readthedocs.io/en/latest/feeding-carbon.html

---

# Q&A