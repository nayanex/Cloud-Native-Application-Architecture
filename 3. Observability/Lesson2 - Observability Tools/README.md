# Lesson Overview

In this lesson, we'll look at the main tools we need for cluster observability. We'll discuss why we need these tools conceptually and then we'll go through the process of installing them.

[![Lesson Overview](https://img.youtube.com/vi/5VqsI33rNx0/0.jpg)](https://www.youtube.com/watch?v=5VqsI33rNx0)

This lesson will get you set up with the tools you need to start doing observability in your cluster.

**Understanding your components.** First, we'll look at the big picture. We'll consider three major needs that we will encounter when trying to do observability: System data, application data, and data visualization. Then we'll discuss why the three tools we're going to use—Prometheus, Jaeger, and Grafana—are great choices for addressing each of these needs.
**Installing Prometheus, Grafana, and Jaeger.** Next, we'll get into the details of how to install Prometheus, Grafana, and Jaeger, and how to confirm that the installations were successful.
**Edge Case: Using ELK.** Although the tools we are using in this course are excellent, industry-standard tools, it's always good to be aware of other options you may run into during your time as an observability expert. So at the end of the lesson, we will briefly consider **ELK** or **Elasticsearch, Logstash, Kibana**, which is a stack that serves as a popular alternative to the one we use in this course.

# Big Picture: Understanding Your Components

[![Big Picture-Understanding Your Components](https://img.youtube.com/vi/54FSyQYgG_A/0.jpg)](https://www.youtube.com/watch?v=54FSyQYgG_A)

Here are the key points about all three apps, for your reference:

### Prometheus

* Created by **SoundCloud** in 2012
* Belongs to the **Cloud Native Computing Foundation (CNCF)**
* Collects **system** information (contrast this with Jaeger, which collects application information)
* Has a **time-series database** (you can tag with time stamp, making it easier to keep data in chronological order.
* Has its own querying language, called **PromQL**
* Has **built-in alerting tools**
### Jaeger

* Created by **Uber**
* Belongs to **CNCF**
* Collects **application** information (contrast this with Prometheus, which collections system information)
* Provides a **distributed tracing system**
* Uses the **OpenTracing** data model, although it is transitioning to the **OpenTelemetry** model in future
* **Zipkin** is very similar and is a popular alternative

### Grafana

* **Visualization** platform that allows you to build open source **dashboards**
* Supports **time-series databases** as a backend
* It is often bundled with Prometheus
* Expandable with plugins

### QUESTION 1 OF 2

Below are the three tools we just discussed. Can you can match each of them tools with the most appropriate use case?

PRODUCT | USE CASE
--------|---------
Prometheus | `Time Series Database`
Grafana | `Data Visualization Platform`
Jaeger | `Tracing`

### QUESTION 2 OF 2

Which of the following is a part of **OpenTelemetry**?

[ ] OpenApplication
[ ] OpenWatcher
[ ] OpenNative
[x] OpenTracing






