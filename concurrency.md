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

### The principle of lock

- If possible, use a specific lock (like read and write lock) rather than a specific lock
- Lock a block as small as possible. If two part can be executed in the same time, use different lock for these parts


### Concurreny class in Java

#### ConcurrentHashMap

- It is locked for specific segment rather than the whole data structure (difference from hashtable)

#### CopyOnWriteArrayList 

- the object always read only
- if you want to update it, build a snapshot of it, update that snapshot, then let this object refer to this snapshot and discard the original one
- read is not locked. Used for the case where >90% request is read

#### BlockingQueue (interface)

- implemented: 
            - ArrayBlockingQueue // need to assign the size
            - LinkedBlockingQueue // differ from ConcurrentLinkedQueue which is lock-free

- Throw exception: remove(), add();
- Return specific value: offer(), poll()
- Block all the time: put(), take();
- Block for a time-out: offer(e, time, unit), poll(time, unit);
```
 class Producer implements Runnable {
   private final BlockingQueue queue;
   Producer(BlockingQueue q) { queue = q; }
   public void run() {
     try {
       while (true) { queue.put(produce()); }
     } catch (InterruptedException ex) { ... handle ...}
   }
   Object produce() { ... }
 }

 class Consumer implements Runnable {
   private final BlockingQueue queue;
   Consumer(BlockingQueue q) { queue = q; }
   public void run() {
     try {
       while (true) { consume(queue.take()); }
     } catch (InterruptedException ex) { ... handle ...}
   }
   void consume(Object x) { ... }
 }

 class Setup {
   void main() {
     BlockingQueue q = new SomeQueueImplementation();
     Producer p = new Producer(q);
     Consumer c1 = new Consumer(q);
     Consumer c2 = new Consumer(q);
     new Thread(p).start();
     new Thread(c1).start();
     new Thread(c2).start();
   }
 }
```

### race condition

- The final result is related to the order we execute several operations
- using synchronized block to avoid it


### Using condition in coding
- await()
- signal()
- signalAll()
```
class BoundedBuffer {
   final Lock lock = new ReentrantLock();
   final Condition notFull  = lock.newCondition(); 
   final Condition notEmpty = lock.newCondition(); 

   final Object[] items = new Object[100];
   int putptr, takeptr, count;

   public void put(Object x) throws InterruptedException {
     lock.lock();
     try {
       while (count == items.length)
         notFull.await();
       items[putptr] = x;
       if (++putptr == items.length) putptr = 0;
       ++count;
       notEmpty.signal();
     } finally {
       lock.unlock();
     }
   }

   public Object take() throws InterruptedException {
     lock.lock();
     try {
       while (count == 0)
         notEmpty.await();
       Object x = items[takeptr];
       if (++takeptr == items.length) takeptr = 0;
       --count;
       notFull.signal();
       return x;
     } finally {
       lock.unlock();
     }
   }
 }
```



