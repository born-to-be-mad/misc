# Effective Java by Joshua Bloch 
* Static factory methods, unlike constructors, 
  * have names
  * are not required to create a new object each time they’re invoked.
  * can return an object of any subtype of their return type
  * the class of the returned object can vary from call to call as a function of the input parameters
  * the returned object need not exist when the class containing the method is written
* common names for static factory methods
  * `from`
  * `of`
  * `valuuOf`
  * `instance` or `getInstance`
  * `create` or `newInstance`
  * `getType`
  * `newType`
  * `type`
* JavaBeans pattern precludes the possibility of making a class immutable 
* The Builder pattern simulates named optional parameters, and it is well suited to class hierarchies
* The Builder pattern is a good choice when designing classes whose constructors or static factories would have more than a handful of parameters
* Making a class a singleton can make it difficult to test its clients
* A single-element enum type is often the best way to implement a singleton
* A class can be made non-instantiable by including a private constructor
* Prefer primitives to boxed primitives, and watch out for unintentional autoboxing.
* Nulling out object references should be the exception rather than the norm.
* Finalizers are unpredictable, often dangerous, and generally unnecessary.
* Cleaners are less dangerous than finalizers, but still unpredictable, slow, and generally unnecessary.
* Never depend on a finalizer or cleaner to update persistent state
* To protect non-final classes from finalizer attacks, write a final finalize method that does nothing
* Prefer `try-with-resources` to `try-finally`
* Once you’ve violated the equals contract, you simply don’t know how other objects will behave when confronted with your object.
* Always override `hashCode` when you override `equals`
* Use the == operator to check if the argument is a reference to this object.
* Use the instanceof operator to check if the argument has the correct type.
* Cast the argument to the correct type.
* For each “significant” field in the class, check if that field of the argument matches the corresponding field of this object
* Do not be tempted to exclude significant fields from the hash code computation to improve performance
* Don’t provide a detailed specification for the value returned by hashCode, so clients can’t reasonably depend on it; this gives you the flexibility to change it
* Always override `toString`. It should return all of the interesting information contained in the object
* Immutable classes should never provide a clone method
* Use of the relational operators < and > in compareTo methods is verbose and error-prone and no longer recommended
* Make each class or member as inaccessible as possible
* Instance fields of public classes should rarely be public
* If a class is package-private or is a private nested class, there is nothing inherently wrong with exposing its data fields
* Immutable objects are inherently thread-safe; they require no synchronization.
* Classes should be immutable unless there’s a very good reason to make them mutable.
* If a class cannot be made immutable, limit its mutability as much as possible.
* The major disadvantage of immutable classes is that they require a separate object for each distinct value. 
* The class must document its self-use of overridable methods
* You must test your class by writing subclasses before you release it.
* Constructors must not invoke overridable methods, directly or indirectly.
