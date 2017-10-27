### synchronized key word

- synchronized is based on instance level. If you use the synchronized to declare two methods in a class, you cannot access to
the two method in the thread simultaneously


### ThreadLocal

```
// To implement the following thing, every thread stores: ThreadLocal.ThreadLocalMap
private static final ThreadLocal<DateFormat> threadLocalDateFormat
            = new ThreadLocal<>();
// Soft reference will delete only when memory is not enough
private static final ThreadLocal<SoftReference<DateFormat>> threadLocalDateFormat
            = new ThreadLocal<>();
// Weak reference will delete instantly if there is not strong reference
private static final ThreadLocal<WeakReference<DateFormat>> threadLocalDateFormat
            = new ThreadLocal<>();
```

###
