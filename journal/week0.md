# Week 0 — Billing and Architecture

## Table of Contents
- [Week 0 — Billing and Architecture](#week-0---billing-and-architecture)
  * [What is a User Persona?](#what-is-a-user-persona-)
  * [What is Ephemeral?](#what-is-ephemeral-)
  * [What is a Fractional CTO?](#what-is-a-fractional-cto-)
  * [What is the difference between monolithic architecture and microservice architecture?](#what-is-the-difference-between-monolithic-architecture-and-microservice-architecture-)
  * [What are the benefits of microservices?](#what-are-the-benefits-of-microservices-)
  * [What is the Iron Triangle?](#what-is-the-iron-triangle-)
  * [What is the Tech Stack?](#what-is-the-tech-stack-)
  * [What are the different aspects of a good solution design?](#what-are-the-different-aspects-of-a-good-solution-design-)
  * [What are the three design stages in the Systems Development Life Cycle (SDLC)?](#what-are-the-three-design-stages-in-the-systems-development-life-cycle--sdlc--)
  * [What is The Open Group Architecture Framework (TOGAF)?](#what-is-the-open-group-architecture-framework--togaf--)
  * [Resources](#resources)
  * [Best Practises](#tipsbest-practices)

## What is a User Persona?
A user persona is a fictional representation of a user group for a product, service, or website. It is based on market research and data about behaviours, goals, motivations, and pain points of the target audience. User personas are created to help design and develop products that meet the needs of real users. By creating personas, product teams can empathize with users and make design decisions that are more user-centered, improving the overall user experience. The use of personas also ensures that the design and development teams stay focused on the needs of the target audience throughout the product development process.

Week 0’s scenario lecture included the following user personas: - Tony tells you about the project’s continuity and context - Web Dev Group provides you with information about the current state of the project, including what is important to know, what is not important, what actions you should take, and what has already occurred - Investors care about cost and timing, so it’s important to be very transparent with them about that - CTO is there to give you technical requirements

## What is Ephemeral?
Ephemeral refers to something that is short-lived, temporary, or fleeting in nature. In computing, ephemeral data refers to data that is stored temporarily in memory and is deleted once it is no longer needed. Similarly, ephemeral messaging refers to messages or chats that are deleted automatically after a certain period of time, ensuring that they are not stored permanently.

## What is a Fractional CTO?
Fractional CTO (Chief Technology Officer) is a term used to describe a part-time or temporary CTO who works for a company on a fractional basis. Fractional CTOs are typically hired by startups or small and medium-sized business who do not have the budget or resources to hire a full-time CTO. A fractional CTO works on a part-time basis, providing strategic guidance and leadership on technology-related issues such as product development, software engineering, and IT infrastructure. The fractional CTO works with the existing technology team and management to help the company make informed decisions about technology investments and ensure that the technology strategy aligns with the overall business goals.

## What is the difference between monolithic architecture and microservice architecture?
Monolithic architecture and microservice architecture are two different approaches to designing and building software applications.

In a monolithic architecture, the application is built as a single, tightly-coupled unit, where all components, such as the user interface, business logic, and data storage, are all combined into a single codebase. This makes it easier to develop and deploy the application, but it can also lead to challenges as the application grows in size and complexity.

In contrast, microservice architecture is designed as a collection of loosely-coupled services, where each service is responsible for a specific business function. These services communicate with each other through well-defined APIs and can be developed, deployed, and scaled independently. This makes it easier to maintain and update the application, and also allows for greater flexibility and scalability as the application grows.

Cruddur is designed using a microservice architecture.

## What are the benefits of microservices?
The benefits of microservices architecture include increased agility, flexible scaling, easy deployment, technological freedom, reusable code, and increased resilience. Microservices enable small, independent teams to take ownership of their services, leading to shorter development cycle times. The ability to independently scale services and continuous integration and delivery help to reduce the cost of failure, accelerate time-to-market, and increase flexibility. Teams also have the freedom to choose the best tools to solve their specific problems, leading to increased innovation. Additionally, microservices increase an application’s resistance to failure, as service independence reduces the risk of total application failure in case of component failure.

> Resource: [What are Microservices?](https://aws.amazon.com/microservices/)

## What is the Iron Triangle?
The “Iron Triangle” is a project management concept that represents a trade-off between three constraints in project management: time (schedule), cost (budget, resources), and scope (features, functionality). The idea is that you can only change two of these constraints at a time, and that any change to one of them will impact one or both of the others.

For example, if you need to reduce the cost of a project, you can either shorten the timeline (reduce the time constraint) or reduce the scope of work (reduce the scope constraint). However, changing both time and cost simultaneously is often difficult or impossible. The Iron Triangle is a reminder that trade-offs must be made in project management and that it is essential to prioritize and balance the different constraints.

## What is the Tech Stack?
Front-end: JavaScript, React Back-end: Python, Flask, API Infrastructure: AWS, Docker

## What are the different aspects of a good solution design?

- **Requirements:** These are the technical and business-oriented needs or expectations of stakeholders that the solution must meet to be successful. Requirements may include performance, scalability, security, usability, reliability, cost-effectiveness, and regulatory compliance.
        - Meets ISO standards
        - 99.9% uptime
        - Users can do a specific task

- **Risks:** These are potential problems or challenges that may arise during the implementation or operation of the solution. Risks may include technical, operational, financial, or legal issues that could negatively impact the project’s success. Risks must be mitigated.
        - Single Point of Failure (SPoFs)
        - User Commitment
        - Late delivery

- **Assumptions:** These are statements or beliefs that are taken for granted or presumed to be true, but may not be verified or validated. Assumptions may be made about the environment, user behaviour, technology, or other factors that may affect the solution’s design or performance. These factors are held as true for the planning and implementation phases.
        - Sufficient network bandwidth
        - Stakeholders will be available to make decisions
        - Budget is approved

- **Constraints:** These are limitations or restrictions that may affect the design or implementation of the solution. Constraints may include factors such as budget, time, resources, technology standards, or other dependencies that must be considered when designing the solution.
        - Time
        - Budget
        - Vendor Selection

## What are the three design stages in the Systems Development Life Cycle (SDLC)?

- **Conceptual Design (Napkin Design):** In this stage, the focus is on understanding the requirements and objectives of the system, as well as the needs of the stakeholders. The goal is to develop a high-level conceptual design that outlines the scope, functions, and features of the system. This is often created by business stakeholders and architects.

![Cruddur Napkin Diagram](/_docs/assets/napkin-design.jpeg)

- **Logical Design (Blueprint):** In this stage, the focus is on developing a detailed logical design of the system, which includes defining the data structures, processes, and interfaces required to meet the system requirements and how the system should be implemented. This may include environments without actual names or sizes. The goal is to create a logical design that is flexible, efficient, and scalable.

![Cruddur Architecture Diagram](/_docs/assets/cruddur-architecture.jpeg)

- **Physical Design:** In this stage, the focus is on developing a detailed physical design of the system, which includes defining the hardware, software, and network components required to support the logical design. This represents the actual system built, which may include IP addresses, EC2 instances, etc. The goal is to create a physical design that is reliable, secure, and efficient.

## What is The Open Group Architecture Framework (TOGAF)?
“TOGAF is an architecture framework that provides the methods and tools for assisting in the acceptance, production, use, and maintenance of an enterprise architecture. It is based on an iterative process model supported by best practices and a re-usable set of existing architecture assets.”

**Benefits of TOGAF:**

- The most popular framework for Enterprise Architecture (EA)
- Common dictionary of words to convey desired outcomes
- Meta-model for the creation of the underlying projects
- Maps closely to the Well-Architected Tool

**What is the AWS Well-Architected Framework?**

The AWS Well-Architected Framework is a set of best practices for designing and operating reliable, secure, efficient, and cost-effective infrastructure and applications in the cloud. It provides a comprehensive review of the architectural decisions and trade-offs that go into building and operating systems in the cloud. The framework includes six pillars: operational excellence, security, reliability, performance efficiency, cost optimization, and sustainability. The AWS Well-Architected Framework is intended to help organizations design and evaluate their infrastructure and applications, identify areas for improvement, and implement best practices for cloud architecture.

**The six pillars:**

1. **Operational Excellence:** Focuses on running and monitoring systems to deliver business value and to continually improve processes and procedures. It includes areas such as automation, monitoring, and continuous improvement.
2. **Security:** Focuses on protecting information and systems. It includes areas such as confidentiality, integrity, and availability of data and systems, as well as security best practices and compliance with regulations.
3. **Reliability:** Focuses on ensuring that systems can recover from failures and continue to function as expected. It includes fault tolerance, disaster recovery, and the ability to scale systems.
4. **Performance Efficiency:** Focuses on using resources efficiently and cost-effectively. It includes selecting the right resource types and sizes, optimizing workloads, and managing resources to minimize costs.
5. **Cost Optimization:** Focuses on minimizing costs and maximizing return on investment. It includes cost-effective resource selection, resource utilization, and cost allocation.
6. **Sustainability:** Focuses on reducing the environmental impact of IT systems by minimizing the use of resources such as energy, water, and raw materials, and by adopting sustainable practices throughout the lifecycle of a system.
7. **Resources:** - Introduction to AWS Well-Architected Video by Andrew Brown - AWS Well-Architected - Build secure, efficient cloud applications - AWS Well-Architected Hands-on Labs - AWS Well-Architected Tool

## **Resources:** 

- [Introduction to AWS Well-Architected Video by Andrew Brown](https://www.youtube.com/watch?v=i-hOfAJb3cE) 
- [AWS Well-ArchitectedBuild secure, efficient cloud applications](https://aws.amazon.com/architecture/well-architected/?wa-lens-whitepapers.sort-by=item.additionalFields.sortDate&wa-lens-whitepapers.sort-order=desc&wa-guidance-whitepapers.sort-by=item.additionalFields.sortDate&wa-guidance-whitepapers.sort-order=desc) 
- [AWS Well-Architected Hands-on Labs](https://www.wellarchitectedlabs.com/) 
- [AWS Well-Architected Tool](https://aws.amazon.com/well-architected-tool/)
- [C4 Model](https://youtube.com/playlist?list=PLQ1ygg_ljoUUDP9Lol37vCWlG8pKMpylf&si=kZxFNSem54nGyrwV)
- [Sustainability Pilar](https://docs.aws.amazon.com/wellarchitected/latest/sustainability-pillar/sustainability-pillar.html)
- [Different Models](https://www.bcs.org/articles-opinion-and-research/a-comparison-of-the-top-four-enterprise-architecture-frameworks)

## **Tips/Best Practices*
1. Setting Billing Alerts is the first step to any cloud related project. Before even we start using cloud services. 
2. Asking Question while the meeting will help you in understanding what we are building & construct our Archi Diagram. Understand their Constraints, Risk, Assumptions & Requirements are.
3. Ask "Dumb Questions" eg. What db are we using? How can we build our app in 3 weeks if there are only 2 full time devs? & Think from the perspective of an end user. eg. When logging will there be an auth?     
4. Soft Skills are important while talking to a person who's not in tech. Explaining him so that he understands -- Architecture Diagram. 
5. Document Everything (If a layman doesn't understand from the name, what it does. Document & Explain it)
6. Check if the company has Sustainability goals and figure out something from the Sustainability Pillar.
