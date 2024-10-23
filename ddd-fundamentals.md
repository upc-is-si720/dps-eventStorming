# Domain-Driven Design (DDD) Fundamentals

Domain-Driven Design (DDD) is a set of principles and patterns that emphasize understanding the complex business domain to a greater extent and using that understanding to model the software. The primary goal of DDD is to create a shared model among stakeholders (domain experts, architects, and developers) that accurately represents the complexities and nuances of the business domain. This shared model guides the development process, ensuring that the software aligns closely with the needs and objectives of the business.

![DDD Starter Modelling Process](/assets/images/fundamentals/ddd-starter-modeling-circular.webp)

_DDD intends to help you identify the crucial parts of your system that will have the most impact on business_.

DDD advocates using a ‘ubiquitous language’, a common language that software developers, businesses, and other stakeholders share. This language, used in the design and implementation of the software, ensures that the software accurately reflects the business domain it is intended to serve.

Domain-Driven Design (DDD) focuses on reducing complexity by dividing the problem into smaller, more manageable subdomains. It involves breaking down a complex domain into distinct subproblems, making it easier to manage and understand.

## DDD Terminology

- **Domain**: The problem space or area of knowledge that the application is concerned with. It comprises all the business logic, rules, and constraints.

- **Ubiquitous Language**: A common language shared by all team members (developers, domain experts, and stakeholders) and used consistently across the project. This language helps ensure that all team members have a shared understanding of the domain concepts and terminology.

- **Bounded Contexts**: Different parts of the domain are divided into distinct boundaries within which a particular model applies. Each bounded context has its own model and rules, and the boundaries help to manage complexity and ensure clarity by dividing the domain into smaller, more manageable pieces.

- **Context Mapping**: Context mapping visualizes the relationships and interactions between different bounded contexts. It helps in understanding how different parts of the system fit together. Types of relationships include shared kernel, customer/supplier, conformist, anti-corruption layer, etc.

- **Entities**: objects that have a distinct identity and lifecycle. They are not defined by their attributes alone but by their unique identity within the domain. For example, in a customer management system, a customer is an entity with a persistent identity, regardless of changes in their name, address, or other attributes.

- **Value Objects**: Objects that are defined by their attributes rather than a unique identity. They are immutable and can be freely shared and reused. Examples of value objects include date ranges, addresses, or monetary amounts.

- **Aggregates**: In complex domains, entities and value objects often have meaningful relationships and dependencies. Aggregates serve as clusters that group entities and value objects, treating them as a single unit. An aggregate has a root entity, known as an aggregate root, each aggregate has a root entity known as the aggregate root, through which all interactions with the aggregate occur and enforce the consistency rules for the aggregate.

- **Repositories**: Mechanisms for accessing aggregates from the persistence store. They provide methods for retrieving and persisting aggregates while encapsulating the data access logic.

- **Services**: operations that do not naturally fit within the domain entities or value objects. Domain services encapsulate domain logic that is not tied to a specific entity.

- **Factories**: Patterns used to create complex objects and aggregates. They encapsulate the creation logic and ensure that the created objects are in a valid state.

- **Domain Events**: events that are significant within the domain and represent something that has happened. They are used to communicate changes and trigger actions within the domain.

### Deep dive into Domain

DDD divides the domain into three subdomain categories.

- Core Subdomain
- Supporting Subdomain
- Generic Subdomain

#### Core Subdomain 

Core Subdomain is what makes your product unique from other products. The core domain is so critical and fundamental to the business that it gives you a competitive advantage and is a foundational concept behind the business.

This is the domain you want your most experienced people to work on, instead of having them work on complex (and fun) technical or infrastructure problems.

For example, in an e-commerce application, the core domains include product management, order management, supply chain management, compliance and risk management, and many others.

#### Supporting domains

Supporting domains aid the core subdomain by providing necessary capabilities that are important but not unique or critical to the business’s competitive advantage. In short, a supporting subdomain is a subdomain that is necessary for the product to succeed, but it does not fall into the core domain category.

For an e-commerce platform, the supporting subdomain might include inventory management and customer support systems.

#### Generic Subdomain

The Generic Subdomain encompasses parts of the domain that are common across different businesses and industries. These subdomains provide standard functionalities that are not specific to the business’s unique needs. For an e-commerce platform, the generic subdomain might include authentication and logging.

## Domain Modeling using DDD

Domain modeling using DDD is categorized into two main aspects—strategic and tactical design.

![DDD Strategic and tactical design](/assets/images/fundamentals/strategic-and-tactical-design.webp)

### Strategic Design

Strategic Design deals with understanding and defining the broader business context and ensuring that the software architecture aligns with business goals and strategies. **Strategic DDD** is useful for dividing **large and complex business problem(s)** into multiple chunks with **clear boundaries** and **specific responsibilities** to build high-level software design.

Strategic design primarily focuses on:

- Understanding the problem space and breaking it down into use cases very clearly.
- Identifying the business core domains and subdomains (**Core, Supporting and Generic Subdomains**).
- Defining the clear boundaries between different parts of the system (**Bounded Context**)
- Mapping relationships between different Bounded Contexts (**ContextMap**)

### Tactical Design

Tactical Design focuses on the detailed design and implementation within the boundaries defined by strategic DDD. It provides patterns and practices for modeling and implementing the domain logic. It is a set of **patterns and building blocks** to refine the results of strategic patterns applied to a stage where it can be converted into **working code**.

Tactical design primarily focuses on: 

- Identifying the **entities** and **value objects**.
- Define **Aggregates**. Aggregates play a crucial role in managing data integrity and transactional boundaries.
- Define **Repositories** and **Factories**.
- Define **Domain services** and **Domain Events**.

Strategic DDD helps in organizing and structuring the domain at a high level, ensuring alignment with business goals and managing complexity through bounded contexts and context mapping. Tactical DDD provides the detailed design and implementation patterns necessary to model and implement the domain logic within the boundaries defined by strategic DDD. Together, they provide a comprehensive approach to designing and developing complex software systems.


## Applying Domain Design Principles for Your Complex Product

Domain-Driven Design (DDD) initiative for a new complex project involves a series of structured steps to ensure that the design is aligned with business goals.

![DDD Starter Modeling Steps](/assets/images/fundamentals/ddd-starter-modeling-steps.webp)

### 1. Initiate Discovery and Preparation

- **Stakeholder Engagement**: Identify the key stakeholders (domain experts, business analysts, project sponsors, etc.) and assemble a cross-functional team including domain experts, developers, QA, UX designers, and architects. Conduct initial meetings to understand business goals, challenges, and expectations.
- **Training**: ensure team members are familiar with DDD principles or arrange for training if necessary.
- **Define High-Level Objectives**: Outline the project’s high-level goals, use cases, scope, and constraints, and identify key success metrics and deliverables.

### 2. Domain Exploration: Deep-dive Sessions

- **Create the Ubiquitous Language**: Develop a shared/common language that accurately reflects domain concepts and terminology. Ensure all team members adopt and use this language consistently.
- **Event Storming Workshops**: Organize event storming sessions with all the stakeholders to explore the domain comprehensively. The outcome of Event Storming sessions is identifying the domain events, commands, and external systems. These sessions help you to uncover insights, identify pain points, and define core processes.

### 3. Define Bounded Contexts

- **Identify Bounded Contexts**: Break down the domain into distinct bounded contexts based on business capabilities and areas of responsibility. Each context should have clear boundaries and its ubiquitous language. The outcome is all the domain contexts along with key responsibilities.
- **Context Mapping**: Create a context map to visualize relationships and interactions between bounded contexts. Identify and document types of relationships (e.g., shared kernel, customer/supplier, conformist, and others).

### 4. Model the Domain

- **Detailed Domain Modeling**: Identify and define entities, value objects, aggregates, and domain services within each bounded context. Use collaboration sessions with domain experts to refine and validate the model.
- **Define Aggregate Boundaries**: Establish aggregate boundaries to ensure consistency and transactional integrity. Identify aggregate roots and design repositories for data persistence.

### 5. Design Microservices

- **Align Microservices with Bounded Contexts**: Start designing microservices to align with bounded contexts, ensuring they are cohesive and loosely coupled. Define clear APIs and events for inter-service communication.
- **Ensure Autonomy and Independence**: Each microservice should be independently deployable, and scalable. It should have its own databases.

### 6. Implement Core DDD Patterns

- **Implement Aggregates and Repositories**: Develop aggregates to encapsulate business rules and maintain consistency. Implement repositories to manage aggregate persistence and encapsulate data access logic.
- **Develop Domain Services**: Create domain services to handle complex business logic that doesn’t fit naturally within entities or value objects.
- **Use Factories and Domain Events**: Implement factories to handle complex aggregate creation. Use domain events to capture significant domain occurrences and trigger necessary actions.

### 7. Iterative Development and Continuous Feedback

- **Agile Iterations**: Use agile methodologies to develop the system in iterative cycles. Regularly deliver increments of the software to gather feedback and make improvements.
- **Continuous Feedback Loops**: Establish mechanisms for continuous feedback from users, stakeholders, and team members. Use feedback to refine the domain model, improve processes, and address technical debt.

### 8.Documentation, Knowledge Sharing, and Adapatbility

- **Maintain Comprehensive Documentation**: Document the domain model, bounded contexts, context map, and service contracts. Keep documentation up to date to reflect changes and new insights.
- **Facilitate Knowledge Sharing**: Conduct regular knowledge-sharing sessions, workshops, and retrospectives. Encourage collaboration and open communication within the team.
- **Adapt to Changes**: Be prepared to adapt the domain model and architecture in response to changing business requirements. Foster a culture of continuous improvement and learning.

## Reference

https://anjireddy-kata.medium.com/architecture-and-design-101-domain-driven-design-ddd-fundamentals-b2dd1571d666

https://github.com/SAP/curated-resources-for-domain-driven-design