# System architecture

## Overview
This project is a distributed event-driven system that aims to store and process data in real time, inspired by distributed streaming platforms such as Kafka. It is intended as a personal learning project, prioritizing design clarity, separation of responsibilities, and the possibility of evolving the architecture over time.

The main focus is not only on ensuring that the system works, but also on understanding and justifying the architectural decisions made during its construction.

## Goals
- Maintain a clear and easy-to-understand structure.
- Prioritize component decoupling to ensure system scalability, allowing for component updates without the need for structural refactoring.
- Serve as a foundation for learning Java and event-driven architectures.

## Main components

1. Producer
    Responsible for generating or receiving initial events (input data). It can represent:

    - Simulated data
    - Data read from an external source

    Its sole responsibility is to issue events, without knowing how they are subsequently processed.

2. Processor (Broker)
    Responsible for applying business logic to events:

    - Validation
    - Transformation

    This component acts as the core of the system and concentrates processing decisions.

3. Consumer
    Manages the final destination of processed events:

    - Persistence
    - Logging
    - Visualization
    - Sending to another system

    This component is decoupled from the producer and processor.

4. Zookeeper
    Coordinates the cluster and ensures brokers work in a synchronized manner.

The components described in this document represent logical roles (not necessarily one-to-one Java classes or deployment units).

## Overall flow
- The producers send messages to the broker (produce an event), which store them in immutable logs. 
- The event enters the processing pipeline.
- The consumer controls the final output. Periodically reads messages from brokers, recording how far they have processed, so that each message is processed only once and in order.

This flow aims to be linear, clear, and easy to follow, avoiding circular dependencies.

## Key decisions
Java is used for its robustness, extensive ecosystem, good support for concurrency and event processing, and its usefulness for real backend projects.

The project structure aims to reflect responsibilities, not technical details: Separation between domain logic and execution and facilitate code navigation.

## Considered alternatives
- Monolithic architecture with direct calls between classes
- Traditional synchronous processing

These options were discarded in order to prioritize learning and conceptual scalability.

## To be defined
- Specific communication mechanism between components
- Error handling and retries
- Possible persistence of events
- Use or non-use of external frameworks

These decisions will be documented as the project evolves.