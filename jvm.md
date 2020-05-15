# HotSpot: interpretation and tiered compilation
_HotSpot_ is a method-based JIT
* L0(interpreter machine code templating)
* L1(C1:client, no profiling)
* L2(C1:client, simple profiling)
* L3(C1:client, advanced profiling)
* L4(C2:server, profile-based optimization)

#JVM tuning

## -Xmx and -XX:MaxMetaspaceSize
* `-Xmx` defines the maximum amount of heap size you are allocating to your application.
```java
-Xmx2g
```
* Metaspace is the region where JVM’s metadata definitions, such as class definitions, method definitions, will be stored. By default, the amount of memory that can be used to store this metadata information is unlimited (i.e. limited by your container or machine’s RAM size).
```java
-XX:MaxMetaspaceSize=256m
```

## GC Algorithm
There are 7 different GC algorithms in OpenJDK(March 2020):
* Serial GC
* Parallel GC
* Concurrent Mark and Sweep GC
* G1 GC
* Shenandoah GC
* Z GC (JVM 11+)
* Epsilon GC (JVM 11+)

If you don’t specify the GC algorithm explicitly, then JVM will choose the DEFAULT algorithm:
* Parallel GC - until Java 8
* G1 GC - since Java 9.

| GC Algorithm    | JVM argument  |
| --------- | ---------- | 
| Serial GC | -XX:+UseSerialGC |
| Parallel GC | -XX:+UseParallelGC |
| Concurrent Market & Sweep (CMS) GC | 	-XX:+UseConcMarkSweepGC |
| G1 GC | -XX:+UseG1GC |
| Shenandoah GC | 	-XX:+UseShenandoahGC |
| Z GC | -XX:+UseZGC |
| Epsilon GC | 	-XX:+UseEpsilonGC |

## Enable GC Logging
Garbage Collection logs contain information about Garbage Collection events, memory reclaimed, pause time duration, etc. 
Typically, GC logs are used for tuning garbage collection performance. 
* From JDK 1 to JDK 8 `-XX:+PrintGCDetails -XX:+PrintGCDateStamps -Xloggc:{file-path}`
```java
-XX:+PrintGCDetails -XX:+PrintGCDateStamps -Xloggc:/opt/workspace/myAppgc.log 
```
* From JDK 9 and above `-Xlog:gc* 7:file={file-path}`
```java
-Xlog:gc*:file=/opt/workspace/myAppgc.log
```

## -XX:+HeapDumpOnOutOfMemoryError, -XX:HeapDumpPath
The best practice is to capture the heap dump right at the moment or few moments before the application starts to experience OutOfMemoryError.
Capturing heap dumps can be automated by passing following JVM arguments:
```java
-XX:+HeapDumpOnOutOfMemoryError and -XX:HeapDumpPath={HEAP-DUMP-FILE-PATH}
```

In `-XX:HeapDumpPath` we specify the file path where heap dump should be stored. 
When you pass these two JVM arguments, heap dumps will be automatically captured and written to a defined file path, when OutOfMemoryError is thrown. 
 
## -Xss
* Each application will have a lot of threads. 
* Each thread will have its own stack. 
* In each thread’s stack following information are stored:
  * Methods/functions that are currently executed
  * Primitive datatypes
  * Variables
  * Object pointers
  * Return values

Each one of them consumes memory. 
If their consumption goes beyond a certain limit, then a _StackOverflowError_ is thrown. 

We can increase the thread’s stack size limit by passing the `-Xss` argument. 
```java
-Xss256k
```
If you set this `-Xss` value to a huge number, then memory will be blocked and wasted. 
(!) Threads are created outside of the heap (i.e. -Xmx), thus this value configured by `-Xss` * amount_of threads will be in addition to the -Xmx value you have already assigned. 
The best practice  is to start from a low value (say 256kb).

## -Dsun.net.client.defaultConnectTimeout and -Dsun.net.client.defaultReadTimeout
* Modern applications use numerous protocols (i.e. SOAP, REST, HTTP, HTTPS, JDBC, RMI, etc.) to connect with remote applications.
  Sometimes remote applications might take a long time to respond(even not respond at all).
If you don’t have proper timeout settings, and if remote applications don’t respond fast enough, then your application threads/resources will get stuck.

* You can pass these two powerful timeout networking properties at the JVM level that can be globally applicable to all protocol handlers that uses java.net.URLConnection:
  * `sun.net.client.defaultConnectTimeout` specifies the timeout (in milliseconds) to establish the connection to the host, f.e. HTTP connections, it is the timeout when establishing the connection to the HTTP server.
  * `sun.net.client.defaultReadTimeout` specifies the timeout (in milliseconds) when reading from the input stream when a connection is established to a resource.

(!) By default, values for these two properties are -1, which means no timeout is set. 

Example when both timeouts are set to 2 seconds:
```java
-Dsun.net.client.defaultConnectTimeout=2000 -Dsun.net.client.defaultReadTimeout=2000
```  

 
## -Duser.timeZone
* We can face with a problem if your application is running in a distributed environment.
  * application running across multiple data center and JVMs in each data center would exhibit different behaviors;
  * deploying application in cloud environment and etc.

It’s highly recommended to set the time zone at the JVM using the  `Duser.timezone` system property.   
```java
-Duser.timezone=US/Eastern
```
