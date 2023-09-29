---
title: Open Source Assignments - Questions
date: 2023-09-29 12:00:00 -0500
categories: [Encora, Weekly Essay]
tags: [apprentice, weekly, encora, open source, oss, questions]     # TAG names should always be lowercase
---
## Overview

The next part in this module is to do some research and answer a question about the stack of our choice (Java for me)

## What does the `@Data` Lombok annotation do under the hood?

The `@Data` annotation in Lombok is a convenient shortcut to automatically generate common boilerplate code in Java classes, such as `getters`, `setters`, `toString()`, `equals()`, and `hashCode()` methods.

By using Lombok annotations like @Data, developers can write cleaner and more concise code without sacrificing readability.

### But, how does it do all that?

* **Lombok uses Annotation Processing (APT):** 

    Annotation Processing is a feature in Java where you can process annotations at compile-time and generate additional code based on those annotations. Lombok leverages this feature.

    Annotations in Java start with the '@' symbol and provide metadata about the code to the compiler or runtime. Lombok's annotations, like @Data, @Getter, @Setter, etc., provide instructions to Lombok's annotation processor on what code to generate.

* **Compiler calls Lombok's Annotation Processor:** When you compile a Java program that uses Lombok annotations, the Java compiler recognizes these annotations and calls Lombok's annotation processor.

    * Lombok's annotation processor analyzes the annotations placed on classes, fields, methods, etc., in the original Java source files. For example, if you annotate a field with @Getter, Lombok knows that a getter method needs to be generated for that field. The annotations in the original files guide Lombok on what specific code needs to be generated.

* **Lombok Code Generation:** Lombok's annotation processor inspects the annotated Java source files. Based on the annotations it finds, Lombok generates new Java source files. These files contain the boilerplate code that developers would otherwise have to write themselves.

    * Code generation for @Data
        * Getters: Lombok generates getter methods for all non-static fields in the class.
        * Setters: Lombok generates setter methods for all non-final, non-static fields.
        equals(Object obj): Lombok generates an equals() method that compares all non-static fields for equality.
        * hashCode(): Lombok generates a hashCode() method that produces a hash code based on all non-static fields.
        * toString(): Lombok generates a toString() method that includes the names and values of all non-static fields.
    * **Code injection:** Lombok uses bytecode manipulation techniques to inject the generated methods directly into the compiled class file. This means that the generated methods become part of the compiled bytecode, even though you didn't write them explicitly in your source code.
    * **Compiled Output**

## Next on the assignment

From the projects we have chosen to contribute to, come up with questions that elicit deep understanding of the project.

## Project to contribute: [Wikimedia Commons Android app](https://github.com/commons-app/apps-android-commons)

    The Wikimedia Commons Android app allows users to upload pictures from their Android phone/tablet to Wikimedia Commons

The particular issue I will be working on is: [Crash when tapping in custom picker while processing #5289](https://github.com/commons-app/apps-android-commons/issues/5289)

I think the following question is relevant to the project and the issue to resolve:

### Question: How do coroutines work in Android?

Coroutines in Android, specifically in the context of Kotlin programming language, provide a way to write asynchronous and non-blocking code more elegantly. They allow developers to write sequential code that looks synchronous, making it easier to understand and maintain asynchronous operations. Coroutines are especially useful for tasks like network requests, database operations, or any other I/O bound operations.

1. Concurrency vs. Parallelism:
    * Concurrency is the concept of running multiple tasks in overlapping time periods, even if only one task is being actively processed at any given moment.
    * Parallelism is the concept of running multiple tasks simultaneously. Coroutines primarily deal with concurrency, not necessarily parallelism.
2. Suspend and Resume:
    * Coroutines allow functions to be paused and resumed.
    * When a coroutine encounters a suspend keyword, it can be suspended without blocking the thread, allowing other tasks to execute.
    * When the suspended operation completes, the coroutine resumes from where it left off.
3. Coroutine Builders:
    * Coroutines are launched using coroutine builders like launch, async, and others.
    * launch is used for fire-and-forget tasks (tasks that you don't need a result from).
    * async is used when you need a result from the coroutine.
4. Coroutine Scopes:
    * Coroutines are always tied to a coroutine scope. The scope determines the lifetime and context of a coroutine.
    * For example, in Android, you might use lifecycleScope or viewModelScope to handle the scope of your coroutines tied to UI components or ViewModels.
5. Dispatchers:
    * Dispatchers define the thread pool or the context in which a coroutine runs.
    * Common dispatchers include Dispatchers.IO (for I/O-bound tasks) and Dispatchers.Main (for UI-related tasks).
6. Suspending Functions:
    * Functions that can be called from coroutines are called suspending functions.
    * Suspending functions can use the suspend modifier and can only be called from other suspending functions or coroutines.
7. Structured Concurrency:
    * Coroutines follow the principle of structured concurrency, meaning that coroutines launched in a specific scope are bound to that scope.
    * When the parent coroutine is canceled, all its child coroutines are automatically canceled.
8. Cancellation:
    * Coroutines are cooperative, meaning they can be canceled.
    * You can explicitly cancel a coroutine job, and well-designed suspending functions periodically check for cancellation to avoid unnecessary work.
9. Exception Handling:
    * Exceptions in coroutines are propagated up to the nearest exception handler.
    * You can use try-catch blocks inside coroutines to handle exceptions.
10. Asynchronous Composition:
    * Coroutines can be used to compose multiple asynchronous operations, making complex asynchronous flows much more readable and manageable.

## Project to contribute: [elasticsearch](https://github.com/elastic/elasticsearch)

    Elasticsearch is a distributed, RESTful search engine optimized for speed and relevance on production-scale workloads. You can use Elasticsearch to perform real-time search over massive datasets for applications including:

    Vector search

    Full-text search

    Logs

    Metrics

    Application performance monitoring (APM)

    Security logs

    ... and more!

The particular issue I will be working on is: [Expand runtime_field data types to include ranges #89707](https://github.com/elastic/elasticsearch/issues/89707)

I think the following question is relevant to the project and the issue to resolve:

### Question: Describe the role of Java Serialization in Elasticsearch.

Java Serialization in Elasticsearch plays a critical role in data storage and retrieval, especially when dealing with distributed systems and data persistence.

Java Serialization is the process of converting Java objects into a byte stream, allowing these objects to be saved in files, sent over networks, or stored in databases. In Elasticsearch, Java Serialization is used to convert complex data structures, such as documents and queries, into a serialized form for storage and transportation. When data is indexed in Elasticsearch, it's often serialized to be stored efficiently in the underlying data store. Similarly, when data is retrieved, it's deserialized back into Java objects for processing.

**Utilization for Data Storage and Retrieval:**

* Data Storage: When documents are indexed in Elasticsearch, they are serialized into a binary format before being stored on disk. This serialized form allows for efficient storage and quick retrieval.

* Data Retrieval: When data is retrieved from Elasticsearch, especially in distributed environments, it's often transmitted as serialized objects. These objects are deserialized back into Java objects on the client-side for further processing or display.

**Challenges and Best Practices:**

* Versioning: One of the challenges with Java Serialization is versioning. If the structure of serialized objects changes (due to code updates, for instance), older versions of the software might not be able to deserialize newer data formats correctly. It's essential to handle versioning carefully to ensure backward compatibility.

* Security: Serialized data can pose security risks if not handled correctly. Ensuring that only trusted sources can deserialize data is crucial to prevent attacks like deserialization vulnerabilities.
