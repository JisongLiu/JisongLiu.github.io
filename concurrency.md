### synchronized key word

- synchronized is based on instance level. If you use the synchronized to declare two methods in a class, you cannot access to
the two method in the thread simultaneously

### Basic thread method

- thread.start() // start the run method of that thread
- thread.join() // code will wait until this thread finished
- thread.setDaemon(true | false) // the thread will exit even when there is a Daemon thread
- thread.setUncaughtExceptionHandler() // set a handler for possible uncaught exception
- when you interrupt a thread, if its state is waiting / blocked -> stop it instantly OR set the interrupt flag as true and then stop it when we can do it

### ThreadLocal

```
// To implement the following thing, every thread stores: 
 Local.ThreadLocalMap
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

- using CopyOnWrite to avoid adding lock on read
- using lock-free to avoid adding the lock
- split the lock like hashmap -> split to different segment like readAndWriteLock
- narrow the range that is locked.

### Dead lock

- resource can only be used for one thread
- resource can not be freed if that thread don't agree
- A thread request a new resource while keep own of current one
- request and wait build a loop


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

### Timer

- schedule / cancel
- implemented way: based on heap; based on Hash Wheel Timer; multi-layer Hash Wheel Timer (hour, minute, second)

### State of thread

- RUNNABLE state: get the lock

- When thread calls wait it releases the current object lock (it keeps all locks from other objects) and than goes to WAITING state.

- When some other thread calls notify or notifyAll on that same object the first thread changes state from WAITING to BLOCKED, Notified thread does NOT automatically reacquire the lock or become RUNNABLE, in fact it must fight for the lock with all other blocked threads.

- WAITING and BLOCKED states both prevent thread from running, but they are very different.

- WAITING threads must be explicitly transformed to BLOCKED threads by a notify from some other thread. WAITING never goes directly to RUNNABLE.

### Lock free

```
class Counter {
	private AtomicInteger max = new AtomicInteger();
	// for loop; compareAndSet, if success, break; or loop || get a condition to break
	public void set(int value) { 
		//第一步循环
		for (;;) {
			int current = max.get(); 
			if (value > current) {
				//第二步CAS
				if (max.compareAndSet(current, value)) { 
					//第三步回退
					break;
				} else {
					continue;
				}
			} else { 
				break; 
			}
	￼￼	} 
	}
	//
	public int getMax() {
		return max.get();
	}
}
```

```
public class LinkedQueue <E> {
    private static class Node <E> {
        final E item;
        final AtomicReference<Node<E>> next;
        Node(E item, Node<E> next) {
            this.item = item;
            this.next = new AtomicReference<Node<E>>(next);
        }
    }
    private AtomicReference<Node<E>> head = new AtomicReference<Node<E>>(new Node<E>(null, null));
    private AtomicReference<Node<E>> tail = head;

    public boolean put(E item) {
        Node<E> newNode = new Node<E>(item, null);
        while (true) {
            Node<E> curTail = tail.get();
            Node<E> tailNext = curTail.next.get();
            if (curTail == tail.get()) {
                if (tailNext == null) { // 看到的是静止状态
                    if (curTail.next.compareAndSet(null, newNode)) {    // A 的第一个CAS
                        tail.compareAndSet(curTail, newNode) ;  // A 的第二个CAS，不用判断结果，因为如果失败了，说明B（或其他线程）帮它完成了这个动作
                        return true;
                    }
                } else {            // 看到中间状态
                    tail.compareAndSet(curTail, tailNext);  // B 帮 A 完成第二个更新动作
                }
            }
        }
    }
}
```

### Volatile

- the variable will not cached in the local thread, all the operation will have the direct influence on the main heap part
- we should use volatile when an variable is used in many places and it is written in some places.
