### item 1 Consider static factory methods instead of constructor
pros: 
- 1. It helps make the client's code more readable 
- 2. Unlike constructors, they are not required to create a new instance 
everytime, you can define your own cache policy 
- 3. Shorten the length ( Map<String, List<String>> m = new HashMap<String, List<String>>();
v.s. Map<String, List<String>> m = HashMap.newInstance();) 
- 4. The return value could be any subtype of the given class which help the polymorphism

### item 2 Use the builder pattern if you meet too much parameter

### item 3 Enfore the singleton property with a private constructor or an enum type 

```
public enum Elvis {
       INSTANCE;
       public
```

### item 4 Make a class noninstantiability using a private constructor method

### item 5 Reuse an instance if it is immutable. E.g. using static key word or String = "Not do it like new String()". If
you can use primitive never use boxed primitive

### item 6 pay attention on the memory leak. Nulling out a reference if this element isn't used; set proper cache policy;
if registered as a listener, never forget to deregister it

### item 7 instead of using finalizer, using terminate() method in finally() block. 

- a class with Finalizer will become slow
- Never do time-critical things in finalizer because it has some latency.

### item 8 - 10 how to override

- If you override an equal method, keep transitive, reflexive, symmetric, consistent
- Always override hashcode when you override the equal method
- Always override the toString() to help we can print the valuable fields of an instance.

### item 11 passed

### item 12 compareTo() -- Comparable interface

- consistent
- compareTo(x, y) == - compareTo(y, x) symmetric
- compareTo(x, x) == 0 reflexive
- compareTo(x, y) == 0 => sign is the same for compareTo(y, z) a 
nd compareTo(x, z) transitive
- compareTo(x, y) > 0 and compareTo(y, z) > 0 => compareTo(x, z) > 0 transitive

### item 13 - 15 Minimize the accessibility of classes and members

- Instance fields should never be public. Because in this case, you give up the ability to limit the values stored in that field and give up taking any action when the field is modified. All in all, you will lose the fexilibity. (public classes should never expose mutable fields)
- It is wrong for a class to have a public static final array field, or an accessor that return that field.
 - make it private and expose it as a unmodified public field
 - getter return a copy of that field
- If one variable could be immutable, declare it as immutable. It could be shared freely and thread-safe.

### item 16 - 17 Favor composition over inheritance

- Unlike method invocation, inheriotance violates encapsulation.
- Therefore, the class must document its self-use of overridable methods.

### item 18 passed

### item 19 how to use the utility class 

- import static java.lang.Math.*; // it will import all the static function under Math

### item20: Prefer class hierarchies to tagged classes

- E.g.: a class has a enum Shape (square, rectangular) -> subclass square / rectangular

### item 21: Usefunctionobjectstorepresentstrategies





