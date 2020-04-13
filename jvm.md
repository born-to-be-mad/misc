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
* Z GC
* Epsilon GC

If you don’t specify the GC algorithm explicitly, then JVM will choose the default algorithm:
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

## -Xss

## -Dsun.net.client.defaultConnectTimeout and -Dsun.net.client.defaultReadTimeout

## -Duser.timeZone
```java
-Duser.timezone=US/Eastern
```