# Exam objectives for 1Z0-819(Java SE 11 Developer, Oracle Certified Professional)
Since Sept. 2020 it includes both 1Z0-815 and 1Z0-816 (!)
* Working with Java data types
  * Use primitives and wrapper classes, including, operators, parentheses, type promotion and casting
  * Handle text using String and StringBuilder classes
  * Use local variable type inference, including as lambda parameters
* Java Object-Oriented Approach
  * Declare and instantiate Java objects including nested class objects, and explain objects' lifecycles (including creation, de-referencing by reassignment, and garbage collection)
  * Define and use fields and methods, including instance, static and overloaded methods
  * Initialize objects and their members using instance and static initializer statements and constructors
  * Understand variable scopes, apply encapsulation and make objects immutable
  * Create and use subclasses and superclasses, including abstract classes
  * Utilize polymorphism and casting to call methods, differentiate object type versus reference type
  * Create and use interfaces, identify functional interfaces, and utilize private, static, and default methods
  * Create and use enumerations
* Working with Arrays and Collections
  * Use generics, including wildcards
  * Use a Java array and List, Set, Map and Deque collections, including convenience methods
  * Sort collections and arrays using Comparator and Comparable interfaces
* Java Platform Module System
  * Deploy and execute modular applications, including automatic modules
  * Declare, use, and expose modules, including the use of services
* Java I/O API
  * Read and write console and file data using I/O Streams
  * Implement serialization and deserialization techniques on Java objects
  * Handle file system objects using java.nio.file API
* Database Applications with JDBC
  * Connect to and perform database SQL operations, process query results using JDBC API
* Annotations
  * Create, apply, and process annotations
* Controlling Program Flow
  * Create and use loops, if/else, and switch statements
* Exception Handling
  * Handle exceptions using try/catch/finally clauses, try-with-resource, and multi-catch statements
  * Create and use custom exceptions
* Working with Streams and Lambda expressions
  * Implement functional interfaces using lambda expressions, including interfaces from the java.util.function package
  * Use Java Streams to filter, transform and process data
  * Perform decomposition and reduction, including grouping and partitioning on sequential and parallel streams
* Concurrency
  * Create worker threads using Runnable and Callable, and manage concurrency using an ExecutorService and java.util.concurrent API
  * Develop thread-safe code, using different locking mechanisms and java.util.concurrent API
* Secure Coding in Java SE Application
  * Develop code that mitigates security threats such as denial of service, code injection, input validation and ensure data integrity
  * Secure resource access including filesystems, manage policies and execute privileged code
* Localization
  * Implement Localization using Locale, resource bundles, and Java APIs to parse and format messages, dates, and numbers


# How to prepare for 1Z0-819 exam
* Books: As of now there is no book specifically for this exam. However, since this exam combines almost all of the topics of 1Z0-815 and 1Z0-816 exams, 
you may use the 1Z0-815 book and 1Z0-816 book.
* Additionally, you should also go through the updated [Java Secure Coding Guidelines](https://education.oracle.com/product/pexam_1Z0-819).
* Mock Exams: Finally, use [1Z0-819 mock exams](https://enthuware.com/java-certification-mock-exams/oracle-certified-professional/ocp-java-11-exam-1z0-819) to practice answering certification style questions. Since this exam covers a very broad range of topics, you will need to practice with a large number of questions so that you don't miss any topic.


# OCP JAVA 11 CERTIFICATION 1Z0-819 EXAM EXPERIENCE
Our content experts got questions on the following topics, and as explained above, since the number of questions were so less (only 50), some topics were completely left out. Of course, this doesn't mean that the exam doesn't have questions on these topics. Another candidate may get a different set of questions, which may include questions on these topics.

* Modules:
  * Only a few of basic conceptual questions.
  * No question on advanced topic such as services, migration strategies, command line options,
  * Question on jdeps output.
* Security: Two code based questions on doPriviledged. No question on other topics. 
* JDBC:
  * Only a couple of basic questions involving PreparedStatement.
  * Code uses DataSource.getConnection instead of DriverManager.getConnection.
  * No ResultSetMetaData
  * No DriverManager, transactions, savepoint questions.
* Multithreading/Locking:
  * No question on Atomic classes
  * No question on locks
  * Couple of tough questions on ExecutorService
* File I/O:
  * Simple question on methods of Files.copy method involving options such as REPLACE_EXISTING and symbolic links.
  * Question on seriaization
  * No question on Paths or Path relativize
  * No question on Console
* Arrays/Collection/Stream: Several questions
  * Lot of questions used the boxed() method.
  * Heavy focus on autoboxing of elements of a stream.
  * Heavy focus on List.of and List.copyOf methods
  * No question on Deque but TreeSet was used
* Overloading: No complicated question on method resolution.
* Advanced question on Enum
* Advanced question on Annotation
* Simple question on exceptions.

###Remarks:
* One question had 10, yes, 10, options! A couple of them had 7 or 8 options as well. Most had 4-5 though. 
* Only a few questions were very lengthy to read (they had a long problem statement). Most were not so much.
* Time was enough.
* Overall the test did not seem too hard in terms of mind tricks but was hard in terms of depth of understanding required. You can't just read a topic cursorily and expect to answer exam questions on it. For example, the questions on enums and annotations requried that you know the complete ins and outs of how they work.
