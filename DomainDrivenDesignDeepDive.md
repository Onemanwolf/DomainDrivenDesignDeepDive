![image](./images/Designer.png)

# Domain-Driven Design Events Deep Dive


**Domain-Driven Design (DDD)** is an approach to software development that focuses on the domain of the problem you are trying to solve. It is a way of thinking about software development that emphasizes the importance of understanding the domain and modeling it in a way that reflects the business requirements.

**Events** are a key concept in Domain-Driven Design (DDD). They are used to capture changes in the domain and communicate them to other parts of the system. Events are a way to decouple different parts of the system and make it easier to maintain and evolve the system over time.

## Domain-Driven Design (DDD) Events Discovery and Definition

### Best Practices After Discovering and Defining Domain Events

EventStorming is a technique that can be used to discover and define Domain Events in Domain-Driven Design (DDD). It involves collaborative modeling sessions with **domain experts**, **developers**, and other **stakeholders** to explore the domain and identify the events that occur within it. Once the events have been discovered and defined, the next steps usually involve the following:

For more information on EventStorming, check out the following resources: [Introduction to EventStorming](https://leanpub.com/introducing_eventstorming)

**Events** in this context are aligned to the business and use the language of the business. They are not technical events but business events. They are used to capture changes in the domain and communicate them to other parts of the system.

In this stage, we are focused on the business problem space and not the technical solution space. We are trying to understand the domain and the business processes that are involved in the business domain.

**Ubiquitous Language (UL)**: The Ubiquitous Language is the language of the business. It is the language of the business user and experts in the problem space. We also use the Ubiquitous Language in the solution space to name the classes and methods in the code.

Using the Ubiquitous language we discuss the business workflow or process and this discussion will lead to artifacts that will be used to model the domain model which is the logical model of the business processes. Additionally, artifacts will be represented in the codebase as classes and methods that will be used to implement the domain model and the business processes.

**Artifacts**: These artifacts are:

- **Bounded Contexts**: Bounded Contexts are used to represent the language of the business. Additionally, they are used to enforce consistency boundaries in the domain. They have `Commands`, `Events`, `Aggregates`, `ViewModels`, `External Dependencies`, `Factories`, `Repositories`, `Entities`, `Value Objects`, and `Domain Services`.

- **Actor**: An actor is a person or system that executes a command or triggers an event in the domain. They are used to represent the people or systems that interact with the domain.

- **Commands**: Commands are used to change the state of the system. They are used to trigger events in the domain and are used to change the state of the system.

- **Events**: Events are used to communicate changes in the domain to other parts of the system. Additionally, they can trigger commands in other parts of the system.

- **Aggregates**: Aggregates are used to enforce consistency boundaries in the domain. They have Entities, Value Objects, and Domain Services.

- **ViewModels**: ViewModels are used by `Actors` and are displayed in the UI so person `Actors` can make decisions to execute a `Command`.

- **External Dependencies**: External Dependencies are used to represent external dependencies in the domain. They are used to represent external dependencies in the domain and are used to enforce consistency boundaries in the domain.

- **Factories**: Factories are used to create `aggregates`. They are used when there are complex business rules and invariants that need to be enforced consistency boundaries in the domain.

- **Repositories**: Repositories are used to manage the persistence of aggregates. Repositories are concerned only with persisting and retrieving aggregates. Repositories should be aligned to and use the language of the BoundedContext, and the operation should use the language of the business when naming methods and properties. We should place an abstraction layer between the dependent services and the client of the repository.

- **Entities**: Entities are used to represent entities in the domain. They are used to represent entities in the domain and are used to enforce identity in the domain.

- **Value Objects**: Value Objects are used to represent values in the domain. They are used to represent values in the domain and are used to enforce immutability in the domain.

- **Domain Services**: Domain Services are used to encapsulate domain logic. They are used to encapsulate domain logic and are used to enforce domain rules in the domain.

When creating the domain model in code, use the language of the business to name the classes and methods. This will make the code easier to understand and maintain.

**Ubiquitous Language**: The Ubiquitous Language is the language of the business. It is used by the development team to name the classes and methods in the code.

Next, we will have to focus on each Event and dig deeper into the events based on `concert scenarios` that are involved in the domain. This will help to understand the events better and how they are used in the domain. We will focus on the use cases aligned with the concert scenarios that are involved in the domain.

Now that we have discovered and defined the concert scenarios that are involved in the domain, we can now focus on the details of the events that are involved in the domain.

After discovering and defining Domain Events in Domain-Driven Design (DDD), the next steps usually involve diving into the solution space and beginning the process of building the Code Model. At this point, we have crossed into the solution space and are using the artifacts that were created in the problem space to build the code model.

### Events have Boundaries

Events have boundaries; these boundaries encapsulate the behavior and Business language of the Event in what Eric Evans defines as a Bounded Context. The Bounded Context represents a linguistic boundary based on the language of the business, and a Bounded Context is one of the artifacts we discover during the EventStorm workshop. This Bounded Context of the Event encapsulates the behavior of the Event. The Bounded Context is a way to encapsulate the behavior of the Event, and the Event is a way to communicate changes in the domain to other parts of the system.

Events are triggered by Commands, and the Commands are used to change the state of the system. The Commands are used to change the state of the system, and the Events are used to communicate changes in the domain to other parts of the system.

We will discuss in detail Commands and Events in the next section.

1. **Detailing the Event**: Identify the data that the event will carry. This is the data that is required by the downstream services or systems that handle this event in some cases. In some scenarios, the event could be a simple notification that something has happened, and no additional data is required. In case we could just pass the aggregate root identifier of the aggregate root that triggered the event. This is usually done by defining the event class with the necessary properties or fields that represent the data associated with the event.

    - Example: If you have an `OrderCreated` event, you might want to include the `orderId`, `customerId`, `orderDate`, and other relevant information in the event payload.

    - Types of events: There are two types of events in DDD: **Domain Events** and **Integration Events**. Domain Events are internal to the domain and are used to communicate changes within the domain. Integration Events are used to communicate changes between different bounded contexts or external systems.

2. **Event Handlers**: Identify the components that will handle the event. These could be other aggregates, domain services, or even external systems.

3. **Event Trigger**: Identify when the event should be triggered. This is usually in response to a method call on an aggregate root that leads to a state change.

4. **Event Publishing**: Implement the mechanism for publishing the event from the aggregate. This could be done immediately when the event occurs, or it could be done as part of the same transaction when the state change is persisted.

5. **Event Subscribing**: Implement the mechanism for other components to subscribe to the event. This could be done using a message broker in a microservices architecture, or it could be done using an event dispatcher in a monolithic architecture.

6. **Event Handling**: Implement the logic for handling the event in the components that have subscribed to the event. This could involve changing the state of an aggregate, calling a domain service, or sending a message to an external system.

Remember, the goal of Domain Events is to explicitly capture side effects of changes in the domain in a way that is decoupled from the code that triggers the events. This makes the system more maintainable and flexible to changes.

### Domain-Driven Design (DDD), events, and commands are two distinct concepts with different purposes:

- **Commands** represent a request or intent to change the state of the system. They are named in the imperative form (e.g., `CreateOrder`, `UpdateUser`). Commands are sent by one part of the system (typically, the application layer or a client application) to another part of the system (typically, a domain service or an aggregate root).

- **Events** represent something that has already happened in the system. They are named in the past tense (e.g., `OrderCreated`, `UserUpdated`). Events are published by the part of the system where the state change has occurred (typically, an aggregate root) and are consumed by other parts of the system that are interested in that state change (typically, other aggregate roots, domain services, or integration services).

In your scenario, if you're dealing with something that has already happened in the system, you should model it as an event. If you're dealing with a request or intent to change the state of the system, you should model it as a command.

It's important to note that while an event can trigger a command, they are not the same thing and should not be used interchangeably. Mixing these concepts can lead to confusion and can make the system harder to understand and maintain.


The creator of Domain Driven Design is `Eric Evans`. He wrote a book called[ Domain Driven Design: Tackling Complexity in the Heart of Software](https://www.amazon.com/Domain-Driven-Design-Tackling-Complexity-Software/dp/0321125215). The book is a must-read for anyone interested in software design and architecture. It provides a comprehensive overview of the principles and practices of Domain Driven Design and explains how to apply them in practice.

Eric Evans didn't mention Event in his book but it was mentioned later in the book by `Vaughn Vernon` in his book [Implementing Domain-Driven Design](https://www.amazon.com/Implementing-Domain-Driven-Design-Vaughn-Vernon/dp/0321834577). Vaughn Vernon is a thought leader in Domain-Driven Design and has written several books on the subject. He has also spoken at many conferences and has a blog where he shares his thoughts on DDD and other topics.
