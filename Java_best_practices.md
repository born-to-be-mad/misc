# TECHNIQUES FOR WRITING BETTER JAVA

## Avoid `valueOf` When Possible

Even though Java is a strongly-typed language, there are still ways to circumvent this type-checking.
One of the most common ways is the use of String objects to represent all data. For example, it is not uncommon to see the following JavaScript Object Notation (JSON) data sent as the body of a Representational State Transfer (REST) request or response:

```
{
    "name": "John Doe",
    "amount": "100"
}

{
    "name": "John Doe",
    "amount": "anything"
}


public class Account {
    private String name;
    private String amount;

    public long getAmountAsLong() {
        return Long.valueOf(amount);
    }
    // ...getters & setters...

}
```

Solution: not to use `Long.valueOf` but change our JSON to properly represent our intent:

```
{
    "name": "John Doe",
    "account": 100
}

public class Account {
    private String name;
    private long amount;

    public long getAmount() {
        return amount;
    }
    // ...getters & setters...

}
```

- There are cases where valueOf method calls (such as Long.valueOf) are required. If the JSON representation were out of our control, we would have no choice but to treat `amount` as a String. In this case, we should immediately convert `amount` to a long and ensure that all other classes interact with the value as a long, not a String.

```
public class AccountState {
    private String name;
    private String amount;

    // ...getters & setters...
}
public class Account {
    private String name;
    private long amount;

 public Account(AccountState state) {
        this.name = state.getName();
        this.amount = extractAmount(state.getAmount());
    }

    private static long extractAmount(String value) {
        try {
            return Long.valueOf(value);
        }
        catch (NumberFormatException e) {
            return 0;
        }
    }
    // ...getters & setters...
}
```

- when possible, we should avoid using `valueOf` methods that convert a String to some primitive value, including:
  ** Integer.valueOf
  ** Long.valueOf
  ** Float.valueOf
  ** Double.valueOf
  \*\* Boolean.valueOf
  Their inclusion in an application should be considered a code smell and is indicative that we have a String that should be represented by another data type.

## Avoid `instanceof` When Possible

The `instanceof` keyword provides an opportunity to circumvent the type-checking system of the Java compiler.
While there are cases (especially when working with low-level code or when using reflection) that `instanceof` may be necessary, it should be treated as a code smell. It is likely a sign hat we are skipping strict type-checking (and therefore losing the benefits of the Java type-checking system).

- In many cases, instanceof is used to safely convert an object of a known supertype into an object of the desired subtype (called downcasting). This downcasting is common when implementing the equals method in a custom class.

- An unchecked downcast occurs if we do not check for the implementation type of an object before casting that object to that type.

- In many cases, instanceof calls are used as an alternative to proper polymorphism.
- Although there may be a few specific cases where instanceof is necessary (such as implementing the equals method), in general, instanceof checks and unsafe downcasts should be avoided. We should instead use polymorphism to vary behavior based on the implementation type of an object.

## Throw Exceptions Early

When error checking must occur at runtime, it is best to throw exceptions as early as possible.
In large, complex environments where objects are instantiated in one thread and called in another, improper exception handling can cause debugging nightmares. In many cases, the results of improper exception handling can be subtle and insidious.

```

public class SecurityManagerStandard {
    private final SecurityTransactionRepository repo;

    public SecurityManager(SecurityTransactionRepository repo) {
        this.repo = repo;
    }

    public Optional<SecurityTransaction> findTransactionById(long id) {
        //return repo.findById(id); // NPE if repo is null

        //we have resolved the NPE issue, we have introduced a much more subtle problem that can come back to harm us.
        if (repo == null) {
           return Optional.empty();
        } else {
            return repo.findById(id);
        }
    }
}

public class SecurityManagerImproved {
    private final SecurityTransactionRepository repo;

    public SecurityManager(SecurityTransactionRepository repo) {
	     //even if an NPE get thrown, but this time, the exception originates from the constructor of the SecurityManager
         this.repo = Objects.requireNonNull(repo);
    }

    public Optional<SecurityTransaction> findTransactionById(long id) {
        return repo.findById(id);
    }
}
```

This concept of moving the null-check into the constructor is closely related to the concept of Design by Contract (DBC).
In this technique, every method has the following aspects:

- _Preconditions_: Things that must be true for the method to be called
- _Postconditions_: Things that must be true once the method completes execution
- _Invariants_: Things that must be true throughout the life of an object

_It is best to throw exceptions as soon as possible and at the point in which the error occurs_. Deferring an exception to a later point will muddle the debugging process and waste the time of developers trying to find the root cause of issues.

## Validate Arguments With Standard Methods

- validate the arguments at the assignment site and fail-fast if invalid arguments are supplied.
- Use the JDK standard null checking and index checking methods when possible. Bare in mind that the abstraction level of the exceptions thrown by the standard index checking methods may be inappropriate.
- Java Development Kit (JDK) 7 added a new class (called `Objects`) which includes the `requireNonNull` method that allows developers to check that an object is not null
  - requireNonNull(T obj)
  - requireNonNull(T obj, String message)
  - requireNonNull(T obj, Supplier<String> messageSupplier)
  - requireNonNullElse(T obj, T defaultObj)
  - requireNonNullElseGet(T obj, Supplier<? extends T> supplier)
- JDK 9
  - checkFromIndexSize(int fromIndex, int size, int length)
  - checkFromToIndex(int fromIndex, int toIndex, int length)
  - checkIndex(int index, int length)

## Get to Know the Object Class

- `Object` class has eleven methods that are inherited by all classes in the Java environment.
- overriding the equals method results in the following implementation structure:
  - Check if the supplied object is this object
  - Check if the supplied object has the same type as this object
  - Check if the fields of the supplied object are the same as the fields of this object
- `hashCode`
  - Hash codes are usually some ordered summation of the values of each field in an object
  - The number 31 was chosen because it is an odd prime. If it were even and the multiplication overflowed, information would be lost, because multiplication by 2 is equivalent to shifting. The advantage of using a prime is less clear, but it is traditional. A nice property of 31 is that the multiplication can be replaced by a shift and a subtraction for better performance on some architectures: 31 \* i = (i << 5) - i.
- In order to reduce the tediousness of implementing the hashCode method for a class with numerous fields, the `Objects` class includes a static method `hash` that allows for an arbitrary number of values to be hashed together
- Get to know the Object class: Every class inherits from it and the Java environment makes serious expectations for its methods. Be sure to follow these rules when overridding either equals or hashCode and be sure never to override one without overriding the other.

## Experiment With jshell

- a Read-Evaluate-Print Loop (REPL) tool called jshell was introduced since JDK 9
- Use `jshell` to evaulate the runtime behavior of a Java statement or groups of statements.
  - Taking a few seconds to see how a statement is actually evaluated can save value minutes or hours.

## Read Well-Written Code

- The JDK source code can be found lib/src.zip under a standard JDK installation
- Garner a great deal of information about how a particular class works by looking at its implementation
- Read as much code written by experienced Java developers as possible. Each developer has his or her own style, and each are human and can make poor choices, but on the whole, developers should emulate the code written by many of the original authors of Java and many of its most prolific practitioners.

## String Formatting

| Conversion | Category       | Description                                         |
| ---------- | -------------- | --------------------------------------------------- |
| %b, %B     | general        | true of false                                       |
| %h, %H     | general        | hash code value of the object                       |
| %s, %S     | general        | string                                              |
| %c, %C     | character      | unicode character                                   |
| %d         | integral       | decimal integer                                     |
| %o         | integral       | octal integer, base 8                               |
| %x, %X     | integral       | hexadecimal integer, base 16                        |
| %e, %E     | floating point | decimal number in scientific notation, 1.000000e+02 |
| %f         | floating point | decimal number                                      |
| %g,%G      | floating point | decimal number, rounding for the precision          |
| %a,%A      | floating point | hexadecimal floating-point, 0x1.4333333333333p3     |
| %t,%T      | date/time      | prefix for date and time conversion                 |
| %%         | percent        | display literal ‘%’                                 |
| %n         | line separator | new line, System.getProperty("line.separator")      |

Reorder the arguments with `%{index}${conversion}`:

- 1\$ – first argument
- %2\$ – second argument
- %3\$ – third argument
- %{index}\$ – {index} argument
