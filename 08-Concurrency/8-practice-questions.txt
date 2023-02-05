1. What is the output of the following code snippet?
    Callable c = new Callable() {
        public Object run() {
            System.out.print("X");
            return 10;
        }
    };
    var s = Executors.newScheduledThreadPool(1);
    for(int i=0; i<10; i++) {
        Future f = s.submit(c);
        f.get();
    }
    s.shutdown();
    System.out.print("Done!");

    A. XXXXXXXXXXDone!
    B. Done!XXXXXXXXXX
    C. The code does not compile.
    D. The code hangs indefinitely at runtime.
    E. The code throws an exception at runtime.
    F. The output cannot be determined ahead of time.

    Explanation :
    C. The code does not compile because Callable must define a call() method, not a run() method, so option C is the correct answer. 
    If the code was fixed to use the correct method name, then it would complete without issue, printing XXXXXXXXXXDone! at runtime. 
    The f.get() call will block and wait for the results before moving on to the next iteration of the for loop.

2. Which of the following methods is not available on an ExecutorService instance?
    (Choose two.)

    A. execute(Callable)
    B. shutdownNow()
    C. submit(Runnable)
    D. exit()
    E. submit(Callable)
    F. execute(Runnable)

    Explanation :
    A,D. Option A is correct, as ExecutorService does not define nor inherit an overloaded method execute() that takes a Callable parameter. 
    ExecutorService defines two shutdown methods, shutdown() and shutdownNow(), one of which is shown in option B. 
    Option D is correct, as exit() does not exist and is not one of shutdown methods. 
    The ExecutorService interface defines the two submit() methods shown in options C and E. 
    Because ExecutorService extends Executor, it also inherits the execute(Runnable) method presented in option F.

3. The following program simulates flipping a coin an even number of times. Assuming five
    seconds is enough time for all of the tasks to finish, what is the output of the following
    application?
    import java.util.concurrent.*;
    import java.util.concurrent.atomic.*;
    public class Luck {
        private AtomicBoolean coin = new AtomicBoolean(false);
        void flip() {
            coin.getAndSet(!coin.get());
        }
        public static void main(String[] gamble) throws Exception {
            var luck = new Luck();
            ExecutorService s = Executors.newCachedThreadPool();
            for(int i=0; i<1000; i++) {
                s.execute(() -> luck.flip());
            }
            s.shutdown();
            Thread.sleep(5000);
            System.out.println(luck.coin.get());
        } 
    }

    A. false
    B. true
    C. The code does not compile.
    D. The code hangs indefinitely at runtime.
    E. The code throws an exception at runtime.
    F. The output cannot be determined ahead of time.

    Explanation :
    F. The code compiles and runs without issue. Even though the thread-safe AtomicBoolean is used, it is not used in a thread-safe manner. 
    The flip() method first retrieves the alue and then sets a new value. 
    These two calls are not executed together in an atomic or synchronized manner. 
    For this reason, the output could be true or false, with one or more of the flips possibly being lost, and making option F correct.

4. Which of the following is a recommended way to define an asynchronous task?

    A. Create a Callable expression and pass it to an instance of an Executor.
    B. Create a class that extends Thread and override the start() method.
    C. Create a Runnable lambda expression and pass it to a Thread constructor.
    D. Create an anonymous Runnable class that overrides the begin() method.
    E. All of the above.

    Explanation :
    C. Option A is incorrect, although it would be correct if Executor were replaced with ExecutorService. 
    Option B is also incorrect, but it would be correct if start() were replaced with run(). 
    Option C is correct and is a common way to define an asynchronous task using a lambda expression. 
    Option D is incorrect, as Runnable does not inherit a begin() method.

5. Given the following program, how many times is Locked! expected to be printed? Assume
    100 milliseconds is enough time for each task created by the program to complete.
    import java.util.concurrent.locks.*;
    public class Padlock {
        private Lock lock = new ReentrantLock();
        public void lockUp() {
            if (lock.tryLock()) {
                lock.lock();
                System.out.println("Locked!");
                lock.unlock();
            }
        }
        public static void main(String... unused) throws Exception {
            var gate = new Padlock();
            for(int i=0; i<5; i++) {
                new Thread(() -> gate.lockUp()).start();
                Thread.sleep(100);
            }
        } 
    }

    A. One time.
    B. Five times.
    C. The code does not compile.
    D. The code hangs indefinitely at runtime.
    E. The code throws an exception at runtime.
    F. The output cannot be determined ahead of time.

    Explanation :
    A. If the tryLock() method returns true, then a lock is acquired that must be released. That means the lockUp() method actually contains two calls to lock the object and only one call to unlock it. 
    For this reason, the first thread to reach tryLock() obtains a lock that is never released. 
    For this reason, Locked! is printed only once, and option A is correct. 
    If the call to lock() inside the if statement was removed, then the expected output would be to print the statement five times.
        
6. Given the original array, how many of the following for statements result in an exception at
    runtime, assuming each is executed independently?
    var original = List.of(1,2,3,4,5);

    var copy1 = new CopyOnWriteArrayList<Integer>(original);
    for(Integer w : copy1)
        copy1.remove(w);

    var copy2 = Collections.synchronizedList(original);
    for(Integer w : copy2)
        copy2.remove(w);

    var copy3 = new ArrayList<Integer>(original);
    for(Integer w : copy3)
        copy3.remove(w);

    var copy4 = new ConcurrentLinkedQueue<Integer>(original);
    for(Integer w : copy4)
        copy4.remove(w);

    A. Zero.
    B. One.
    C. Two.
    D. Three.
    E. Four.
    F. The code does not compile.

    Explanation :
    C. CopyOnWriteArrayList makes a copy of the array every time it is modified, preserving the original list of values the iterator is using, even as the array is modified. 
    For this reason, the for loop using copy1 does not throw an exception at runtime. 
    On the other hand, the for loops using copy2 and copy3 both throw ConcurrentModificationException at runtime since neither allows modification while they are being iterated upon. 
    Finally, the ConcurrentLinkedQueue used in copy4 completes without throwing an exception at runtime. 
    For the exam, remember that the Concurrent classes order read/write access such that access to the class is consistent across all threads and processes, while the synchronized classes do not. 
    Because exactly two of the for statements produce exceptions at runtime, option C is the correct answer

7. Fill in the blanks: ______________ is a special case of ______________, in which two or more
    active threads try to acquire the same set of locks and are repeatedly unsuccessful.

    A. Deadlock, livelock
    B. Deadlock, resource starvation
    C. Livelock, resource starvation
    D. Resource starvation, race conditions
    E. Resource starvation, livelock
    F. None of the above

    Explanation :
    C. Resource starvation is when a single active thread is perpetually unable to gain access to a shared resource. 
    Livelock is a special case of resource starvation, in which two or more active threads are unable to gain access to shared resources, repeating the process over and over again. 
    For these reasons, option C is the correct answer. 
    Deadlock and livelock are similar, although in a deadlock situation the threads are stuck waiting, rather than being active or performing any work. 
    Finally, a race condition is an undesirable result when two tasks that should be completed sequentially are completed at the same time.

8. What is the output of the following application?
    3: public class TpsReport {
    4:      public void submitReports() {
    5:          var s = Executors.newCachedThreadPool();
    6:          Future bosses = s.submit(() -> System.out.print("1"));
    7:          s.shutdown();
    8:          System.out.print(bosses.get());
    9:      }
    10:     public static void main(String[] memo) {
    11:         new TpsReport().submitReports();
    12:     }
    13: }

    A. null
    B. 1null
    C. 1
    D. Line 6 does not compile.
    E. Line 8 does not compile.
    F. An exception is thrown at runtime.

    Explanation :
    E. The class does not compile because the Future.get() on line 8 throws a checked InterruptedException and a checked ExecutionException, neither of which is handled nor declared by the submitReports() method. 
    If the submitReports() and accompanying main() methods were both updated to declare these exceptions, then the application would print 1null at runtime. 
    For the exam, remember that Future can be used with Runnable lambda expressions that do not have a return value but that the return value is always null when completed.

9. Which of the following static methods does not exist in the Executors class? (Choose two.)
    A. newFixedScheduledThreadPool()
    B. newThreadPool()
    C. newFixedThreadPool(int)
    D. newSingleThreadExecutor()
    E. newScheduledThreadPool(int)
    F. newSingleThreadScheduledExecutor()

    Explanation :
    A,B. Options C, D, E, and F are all proper ways to obtain instances of ExecutorService. 
    Remember that newSingleThreadExecutor() is equivalent to calling newFixedThreadPool(int) with a value of 1. 
    The correct answers are options A and B, as neither of these methods exist.

10. How many times does the following application print Ready at runtime?
    package parade;
    import java.util.concurrent.*;
    public class CartoonCat {
        private void await(CyclicBarrier c) {
            try {
                c.await();
            } catch (Exception e) {}
        }
        public void march(CyclicBarrier c) {
            var s = Executors.newSingleThreadExecutor();
            for(int i=0; i<12; i++)
                s.execute(() -> await(c));
            s.shutdown();
        }
        public static void main(String... strings) {
            new CartoonCat().march(new CyclicBarrier(4,
                () -> System.out.println("Ready")));
        }
    }

    A. Zero.
    B. One.
    C. Three.
    D. The code does not compile.
    E. An exception is thrown at runtime.

    Explanation :
    A. The code compiles without issue but hangs indefinitely at runtime. 
    The application defines a thread executor with a single thread and 12 submitted tasks. 
    Because only one thread is available to work at a time, the first thread will wait endlessly on the call to await(). 
    Since the CyclicBarrier requires four threads to release it, the application waits endlessly in a frozen condition. 
    Since the barrier is never reached and the code hangs, the application will never output Ready, making option A the correct answer. 
    If newCachedThreadPool() had been used instead of newSingleThreadExecutor(), then the barrier would be reached three times, 
    and option C would be the correct answer.

11. Let’s say you needed a thread executor to create tasks for a CyclicBarrier that has a barrier
    limit of five threads. Which static method in ExecutorService should you use to obtain it?

    A. newSingleThreadExecutor()
    B. newSingleThreadScheduledExecutor()
    C. newCachedThreadPool()
    D. newFixedThreadPool(2)
    E. None of the above

    Explanation :
    E. Trick question! ExecutorService does not contain any of these methods. 
    To obtain an instance of a thread executor, you need to use the Executors factory class. 
    For this reason, option E is the correct answer. 
    If the question had instead asked which Executors method to use, then the correct answer would be option C. 
    Options A, B, and D do not create enough threads for a CyclicBarrier expecting to reach a limit of five concurrent threads. 
    Option C, on the other hand, will create threads as needed and is appropriate for use with a CyclicBarrier.

12. The following diagrams represent the order of read/write operations of two threads sharing
    a common variable. Each thread first reads the value of the variable from memory and then
    writes a new value of the variable back to memory. Which diagram demonstrates proper
    synchronization?

    A. 
    ______________
    |  Thread 1  |
    ______________
     ^          |
     |          V
   __________________
    | Shared Memory |
   __________________
        |    ^
        V    |
    ______________
    | Thread 2   |
    ______________
    -------------->
         Time 

    B. 
    ______________
    |  Thread 1  |
    ______________
        ^       |
        |       V
   __________________
    | Shared Memory |
   __________________
      |      ^
      V      |
    ______________
    | Thread 2   |
    ______________
    -------------->
         Time 

    C. 
    ______________
    |  Thread 1  |
    ______________
           ^   |
           |   V
   __________________
    | Shared Memory |
   __________________
      |   ^
      V   |
    ______________
    | Thread 2   |
    ______________
    -------------->
         Time 

    D. 
    ______________
    |  Thread 1  |
    ______________
      ^      |
      |      V
   __________________
    | Shared Memory |
   __________________
         |      ^
         V      |
    ______________
    | Thread 2   |
    ______________
    -------------->
         Time 

    Explanation :
    C. Part of synchronizing access to a variable is ensuring that read/write operations are atomic or happen without interruption. 
    For example, an increment operation requires reading a value and then immediately writing it. 
    If any thread interrupts this process, then data could be lost. 
    In this regard, option C shows proper synchronized access. 
    Thread 2 reads a value and then writes it without interruption. 
    Thread 1 then reads the new value and writes it. 
    The rest of the answers are incorrect because one thread writes data to the variable in-between another thread reading and writing to the same variable. 
    Because a thread is writing data to a variable that has already been written to by another thread, it may set invalid data. 
    For example, two increment operations running at the same time could result in one of the increment operations being lost

13. What is the output of the following application?
    import java.util.*;
    import java.util.concurrent.*;
    public class Race {
        ExecutorService service = Executors.newFixedThreadPool(8);
        public static int sleep() {
            try { Thread.sleep(1000); } catch (Exception e) {}
            return 1;
        }
        public void hare() {
            try {
                Callable<Integer> c = () -> sleep();
                final var r = List.of(c,c,c);
                var results = service.invokeAll(r);
                System.out.println("Hare won the race!");
            } catch (Exception e) {e.printStackTrace();}
        }
        public void tortoise() {
            try {
                Callable<Integer> c = () -> sleep();
                final var r = List.of(c,c,c);
                Integer result = service.invokeAny(r);
                System.out.println("Tortoise won the race!");
            } catch (Exception e) {e.printStackTrace();}
        }
        public static void main(String[] p) throws Exception {
            var race = new Race();
            race.service.execute(() -> race.hare());
            race.service.execute(() -> race.tortoise());
        }
    }

    A. Hare won the race! is printed first.
    B. Tortoise won the race! is printed first.
    C. The code does not compile.
    D. The code hangs indefinitely at runtime.
    E. The code throws an exception at runtime.
    F. The output cannot be determined ahead of time.

    Explanation :
    F. The code compiles and runs without issue. 
    The two methods hare() and tortoise() are nearly identical, with one calling invokeAll() and the other calling invokeAny(). 
    Calling the invokeAll() method causes the current thread to wait until all tasks are finished, 
    while calling the invokeAny() method will cause the current thread to wait until at least one task is complete. 
    Both ExecutorService methods operate synchronously, waiting for a result from one or more tasks, 
    but each method call has been submitted to the thread executor as an asynchronous task. 
    For this reason, both methods will take about one second to complete, and since either can finish first, 
    the output will vary at runtime, making option F correct. 
    Note that this program does not terminate, since the ExecutorService is not shut down.

14. Which of the following concurrent collections is sorted? (Choose two.)

    A. ConcurrentSkipList
    B. ConcurrentSkipListSet
    C. CopyOnWriteArrayList
    D. ConcurrentSkipListMap
    E. ConcurrentLinkedQueue
    F. LinkedBlockingQueue

    Explanation :
    B,D. ConcurrentSkipList does not exist as a concurrent collection, making option A incorrect. 
    ConcurrentSkipListSet implements the SortedSet interface, in which the elements are kept sorted, making option B correct. 
    ConcurrentSkipListMap implements the SortedMap interface, in which the keys are kept sorted, making option D correct. 
    The other options define structures that are ordered, but not sorted. 
    Remember, if you see SkipList as part of a concurrent class name, it means it is sorted in some way.

15. What is the output of the following application?
    package taxes;
    import java.util.concurrent.*;
    public class Accountant {
        public static void completePaperwork() {
            System.out.print("[Filing]");
        }
        public static double getPi() {
            return 3.14159;
        }
        public static void main(String[] args) throws Exception {
            ExecutorService x = Executors.newSingleThreadExecutor();
            Future<?> f1 = x.submit(() -> completePaperwork());
            Future<Object> f2 = x.submit(() -> getPi());
            System.out.print(f1.get()+" "+f2.get());
            x.shutdown();
        }
    }
    A. [Filing]
    B. [Filing]3.14159
    C. [Filing]null 3.14159
    D. The declaration of f1 does not compile.
    E. The declaration of f2 does not compile.
    F. The output cannot be determined ahead of time.

    Explanation :
    C. The code compiles without issue, so options D and E are incorrect. 
    The f1 declaration uses the version of submit() in ExecutorService, which takes a Runnable and returns a Future<?>, 
    while the f2 declaration uses an overloaded version of submit(), which takes a Callable expression and returns a generic Future object. 
    The call f1.get() waits until the task is finished and always returns null, 
    since Runnable expressions have a void return type, so [Filing]null is printed first. 
    The call to f2.get() returns then prints 3.14159. For these reasons, option C is the correct answer.

16. Assuming 10 seconds is enough time for all of the tasks to finish, what statements about the
    following program are correct? (Choose two.)

    import java.util.concurrent.*;
    import java.util.concurrent.atomic.*;

    public class Clock {
        private AtomicLong bigHand = new AtomicLong(0);
        void incrementBy10() {
            bigHand.getAndSet(bigHand.get() + 10);
        }
        public static void main(String[] c) throws Exception {
            var smartWatch = new Clock();
            ExecutorService s = Executors.newCachedThreadPool();
            for(int i=0; i<100; i++) {
                s.submit(() -> smartWatch.incrementBy10()).get();
            }
            s.shutdown();
            s.awaitTermination(10, TimeUnit.SECONDS);
            System.out.println(smartWatch.bigHand.get());
        } }

    A. The code does not compile.
    B. The incrementBy10() method is thread-safe.
    C. The incrementBy10() method is not thread-safe.
    D. The output is 1000 on every execution.
    E. The output cannot be determined ahead of time.
    F. The code hangs indefinitely at runtime.

    Explanation :
    C,D. The code compiles and runs without issue. While an AtomicLong is used, there are two calls on this variable, the first to retrieve the value and the second to set the new value. 
    These two calls are not executed together in an atomic or synchronized manner. 
    For this reason, the incrementBy10() method is not thread-safe, and option C is correct. 
    That said, the code performs in single-threaded manner at runtime because the call to get() in the main() method waits for each thread to finish. 
    For this reason, the output is consistently 1000, making option D correct.

17. What is the most likely result of executing the following application?

    import java.util.concurrent.*;
    public class Riddle {
    public void sleep() {
        try { Thread.sleep(5000); } catch (Exception e) {}
    }
    public String getQuestion(Riddle r) {
        synchronized {
            sleep();
            if(r != null) r.getAnswer(null);
            return "How many programmers does it take "
                    + "to change a light bulb?";
        }
    }
    public synchronized String getAnswer(Riddle r) {
        sleep();
        if(r != null) r.getAnswer(null);
        return "None, that's a hardware problem";
    }
    public static void main(String... ununused) {
        var r1 = new Riddle();
        var r2 = new Riddle();
        var s = Executors.newFixedThreadPool(2);
        s.submit(() -> r1.getQuestion(r2));
        s.execute(() -> r2.getAnswer(r1));
        s.shutdown();
    }
    }

    A. A deadlock is produced at runtime.
    B. A livelock is produced at runtime.
    C. The application completes successfully.
    D. The code does not compile.
    E. The code hangs indefinitely at runtime.
    F. The output cannot be determined ahead of time.

    Explanation :
    D. The synchronized block used in the getQuestion() method requires an object to synchronize on. 
    Without it, the code does not compile, and option D is the correct answer. 
    What if the command was fixed to synchronize on the current object, such as using synchronized(this)? 
    Each task would obtain a lock for its respective object and then wait a couple of seconds before requesting the lock for the other object. 
    Since the locks are already held, both wait indefinitely, likely resulting in a deadlock. 
    We say most likely because even with corrected code, a deadlock is not guaranteed. 
    It is possible, albeit very unlikely, for the JVM to wait five seconds before starting the second task, 
    allowing enough time for the first task to finish and avoiding the deadlock completely.

18. Which ScheduledExecutorService method can result in the same action being executed by two
    threads at the same time?

    A. scheduleAtFixedDelay()
    B. scheduleAtFixedRate()
    C. scheduleWithFixedDelay()
    D. scheduleAtSameRate()
    E. scheduleWithRate()
    F. None of the above

    Explanation :
    B. Options A, D, and E include method names that do not exist in ScheduledExecutorService. 
    The scheduleAtFixedRate() method creates a new task for the associated action at a set time interval, even if previous tasks for the same action are still active. 
    In this manner, it is possible multiple threads working on the same action could be executing at the same time, making option B the correct answer. 
    On the other hand, scheduleWithFixedDelay() waits until each task is completed before scheduling the next task, 
    guaranteeing at most one thread working on the action is active in the thread pool.

19. What is the output of the following application?
    package olympics;
    import java.util.concurrent.*;
    public class Athlete {
    int stroke = 0;
    public synchronized void swimming() {
        stroke++;
    }
    private int getStroke() {
        synchronized(this) { return stroke; }
    }
    public static void main(String... laps) {
        ExecutorService s = Executors.newFixedThreadPool(10);
        Athlete a = new Athlete();
        for(int i=0; i<1000; i++) {
            s.execute(() -> a.swimming());
        }
        s.shutdown();
        System.out.print(a.getStroke());
    } }

    A. A deadlock is produced at runtime.
    B. A livelock is produced at runtime.
    C. 1000
    D. The code does not compile.
    E. The result is unknown until runtime because stroke is not written in a thread-safe manner and a write may be lost.
    F. None of the above.

    Explanation :
    F. The application compiles, so option D is incorrect. 
    The stroke variable is thread-safe in the sense that no write is lost, since all writes are wrapped in a synchronized method, making option E incorrect. 
    The issue here is that the main() method reads the value of getStroke() while tasks may still be executing within the ExecutorService. 
    The shutdown() method stops new tasks from being submitted but does not wait for previously submitted tasks to complete. 
    Therefore, the result may output 0, 1000, or anything in between, making option F the correct answer. 
    If the ExecutorService method awaitTermination() is called before the value of stroke is printed and enough time elapses, then the result would be 1000 every time.

20. Which of the following is most likely to be caused by a race condition?

    A. A thread perpetually denied access to a resource
    B. A program hanging indefinitely
    C. An int variable incorrectly reporting the number of times an operation was performed
    D. Two threads actively trying to restart a blocked process that is guaranteed to always end the same way
    E. Two threads endlessly waiting on each other to release shared locks

    Explanation :
    C. A race condition is an undesirable result when two tasks that should be completed sequentially are completed at the same time. 
    The result is often corruption of data in some way. 
    If two threads are both modifying the same int variable and there is no synchronization, then a race condition can occur with one of the writes being lost. 
    For this reason, option C is the correct answer. Option A is the description of resource starvation. 
    Options D and E are describing livelock and deadlock, respectively, while option B is the potential result of either of those events occurring.

21. Which statement about the following class is correct?
    package my;
    import java.util.*;
    public class ThreadSafeList {
        private List<Integer> data = new ArrayList<>();
        public synchronized void addValue(int value) {
            data.add(value);
        }
        public int getValue(int index) {
            return data.get(index);
        }
        public int size() {
            synchronized(ThreadSafeList.class) {
                return data.size();
            }
        }
    }

    A. The code compiles and is thread-safe.
    B. The code compiles and is not thread-safe.
    C. The code does not compile because of the size() method.
    D. The code does not compile because of the getValue() method.
    E. The code does not compile for another reason.
    F. None of the above.

    Explanation :
    B. The class compiles without issue. The class attempts to create a synchronized version of a List<Integer>. 
    The size() and addValue() help synchronize the read/write operations. 
    Unfortunately, the getValue() method is not synchronized so the class is not thread-safe, and option B is the correct answer. 
    It is possible that one thread could add to the data object while another thread is reading from the object, leading to an unexpected result.

22. Which two method names, when filled into the print2() method, produce the same output
    as the print1() method? Assume the input arguments for each represent the same non-null
    numeric value.
    public static synchronized void print1(int counter) {
        System.out.println(counter--);
        System.out.println(++counter);
    }
    public static synchronized void print2(AtomicInteger counter) {
        System.out.println(counter._____________);
        System.out.println(counter._____________);
    }

    A. decrementAndGet() and getAndIncrement()
    B. decrementAndGet() and incrementAndGet()
    C. getAndDecrement() and getAndIncrement()
    D. getAndDecrement() and incrementAndGet()
    E. None of the above

    Explanation :
    D. The post-decrement operator (––) decrements a value but returns the original value. 
    It is equivalent to the atomic getAndDecrement() method. 
    The pre-increment operator (++) increments a value and then returns the new value. 
    It is equivalent to the incrementAndGet() atomic operation. 
    For these reasons, option D is the correct answer.

23. How many lines of the following code snippet contain compilation errors?
    11: ScheduledExecutorService t = Executors
    12:     .newSingleThreadScheduledExecutor();
    13: Future result = t.execute(System.out::println);
    14: t.invokeAll(null);
    15: t.scheduleAtFixedRate(() -> {return;},5,TimeUnit.MINUTES);

    A. None
    B. One
    C. Two
    D. Three
    E. None of the above

    Explanation :
    C. Line 13 does not compile because the execute() method has a return type of void, not Future. 
    Line 15 does not compile because scheduleAtFixedRate() requires four arguments that include an initial delay and period value. 
    For these two reasons, option C is the correct answer.

24. How many times does the following application print W at runtime?
    package crew;
    import java.util.concurrent.*;
    import java.util.stream.*;
    public class Boat {
        private void waitTillFinished(CyclicBarrier c) {
            try {
                c.await();
                System.out.print("W");
            } catch (Exception e) {}
        }
        public void row(ExecutorService s) {
            var cb = new CyclicBarrier(5);
            IntStream.iterate(1, i-> i+1)
                    .limit(12)
                    .forEach(i -> s.submit(() -> waitTillFinished(cb)));
        }
        public static void main(String[] oars) {
            ExecutorService service = null;
            try {
                service = Executors.newCachedThreadPool();
                new Boat().row(service);
            } finally {
                service.isShutdown();
            } 
        } 
    }

    A. 0
    B. 10
    C. 12
    D. The code does not compile.
    E. The output cannot be determined ahead of time.
    F. None of the above.

    Explanation :
    B. When a CyclicBarrier goes over its limit, the barrier count is reset to zero. 
    The application defines a CyclicBarrier with a barrier limit of 5 threads. 
    The application then submits 12 tasks to a cached executor service. 
    In this scenario, a cached thread executor will use between 5 and 12 threads, reusing existing threads as they become available. 
    In this manner,there is no worry about running out of available threads. 
    The barrier will then trigger twice, printing five values for each of the sets of threads, for a total of ten W characters. 
    For this reason, option B is the correct answer.

25. Using the Boat class from the previous question, what is the final state of the application?

    A. The application produces an exception at runtime.
    B. The application terminates successfully.
    C. The application hangs indefinitely because the ExecutorService is never shut down.
    D. The application produces a deadlock at runtime.
    E. None of the above.

    Explanation :
    D. The application does not terminate successfully nor produce an exception at runtime, making options A and B incorrect. 
    It hangs at runtime because the CyclicBarrier limit is 5, while the number of tasks submitted and awaiting activation is 12. 
    This means that two of the tasks will be left over, stuck in a deadlocked state, waiting for the barrier limit to be reached but with no more tasks available to trigger it. 
    For this reason, option D is the correct answer. 
    If the number of tasks was a multiple of the barrier limit, such as 15 instead of 12, 
    then the application will still hang because the ExecutorService is never shut down, and option C would be correct. 
    The isShutdown() call in the application finally block does not trigger a shutdown. Instead, shutdown() should have been used.

26. Given the following program, how many times is TV Time expected to be printed? Assume
    10 seconds is enough time for each task created by the program to complete.
    import java.util.concurrent.*;
    import java.util.concurrent.locks.*;
    public class Television {
        private static Lock myTurn = new ReentrantLock();
        public void watch() {
            try {
                if (myTurn.lock(5, TimeUnit.SECONDS)) {
                    System.out.println("TV Time");
                    myTurn.unlock();
                }
            } catch (InterruptedException e) {}
        }
        public static void main(String[] t) throws Exception {
            var newTv = new Television();
            for (int i = 0; i < 3; i++) {
                new Thread(() -> newTv.watch()).start();
                Thread.sleep(10*1000);
            }
        }
    }

    A. One time.
    B. Three times.
    C. The code does not compile.
    D. The code hangs indefinitely at runtime.
    E. The code throws an exception at runtime.
    F. The output cannot be determined ahead of time.

    Explanation :
    C. The Lock interface does not include an overloaded version of lock() that takes a timeout value and returns a boolean. 
    For this reason, the code does not compile, and option C is correct. 
    If tryLock(long,TimeUnit) had been used instead of lock(), then the program would have been expected to print TV Time three times at runtime.

27. Given the original array, how many of the following for statements enter an infinite loop at
    runtime, assuming each is executed independently?

    var original = new ArrayList<Integer>(List.of(1,2,3));

    var copy1 = new ArrayList<Integer>(original);
    for(Integer q : copy1)
        copy1.add(1);

    var copy2 = new CopyOnWriteArrayList<Integer>(original);
    for(Integer q : copy2)
        copy2.add(2);

    var copy3 = new LinkedBlockingQueue<Integer>(original);
    for(Integer q : copy3)
        copy3.offer(3);

    var copy4 = Collections.synchronizedList(original);
    for(Integer q : copy4)
        copy4.add(4);

    A. Zero.
    B. One.
    C. Two.
    D. Three.
    E. Four.
    F. The code does not compile.

    Explanation :
    B. The for loops using copy1 and copy4 both throw a ConcurrentModificationException at runtime, since neither allows modification while they are being iterated upon. 
    Next, CopyOnWriteArrayList makes a copy of the collection every time it is modified, preserving the original list of values the iterator is using. 
    For this reason, the for loop using copy2 completes without throwing an exception or creating an infinite loop. 
    On the other hand, the loop with copy3 enters an infinite loop at runtime. 
    Each time a new value is inserted, the iterator is updated, and the process repeats. 
    Since this is the only statement that produces an infinite loop, option B is correct.

28. Which ExecutorService method guarantees all running tasks are stopped in an
    orderly fashion?

    A. shutdown()
    B. shutdownNow()
    C. halt()
    D. shutdownAndTerminate()
    E. None of the above

    Explanation :
    E. The shutdown() method prevents new tasks from being added but allows existing tasks to finish. 
    In addition to preventing new tasks from being added, the shutdownNow() method also attempts to stop all running tasks. 
    Neither of these methods guarantees any task will be stopped, making option E the correct answer. 
    Options C and D are incorrect because they name methods that do not exist in ExecutorService.

29. Assuming 10 seconds is enough time for all of the tasks to finish, what is the output of the
    following application?
    import java.util.concurrent.*;
    public class Bank {
        static int cookies = 0;
        public synchronized void deposit(int amount) {
            cookies += amount;
        }
        public static synchronized void withdrawal(int amount) {
            cookies -= amount;
        }
        public static void main(String[] amount) throws Exception {
            var teller = Executors.newScheduledThreadPool(50);
            Bank bank = new Bank();
            for(int i=0; i<25; i++) {
                teller.submit(() -> bank.deposit(5));
                teller.submit(() -> bank.withdrawal(5));
            }
            teller.shutdown();
            teller.awaitTermination(10, TimeUnit.SECONDS);
            System.out.print(bank.cookies);
        } 
    }

    A. 0
    B. 125
    C. -125
    D. The code does not compile.
    E. The result is unknown until runtime.
    F. An exception is thrown.

    Explanation :
    E. The program compiles and does not throw an exception at runtime. 
    The class attempts to add and remove values from a single cookie variable in a thread-safe manner but fails to do so because the methods deposit() and withdrawal() synchronize on different objects. 
    The instance method deposit() synchronizes on the bank object, while the static method withdrawal() synchronizes on the static Bank.class object. 
    Since the compound assignment operators (+=) and (-=) are not thread-safe, 
    it is possible for one call to modify the value of cookies while the other is already operating on it, resulting in a loss of information. 
    For this reason, the output cannot be predicted, and option E is the correct answer. 
    If the two methods were synchronized on the same object, then the cookies variable would be protected from concurrent modifications, printing 0 at runtime.

30. What is the output of the following application?
    import java.util.*;
    public class SearchList<T> {
        private List<T> data;
        private boolean foundMatch = false;
        public SearchList(List<T> list) {
            this.data = list;
        }
        public void exists(T v,int start, int end) {
            if(end-start==0) {}
            else if(end-start==1) {
                foundMatch = foundMatch || v.equals(data.get(start));
            } else {
                final int middle = start + (end-start)/2;
                new Thread(() -> exists(v,start,middle)).run();
                new Thread(() -> exists(v,middle,end)).run();
            }
        }
        public static void main(String[] a) throws Exception {
            List<Integer> data = List.of(1,2,3,4,5,6);
            SearchList<Integer> t = new SearchList<Integer>(data);
            t.exists(5, 0, data.size());
            System.out.print(t.foundMatch);
        } 
    }

    A. true
    B. false
    C. The code does not compile.
    D. The result is unknown until runtime.
    E. An exception is thrown.
    F. None of the above.

    Explanation :
    A. The code attempts to search for a matching element in an array using multiple threads. 
    While it does not contain any compilation problems, it does contain an error. 
    Despite creating Thread instances, it is not a multithreaded program. 
    Calling run() on a Thread runs the process as part of the current thread. 
    To be a multithreaded execution, it would need to instead call the start() method. 
    For this reason, the code completes synchronously, waiting for each method call to return before moving on to the next and printing true at the end of the execution, making option A the correct answer. 
    On the other hand, if start() had been used, then the application would be multithreaded but not thread-safe. 
    The calls to update foundMatch are not synchronized, and even if they were, the result might not be available by the time print() in the main() method was called. 
    For this reason, the result would not be known until runtime.