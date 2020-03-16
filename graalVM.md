# GraalVM

_GraalVM_ is a universal virtual machine for running applications written in JavaScript, Python, Ruby, R, JVM-based languages like Java, Scala, Kotlin, Clojure, and LLVM-based languages such as C and C++.

_GraalVM_ removes the isolation between programming languages and enables interoperability in a shared runtime.

- GraalVM Native Image allows you to ahead-of-time compile Java code to a standalone executable, called a _native image_.
  - _native-image_ is a utility that processes all the classes of your application and their dependencies, including those from the JDK. It statically analyses these classes to determine which classes and methods are reachable and used during application execution. Then, it passes all this reachable code as the input to the GraalVM compiler, which _ahead-of-time_(AOT) compiles it to the native binary. In simple words it converts a bytecode that runs on the JVM (on any platform) to native code for a specific OS/platform — which is where the performance comes from.

The key benefits of AOT compiling Java application to a native binary are:

- Speed of startup
- Reduced memory footprint

## How to use _GraalVM_?

- GraalVM is similar to any Java SDK (JDK) that we download from any vendor, except that it has JVMCI: Java-level JVM Compiler Interface support, and Graal is the default JIT compiler.
  [Oracle GraalVM](https://www.oracle.com/downloads/graalvm-downloads.html)

### GraalVM SDK structure

- GraalVM SDK is semantically similar to the traditional Java SDKs. A few items that look interesting in the list are `Rscript`, `lli`, and `ployglot`.

- Each of the sub-folders in `examples` contains examples for the respective languages supported by the GraalVM, including `embed` and `native-image`.

### Multiple language example

- Go to `/examples/embed` and create `HelloPolyglotWorld.java`

```

import org.graalvm.polyglot.*;
public class HelloPolyglotWorld {
    public static void main(String[] args) throws Exception {
        System.out.println("Hello polyglot world Java!");
        Context context = Context.create();
        context.eval("js", "print('Hello polyglot world JavaScript!');");
        context.eval("ruby", "puts 'Hello polyglot world Ruby!'");
        context.eval("R", "print('Hello polyglot world R!');");
        context.eval("python", "print('Hello polyglot world Python!');");
    }
}
```

- compile `$GRAAL_HOME/bin/javac HelloPolyglotWorld.java`
- run `$GRAAL_HOME/bin/java HelloPolyglotWorld`
  - results
  ```
    Hello polyglot world Java!
    Hello polyglot world JavaScript!
    Hello polyglot world Ruby!
    [1] "Hello polyglot world R!"
    Hello polyglot world Python!
  ```

### Native image

- go to `/native-image` of graalVM SDK
- create `HelloWorld.java'
  ```
    public class HelloWorld {
        public static void main(String[] args) {
            System.out.println("Hello, World!");
        }
    }
  ```
- compile into bytecode `$GRAAL_HOME/bin/javac HelloWorld.java`
- compile the bytecode (HelloWorld.class) into native code `$GRAAL_HOME/bin/native-image HelloWorld`
  - result `helloworld` - the native binary that runs on the platform we compiled it on using native-image command
- execute `helloworld` native binary
