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
