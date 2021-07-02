# Architecture Consideration for Cloud Native Applications

## Introduction

[![Introduction To Monoliths And Microservices](https://img.youtube.com/vi/3AM5kur6w9M/0.jpg)](https://www.youtube.com/watch?v=3AM5kur6w9M)

Before building an application, it is common to go through a design phase to identify the main requirements and structure of an application. In correlation with the available resources, a team will choose the most suitable project architecture.

In the industry, usually, the two main approaches that are usually referenced are **monoliths and microservices**.

We will cover:

* Monoliths and Microservices
* Trade-offs for Monoliths and Microservices
* Practices for Application Development

## Design Considerations for Cloud-Native Applications

[![Design Considerations For Cloud-Native Applications](https://img.youtube.com/vi/t62N9-IoutA/0.jpg)](https://www.youtube.com/watch?v=t62N9-IoutA)

When building an application it is important to allocate time for context discovery. This includes listing all necessary functionalities of the application and enumerating any resources that can enable its buildout. This phase sets the fundamentals of the project. If properly implemented, it can enable the creation of services that are scalable, resilient, and extensible.

The first step in the context discovery process is to list the **functional requirements**, or what application capabilities should deliver to the end-users. For example, a good starting point is to expand on the following:

* Stakeholders
* Functionalities
* End users
* Input and output process
* Engineering teams

The second step is to enumerate the available resources that facilitates the implementation of the project. For example, a good starting point is to list available:

* Engineering resources
* Financial resources
* Timeframes
* Internal knowledge

Also very importatnt to define priorities. What needs to come first?
  
Having a good understanding of functional requirements and available resources can lead to a simpler choice between monolithic and microservice-based architectures.

## Monoliths And Microservices

[![Monoliths And Microservices](https://img.youtube.com/vi/Sk0pgRgb6KU/0.jpg)](https://www.youtube.com/watch?v=Sk0pgRgb6KU)

Prior to an organization delivers a product, the engineering team needs to decide on the most suitable application architecture. In most of the cases 2 distinct models are referenced: monoliths and microservices. Regardless of the adopted structure, the main goal is to design an application that delivers value to customers and can be easily adjusted to accommodate new functionalities.

Also, each architecture encapsulates the 3 main tires of an application:

* UI (User Interface) - handles HTTP requests from the users and returns a response
* Business logic - contained the code that provides a service to the users
* Data layer - implements access and storage of data objects

### Monoliths

In a monolithic architecture, application tiers can be described as:

* part of the same unit
* managed in a single repository
* sharing existing resources (e.g. CPU and memory)
* developed in one programming language
* released using a single binary

![A booking application referencing the monolithic architecture](https://video.udacity-data.com/topher/2020/December/5fdd2602_screenshot-2020-12-18-at-21.57.06/screenshot-2020-12-18-at-21.57.06.png)

Imagine a team develops a booking application using a monolithic approach. In this case, the UI is the website that the user interacts with. The business logic contains the code that provides the booking functionalities, such as search, booking, payment, and so on. These are written using one programming language (e.g. Java or Go) and stored in a single repository. The data layer contains functions that store and retrieve customer data. All of these components are managed as a unit, and the release is done using a single binary.

### Microservices

In a microservice architecture, application tiers are managed independently, as different units. Each unit has the following characteristics:

* managed in a separate repository
* own allocated resources (e.g. CPU and memory)
* well-defined API (Application Programming Interface) for connection to other units
* implemented using the programming language of choice
* released using its own binary
  
![A booking application referencing the microservice architecture](https://video.udacity-data.com/topher/2020/December/5fdd26ac_screenshot-2020-12-18-at-22.01.07/screenshot-2020-12-18-at-22.01.07.png)

Now, let's imagine the team develops a booking application using a microservice approach.

In this case, the UI remains the website that the user interacts with. However, the business logic is split into smaller, independent units, such as login, payment, confirmation, and many more. These units are stored in separate repositories and are written using the programming language of choice (e.g. Go for the payment service and Python for login service). To interact with other services, each unit exposes an API. And lastly, the data layer contains functions that store and retrieve customer and order data. As expected, each unit is released using its own binary.

### New terms

* **Monolith**: application design where all application tiers are managed as a single unit
* **Microservice**: application design where application tiers are managed as independent, smaller units

### Further reading

[What’s the Difference Between Monolith and Microservices](https://nordicapis.com/whats-the-difference-between-monolith-and-microservices/)
[Microservices vs Monolithic Architecture](https://www.mulesoft.com/resources/api/microservices-vs-monolithic)