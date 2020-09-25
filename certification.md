# HOW TO PASS 1Z0-816 OCP JAVA 11 PART 2 EXAM

## Mock Exams
 - [ ] OCP Java 11 - 1Z0-816 Mock Exams Practice Tests/Questions Part 2
 
## Books for OCP Java 11 Certification 1Z0-816
There are no books specifically geared towards OCP Java 11 Part 2 1Z0-816 exam.
 
##  Collection of books and resources for Oracle Certified Professional Java SE 11 Programmer Part 2 exam 1Z0-816
Following books, articles, and links will cover all that is required for this exam. 
If you are preparing to take the 1Z0-816 exam, this path should help you pass 1Z0-816 exam:
- [ ] Start with any OCP JP 8 (1Z0-809) book such as 
  - [ ] [Boyarksy/Selikoff](https://www.amazon.com/gp/product/1119067901/ref=as_li_tl?ie=UTF8&tag=ewhome-20&camp=1789&creative=9325&linkCode=as2&creativeASIN=1119067901&linkId=394d2034df2322c936e73206cc997d2f) 
  - [ ]  [Sierra/Bates](https://www.amazon.com/gp/product/1119067901/ref=as_li_tl?ie=UTF8&tag=ewhome-20&camp=1789&creative=9325&linkCode=as2&creativeASIN=1119067901&linkId=d35ee432659d13ce49388919aab4ff7d).
  
(!)Ignore the following topics in these books:
 * Singleton/Immutability
 * static initializers/blocks
 * Date/Time related topics<BR/>

Following topics from the above books are mandatory to learn:
- [ ] Lambda Expressions (including functional interfaces)
- [ ] Parallel Streams
- [ ] Lambda Operations on Streams
- [ ] Language Enhancements - try with resources, multi catch, Java File I/O (NIO.2)
- [ ] If you have time, go through these topics also (these are not explicitly mentioned in the objectives but are part of Concurrency):
  - [ ] java.util.concurrent.atomic package 
  - [ ] parallel Fork/Join Framework
- [ ] Study the following new topics from any Java 11 book such as [Core Java Vol 2](https://www.amazon.com/gp/product/0135166314/ref=as_li_tl?ie=UTF8&tag=ewhome-20&camp=1789&creative=9325&linkCode=as2&creativeASIN=0135166314&linkId=3a9e15ad39246637aa07466b16c67293) or [Herbert Schildt](https://www.amazon.com/gp/product/1260440230/ref=as_li_tl?ie=UTF8&tag=ewhome-20&camp=1789&creative=9325&linkCode=as2&creativeASIN=1260440230&linkId=36bafe62c000a21fd49de29474044dc5)
  - [ ] Create and use private, default, and static methods of interfaces
  - [ ] Create functional interfaces 
  - [ ] Use lambda expressions with type inferencing ( See [this](https://www.baeldung.com/java-10-local-variable-type-inference) and (this)[https://www.baeldung.com/java-var-lambda-params] article. )
  - [ ] Migration to Modular Application - Section 3 of [The State of Module System](http://openjdk.java.net/projects/jigsaw/spec/sotms/#compatibility--migration) (Read carefully)
  - [ ] Modular services - Section 4 of [The State of Module System](http://openjdk.java.net/projects/jigsaw/spec/sotms/#services) (Read carefully)
  - [ ] Serialization - Read Chapters 1, 2, and 3 of [Serialization Spec](https://docs.oracle.com/javase/8/docs/platform/serialization/spec/serialTOC.html).
  - [ ] Security - Read Full [Secure Coding Guidelines](https://www.oracle.com/technetwork/java/seccodeguide-139067.html).
  - [ ] JDBC - Any book will do. Focus on PreparedStatement. Ignore RowSets etc. 
  - [ ] Formatting - Date formatting has two different methods. 
  Using the old java.text package and using the new java.time.DateTimeFormatter package.  
  Not clear which one they are focussing on but there are questions on java.time.DateTimeFormatter for sure. 
  Either way, go through the Predefined Formatters and Pattern strings given in [DateTimeFormatter API JavaDoc](https://docs.oracle.com/en/java/javase/11/docs/api/java.base/java/time/format/DateTimeFormatter.html).
  - [ ] Annotations - Sufficient to go through this [trail](https://docs.oracle.com/javase/tutorial/java/annotations/).
  
  
## Java SE 11 Programmer II [1Z0-816] Exam Objectives
To optimally prepare for the examination, it is crucial that you create your schedule around the objective guidelines provided by Oracle. The following enlists the primary examination objectives that you need to focus on to pass the examination.

Fundamentals of Java

Creating and using final classes
Creating and using nested, inner, and anonymous classes
Creating and using enumerations
Interfaces of Java

Creating and using interfaces with the default methods
Creating and using interfaces with private methods
Lambda Expressions and Functional Interfaces

Defining and writing functional interfaces
Creating and using lambda expressions with statement lambdas and lambda parameters
Built-in Functional Interfaces

Using interfaces from the java.util.function package
Using the core functional interfaces including Consumer, Predicate, Supplier, and Function
Using binary and primitive variations of the base interfaces of the java.util.function package.
Migrating to Modular Applications

Running modular applications on the modulepath and classpath
Using jdeps for identifying ways to address the cyclic dependencies and for determining dependencies
Migrating a Java-developed application with bottom-up and top-down migration approach
Concurrency

Writing a thread-safe code
Identifying threading-related problems such as livelocks and deadlocks.
I/O (NIO2 and Fundamentals)

Writing the console and file data using the I/O streams
Using the I/O streams to write and read files
Using the path interface for operating on the directory and file paths
Using the Stream APIs with the files
Using the Files class for copying, checking, and deleting a directory or file
Writing and reading objects using serialization
Database Applications with JDBC

Connecting to the databases using the DriverManager and JDBC URLs.
Using PreparedStatement for performing CRUD operations
Using CallableStatement and PreparedStatement APIs for performing database operations.
Annotations

Describing the purpose of typical usage patterns and annotations
Applying the annotations to methods and classes
Declaring custom annotations
Exception Handling and Assertions

Using the try-with-resources construct
Creating and using custom exception classes
Testing invariants by using assertions  

#OCP JAVA 11 CERTIFICATION 1Z0-819 EXAM EXPERIENCE
* Since the number of questions were so less (only 50), some topics were completely left out. Obviously, this doesn't mean that the exam doesn't have questions on those topics.
Specifically, the following things stood out in the exam:
  * Modules:
    * Only a couple of very basic conceptual questions.
    * No question on advanced topic such as services, migration strategies, command line options, module tools such as jdeps.
  * Security: Two code based questions on doPriviledged. No question on other topics. 
  * JDBC:
    * Only a couple of basic questions involving PreparedStatement.
    * No ResultSetMetaData
    * No DriverManager, transactions, savepoint questions.
  * Multithreading/Locking:
    * No question on Atomic classes
    * No question on locks
    * Couple of tough questions on ExecutorService
  * File I/O:
    * Simple question on methods of Files class involving options such as REPLACE_EXISTING.
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

* One question had 10, yes, 10, options! A couple of them had 7 or 8 options as well. Most had 4-5 though. 

* Only a few questions were very lengthy to read (they had a long problem statement). Most were not so much.

* Time was enough.
Overall the test did not seem too hard in terms of mind tricks but was hard in terms of depth of understanding required. You can't just read a topic cursorily and expect to answer exam questions on it. For example, the questions on enums and annotations requried that you know the complete ins and outs of how they work.
