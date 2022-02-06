# JDK Binaries
All of them are located in `jdk/bin` folder:
* `jps` find running JVM process IDs, like `ps aux | grep java`
* `javap <class_file>` disassembling Java class file
* `jmap -heap <process_id>` print summary of JVM's process's memory space
   * `jmap -dum:live,format=b,file=heap.bin PID` to create heap dump
   * `jmap -histo PID` allows quickly collect histogram data.
   * offline heap dump by using core dump:
  ```
  sudo gcore 1234
  jmap -dump:format=b,file=heap.bin /path/to/java core.1234
  ```
  * automatic heap dumps:
    * `-XX+HeapDumpOnOutOfMemoryError` JVM flag
    * `-XX+HeapDumpBeforeFullGC` JVM flag
    * `-XX+HeapDumpAfterFullGC` JVM flag
  * kill JVM after heap dump
    * `-XX:ExitOnOutOfMemoryError`
    * `-XX:CrashOnOutOfMemoryError`
* `jhat <dump_file>` take a generated head dump file and run a local web server
* `jinfo <process_id` see all system properties and command-line flags of a running JVM

# Monitoring Tools
* jconsole - graphical console to monitor and manage Java apps
* jps - experimental:  list of instrumented JVMs on the target system
* jstat - experimental: monitors JMV statistics
* jstatd - experimental: monitors JVMs and enables remote monitoring tool to attach to JVM
* jmc - Java Mission Control

# JVM Profiling Tool
APM(Application Performance Monitoring) is the practice of tracking key software application performance metrics using monitoring software and telemetry data. It is used to ensure system availability, optimize service performance and response times, and improve user experiences.
* `VisualVM` - bundled with JDK(through Java 8), then available as stand-alone(https://visualvm.github.io)
* `Java Flight Recorder` - a component of JDK Mission Control, is a handy utility fo event capturing and visualization.
  * openjdk.java.net/projects/jmc
  * www.oracle.com/java/technologies/jdk-mission.control.html
* `Glowrot` is a light-weight open-source and easy-to-run Java APM with transaction reporting and instrumentation capabilities.
  * https://glowroot.org
  * requires Java-agent VM parameter
* `Prometheus` is an open-source easy-to-run Java APM which cna easily capture Spring Boot metrics over time
  * https://prometheus.io/download
  * requires configuration file

# Troubleshooting Commands
A list of common commands used during the troubleshooting process is mentioned below. 
Please check the syntax during the execution.

### Thread Count  
`cat /proc/<pid>/status | grep Threads`

`ps uH p <pid>`

### Heap Configuration
`java -XX:+PrintFlagsFinal -version | grep HeapSize`

### Thread Dump
`jstack <<pid>>` [Take Thread dumps in some interval say 15 secs for 1 min]

### Thread Stack Size
`java -XX:+PrintFlagsFinal -version | grep ThreadStackSize`

### Others
`pmap –x <<pid>>`

`top`

`nestat -a | grep <<port number>>`

`kill -9 <<pid>>`

`kill -3 <<pid>>`

`ps –ef| grep –i java`

`/bin/jstat –gc <pid>`

`jstat -gc <pid> | tail -l | awk '(split($0,a," "); sum=a[3]+a[4]+a[6]+a[8];`
`print sum " Kb")'`

`/bin/jmap –heap <pid>`
