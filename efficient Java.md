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

### item 21: Use function object store present strategies

- declare an interface to represent the strategy, 
- a class that implements this interface for each concrete strategy. 
       - if it is used only once, it is typically declared and instantiated as an anonymous class. 
       - if it is designed for repeated use, it is generally implemented as a private static member class and exported in a public static final field whose type is the strategy interface.
       
```
        class Host {
       private static class StrLenCmp
               implements Comparator<String>, Serializable {
           public int compare(String s1, String s2) {
               return s1.length() - s2.length();
           }
}
       // Returned comparator is serializable
       public static final Comparator<String>
           STRING_LENGTH_COMPARATOR = new StrLenCmp();
       ...  // Bulk of class omitted
   }
   ```
       
### item 22: If you declare a member class that does not require access to an enclosing instance, always put the static modifier in its declaration

### item 23: Declare the parameter rather than using the raw type

- you lose type safety if you use a raw type like List, but not if you use a parameterized type like List<Object>
- The object is better than raw itself because you will get the error during the complier period not run time

### item 25:Prefer list to array

- List<Object> ol = new ArrayList<Long>(); // Incompatible types BUT Object[] objectArray = new Long[1]; will be correct. In other words, List<T> will be only assigned the type T.
  
### item 26: Favor generic types
- it will helps you to parameterize your function

```
public <T> T[] arrays(T[] a) {      }

class BlockingQueue<E> {
}

class DelayQueue<E extends Delayed> implements BlockingQueue<E>;

```

- For maximum flexibility, use wildcard types on input parameters that represent producers or consumers. 
       - producer-extends, consumer-super.
       - public void popAll(Collection<? super E> dst)
       - public void pushAll(Iterable<? extends E> src)
     
     
     
### item 29: Considertypesafeheterogeneouscontainers

```
// Typesafe heterogeneous container pattern - implementation
public class Favorites {
private Map<Class<?>, Object> favorites =
           new HashMap<Class<?>, Object>();
       public <T> void putFavorite(Class<T> type, T instance) {
           if (type == null)
               throw new NullPointerException("Type is null");
           favorites.put(type, instance);
}
public <T> T getFavorite(Class<T> type) { return type.cast(favorites.get(type));
} }

```

### item 30: use enum instead of int constant

### item 32: Use Enum Set instead of bit fields (in a class)

```
public enum Style { BOLD, ITALIC, UNDERLINE, STRIKETHROUGH }
text.applyStyles(EnumSet.of(Style.BOLD, Style.ITALIC));
```

### item 33: Use EnumMap instead of ordinal indexing

- Passed (useful but not useful for now...)

### item 34: Emulate extensible enums with interfaces 

```
public interface Operation {
       double apply(double x, double y);
}
public enum BasicOperation  implements Operation {
       PLUS("+") {
public double apply(double x, double y) { return x + y; } }, // you can put some logic function here
MINUS("-") {
public double apply(double x, double y) { return x - y; }
       },
       TIMES("*") {
public double apply(double x, double y) { return x * y; } },
DIVIDE("/") {
public double apply(double x, double y) { return x / y; }
};
```
### item35 Prefer annotations to naming patterns

- E.g.: the naming patterns: you have to start with test if you write a code with Junit, which is naming patterns

### Item36: Consistently use the Override annotation

### Item37: Use marker interfaces to define types

- marker here is like Serializable

### item 38 - 40: tips for method:

- always check the parameters for validity
- it is essential to make a defensive copy of each mutable parameter to the constructor (because it is referrence)
- For parameter types, favor interfaces over classes (Map<> -> you can pass HashMap or HashTable)
- Prefer two-element enum types to boolean parameters (it makes your code more readable and extendable)



