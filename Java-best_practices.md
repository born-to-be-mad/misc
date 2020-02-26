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

* There are cases where valueOf method calls (such as Long.valueOf) are required. If the JSON representation were out of our control, we would have no choice but to treat `amount` as a String. In this case, we should immediately convert `amount` to a long and ensure that all other classes interact with the value as a long, not a String. 
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

* when possible, we should avoid using `valueOf` methods that convert a String to some primitive value, including:
** Integer.valueOf
** Long.valueOf
** Float.valueOf
** Double.valueOf
** Boolean.valueOf
Their inclusion in an application should be considered a code smell and is indicative that we have a String that should be represented by another data type.

## Avoid `instanceof` When Possible
The `instanceof` keyword provides an opportunity to circumvent the type-checking system of the Java compiler. 
While there are cases (especially when working with low-level code or when using reflection) that `instanceof` may be necessary, it should be treated as a code smell. It is likely a sign hat we are skipping strict type-checking (and therefore losing the benefits of the Java type-checking system).

* In many cases, instanceof is used to safely convert an object of a known supertype into an object of the desired subtype (called downcasting). This downcasting is common when implementing the equals method in a custom class.

*  An unchecked downcast occurs if we do not check for the implementation type of an object before casting that object to that type.

* In many cases, instanceof calls are used as an alternative to proper polymorphism.
* Although there may be a few specific cases where instanceof is necessary (such as implementing the equals method), in general, instanceof checks and unsafe downcasts should be avoided. We should instead use polymorphism to vary behavior based on the implementation type of an object.

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
* _Preconditions_: Things that must be true for the method to be called
* _Postconditions_: Things that must be true once the method completes execution
* _Invariants_: Things that must be true throughout the life of an object

_It is best to throw exceptions as soon as possible and at the point in which the error occurs_. Deferring an exception to a later point will muddle the debugging process and waste the time of developers trying to find the root cause of issues. 