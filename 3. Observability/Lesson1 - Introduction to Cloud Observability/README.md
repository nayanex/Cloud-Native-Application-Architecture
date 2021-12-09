# Course Overview

[![Course Overview](https://img.youtube.com/vi/eWGfsxrFsN8/0.jpg)](https://www.youtube.com/watch?v=eWGfsxrFsN8)

## Glossary

You can download a [PDF glossary](https://video.udacity-data.com/topher/2020/November/5fbe993c_glossary-for-cnand-c4-observability/glossary-for-cnand-c4-observability.pdf) containing the main terms used throughout this course here or at any time from the **Resources** section on the left.

### Course Outline

Here's an outline of all the lessons and topics in this course, for your reference.

#### Lesson 1: Introduction to Cloud Observability

In this first lesson, we'll go over the big picture. Why is observability relevant? And what is your role is as an observability engineer? What tools will you need to be able to conduct observability on your cluster?

* **Big Picture: Monitoring in Clusters**. We'll introduce the big picture of what cloud observability is and how monitoring developed.
* **Business Stakeholders**. As a cloud observability expert, it's important to understand who the various stakeholders are that you'll be interacting with, so you can understand the sort of events you need to monitor for and how others will be using this information.
* **Where to Use Observability**. We'll also talk about the conditions under which observability can be applied, and make a distinction between monitoring your system and observing the individual events within an application.
* **Prerequisites**. We'll briefly go over the skills and concepts you should already have in order to ensure success in this course.
* **Tools, Environment and Dependencies**. Finally, we'll go over a few technical requirements, along with the software and tools you'll need to install for this course.

#### Lesson 2: Observability Tools

This lesson will get you set up with the tools you need to start doing observability in your cluster.

* **Understanding your components**. First, we'll look at the big picture. We'll consider three major needs that we will encounter when trying to do observability: System data, application data, and data visualization. Then we'll discuss why the three tools we're going to use—Prometheus, Jaeger, and Grafana—are great choices for addressing each of these needs.
* **Installing Prometheus, Grafana, and Jaeger.** Next, we'll get into the details of how to install Prometheus, Grafana, and Jaeger, and how to confirm that the installations were successful.
* **Edge Case: Using ELK**. Although the tools we are using in this course are excellent, industry-standard tools, it's always good to be aware of other options you may run into during your time as an observability expert. So at the end of the lesson, we will briefly consider **ELK** or **Elasticsearch**, **Logstash**, **Kibana**, which is a stack that serves as a popular alternative to the one we use in this course.

#### Lesson 3: SLOs, SLIs, and Error Budgets

This lesson is all about **reliability metrics**. In order to observe performance, we first need to get clear on how we are defining and measuring it, and that's what we'll cover here.

* **Defining performance.** The first thing we need to do is define what we mean by site reliability or performance. We will talk about performance in terms of providing a certain level of service, and we'll go over what are called the four golden signals that are used in site reliability modeling.
* **Service-Level Objectives (SLOs)**. We also need a clear objective or goal, and this is where Service-Level Objectives (or SLOs) come in. We will talk about what SLOs are and what factors to consider when setting them.
* **Service-level indicators (SLIs)** . Once we have a clear definition and objective for the level of performance we want to deliver, we need to consider how we will actually measure this performance. This is done using Service-Level Indicators or SLIs.
* **Error Budgets**. Since we cannot guarantee 100% performance, we need to plan for errors. For example, if we are OK with 99% reliability on a metric, that means we have an error budget of 1%. We are deciding that if things get any worse than that 1%, this is a signal to us that an improvement is needed.
* **Building SLAs**. Finally, we will bring this all together and examine Service-Level Agreements or SLAs. While you personally won’t have to worry about SLAs as an SRE, it is important to understand the context of SLAs as it does play a part in the overall SRE model.
#### Lesson 4: Tracing

This lesson is all about **tracing**. Tracing will allow us to get performance data on our applications, particularly on the latency of the key processes within them.

* **Big Picture: What is tracing?** First we will talk about the underlying concept of tracing and how it is different from logs. In particular, we will consider why tracing is increasingly popular in diagnosing latency issues.
* **Distributed Tracing**. In order to do tracing on our Kubernetes cluster, we need an approach to tracing that can handle microservices. This is called distributed tracing. We will explain what distributed tracing is in the context of Kubernetes applications and why this is such a useful tool.
* **Jaeger**. Our tool for distributed tracing is Jaeger. We will discuss the key features of Jaeger as well as the main standards it uses, which are the OpenTracing and OpenTelemetry models.
* **Python Application Tracing**. With Prometheus and Grafana, once we installed them they were pretty much ready to go. In contrast, in order to do tracing with Jaeger, we have to actually add code into the application itself to run a trace. We will walk through how to do this with Python applications.
* **Revisiting Logging**. Finally, we will revisit logging. Although tracing is incredibly useful for issues involving latency, this doesn't mean that you should abandon logging. We will look at some use cases when you will want to utilize logs and consider how how logs are still useful in tracing.


#### Lesson 5: Building Dashboards

In this lesson, we'll look at how we can use Grafana to visualize the data we've been collecting with Prometheus and Jaeger, so that we can see the performance of our system and application at a glance.

* **Starting with dashboards**. First, we'll look at how to set up dashboards with Grafana, and we'll learn the key features of the dashboard UI.
* **Panels**. Next, we'll create panels. These are essentially containers for charts and graphs within our dashboards.
* **Metrics**. Then we will discuss how to use the Prometheus Query Language (PromQL) to track metrics on our cluster, and how to use Jaeger to track metrics on our application.
* **Edge case: Alternative tools**. Finally, we'll look at some alternative tools and learn some of the best practices concerning when we might want to use something other than the Prometheus-Jaeger-Grafana stack for monitoring and observability.

# What You'll Build

[![What You'll Build](https://img.youtube.com/vi/lK9SzKTEdDo/0.jpg)](https://www.youtube.com/watch?v=lK9SzKTEdDo)

For the project at the end of this course, we will create a metrics dashboard. To accomplish this, you'll:

1. Build a **Kubernetes cluster**
2. Create a **monitoring** namespace, in which we will install our monitoring tools, **Prometheus** and **Grafana**
3. Create an **observability** namespace, in which we will install our observability tool, **Jaeger**
4. Create a **default** namespace, where we will install our sample **application** so we have something to monitor

At the end of this process, you'll have your own observability dashboard!

# What is Observability and Why Does it Matter?

[![Monitoring In Clusters](https://img.youtube.com/vi/Y5LyUhncrg0/0.jpg)](https://www.youtube.com/watch?v=Y5LyUhncrg0)

## Monolithic Applications vs Microservices

Let's review the distinction between **monolithic** applications and **microservices**:

* **Monolithic applications**. Monolithic applications have all the services bundled together. The _user interface_, _business logic_ and _data layer_ are all stacked on top of each other, such that making changes to one service can cause all the others to have issues as well.
* **Microservices**. In contrast, with microservices, all of the functions are separated into standalone services that work asynchronously and are distributed in nature. If one service has issues, this does not necessarily impact the rest of the application. Also, due to their small size and portability, microservices are great for Cloud Native development.

## Black Box Monitoring vs White Box Monitoring

There has always been a need to monitor application performance, but the approach to monitoring has changed over time.

* **Black box monitoring**. Historically, we have used _black box monitoring_, which involves getting **indirect** data about the system (such as disk errors, hypervisor resource alerts, or hardware uptime) from the outside and then using this to attempt to infer the cause of a problem (without being able to view the source of the problem directly).
* **White box monitoring**. In _white box monitoring_, we look inside and get **direct** data on the application (such as user utilization, HTTP status errors, and SQL queries); we can directly observe the root cause of the issue.

## Observability

* **Without observability**, we would often have to search through every single service to identify a problem.
* **With observability**, we can look inside the application and even trace through the execution of the application to gather detailed performance data on its individual components.

### QUESTION 1 OF 2

What is **observability**?

[x] It is the ability to measure the internal functions of a system

[ ] It is the ability to watch an application while it deploys

[ ] It is the ability to review logs

[ ] It is the ability to read stdout of your application. 

### QUESTION 2 OF 2

A modern approach to cloud native architecture typically involves…

[ ] A **monolithic**  application and **white box** monitoring, so that we have architecture **with observability**

[ ] A **microservices**-based application and **black box** monitoring, so that we have architecture **with observability**

[ ] A **monolithic**  application and **white box** monitoring, so that we have architecture **without observability**

[x] A **microservices**-based  application and **white box** monitoring, so that we have architecture **with observability**


# Business Stakeholders

[![Business Stakeholders](https://img.youtube.com/vi/9O2CM0u2wj4/0.jpg)](https://www.youtube.com/watch?v=9O2CM0u2wj4)

In a business we have a number of **stakeholders** that are involved in observability:

* **Customers and users** should be the most important stakeholders when it comes to observability, since serving them is typically the main point of the product in the first place (and the ultimate source of revenue, if it is a paid product). They are the ones using our app and we want to make sure that they're having the best experience that they possibly can.
* **Product managers** want to ensure that our customers and users are having the best experience, and that our product is represented properly.
* **Engineering managers** invest a lot of time developing the application and thus have a vested interest in ensuring the product works as intended.
* **Release managers** want to simplify the release process. Anytime they can use observability data to catch an error upon deployment, this can make it easier for them to rollback any problems that occur.
* **Development teams** want feedback so they know what they need to fix and **observability teams** need the same feedback, so that they know what to change when it comes to system adjustments.
* **Partners** may have pipelines that are integrated with your apps. It's very important to them that both sides of the application are working to ensure that that the pipeline is functioning correctly.
* **Investors** want to make sure that the application is healthy so that they have confidence in the reliability and performance of the key product driving the business.
* **Executives** want to ensure that the application is working correctly, especially if it is an application that the business (and the bottom line) are centered around. Executive know that if the customers are having a reliable, high-performance experience with the app, this will contribute to their satisfaction and have a positive impact on revenue.

As you can see, there is a wide variety of stakeholders who all have an interest in observability data. As an observability expert you'll want to keep all of these stakeholders in mind and ensure they are getting the data they need.

### QUIZ QUESTION

Why would a **release manager** care about observability?

[x] The ability to see if an application failed on deploy.

[ ] The ability to see if the application UX is nicer than the old version.

[ ] The ability to change code on the fly. 

[ ] The ability to easily name branches in Git. 

# Monitoring and Observability

Observability has traditionally been broken down into two components: Monitoring and observability. Let's discuss where we would apply each of these approaches and what the distinction is between them.

[![When To Use Observability](https://img.youtube.com/vi/ruRXiYCoeOU/0.jpg)](https://www.youtube.com/watch?v=ruRXiYCoeOU)

### Monitoring

In **monitoring**, we are looking at the system or infrastructure itself. In the context of this course, the system would be a Kubernetes cluster. Monitoring is obviously valuable, but does not tell us what is happening inside of our applications. If an app has performance issues, monitoring will not give us insight on the cause of the issue.

### Observability

In **observability**, we can directly see the internal workings of our applications, including the performance of individual functions and processes. This helps us track down any problems that may exist within the app, or simply identify areas where there is room for improvement in the app's performance.

> Remember, we **monitor systems** and **observe applications**.

## Use Both!

Having both of these tools lets us get a full picture of both the application and the system it's running on. Note that although these are distinct concepts, they are so often used together that you'll commonly hear people say "observability" when they mean monitoring and observability.

### QUESTION 1 OF 2

Which of the following statements are correct?

(Select all that apply.)

[x] Monitoring is used to take a look at the infrastructure

[x] Observability gives us a view inside the app

[ ] Monitoring gives us a view inside the app

[ ] Observability is used to take a look at the infrastructure

### QUESTION 2 OF 2

Below are a few scenarios. See if you can match them up—which are more closely associated with **monitoring** and which are more closely associated with **observability**?

SITUATION | MONITORING OR OBSERVABILITY
----------|----------------------------
Seeing why a pod failed to start | Monitoring
Determining the response time of an application | Observability
Determining an error in Application Execution | Observability
Determining resource usage | Monitoring





