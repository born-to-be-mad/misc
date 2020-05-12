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
* Epsilon GC

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

## -Duser.timeZone
```java
-Duser.timezone=US/Eastern
```
