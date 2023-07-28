# Multiprocessor Programming

*Disclaimer:* many of the information here presented I learned from the book "The Art of multiprocessor programming"

* In a multiprocessor environment, multiple function calls can be executed simultaneously from different threads. Thus, one question arises: what will be the final order of execution (imagine a queue data structure: what will be the first element, the second element, and so on...). Therefore, we have some `consistency models` (order scheme) to decide/to model our data structure.

* `Quiescent consistency` guarantees that two sets of concurrent function calls (like two events of bursts of concurrent function calls) separated by a period of relatively calm will be ordered, i.e. in the first burst, the calls themselves will be inserted (again, imagine a queue data structure) in any particular order *but* they will inserted firstly than the elements inserted in the second burst of concurrent function calls.

* `Sequencial consistency` guarantees that burst of concurrent function calls will have a order (consistent with program order, i.e. if you call, *in the same thread*, insert() and then remove(), the former will be executed early and the latter will be executed later). However, there is no strict order or guarantees *among* threads. They could execute in any order. For instance, imagine a single queue. All threads will insert (call a function) in this queue and only one will be inserted at a time (randomly) but looking from the perspective of the same thread, the items would be ordered.

* `Linearzability` guarantees a sequence for the same thread just like the sequencial consistency but they will be executed (imagine a item being inserted into a queue) in the exactly time they were called (inserted). It's the strongest sequence quarantee and the hardest to implement. When events happens simultaneously, we can pick any order as long as it is the same order for any "reply" history execution anywhere (thread, machine, process, etc) (one rule to rule them all!).

* `Nonblocking` property is when you call something and it does not block. You can receive, for instance, instead a `false` value, which allows to you proceed and try it again another time. On the other hand, a `blocking` property halts the callee for as long as the function called needed.

* Function calls, when developed for a multiprocessor environment, can present different `progress conditions` such as: (i) wait-free, (ii) lock-free and (iii) obstruction-free.

* `Wait-free` means the function guarantees the function will not be blocked (e.g. like using a lock, semaphore, mutex, etc) and no one will starve (i.e. eventually your function call will succeed). If there is a bound number or time, it is called `bounded wait-free`.

* `Lock-free` means the function guarentees the function will not be blocked (e.g. like using a lock, semaphore, mutex, etc), at least one thread will execute but others may starve (depending on the problem it might never happen).

* `Obstruction-free` means the function call execute until the very end after all other functions are aborted. Imagine like, you remove all the obstruction from the way for that particular function to execute, it will execute freely. One way people may implement an obstruction-free is by implementing a rollback function to abort current work in case there is a collision due to concurrency. For instance, the function is free to execute but, if in the final moment it realizes it is in a concurrency situation, it may choose to abort itself.

* `Contention` occurs when multiple threads try to acquire a lock. `High contention` means a big number of threads are trying to acquire a lock and `low contention` means a small number of threads are trying to acquire the lock at the same time.

* `False Sharing` occurs when adjacent data items (such as array elements) share a single cache line. A write to one item invalidates that entire cache line, which causes invalidation traffic to processors that are spinning on unchanged but near items that happen to fall in the same cache line.

* `Cache Coherency` is a situation where multiple processor cores share the same memory hierarchy, but have their own L1 data and instruction caches.

* `Freedom from interference` is when an algorithm guarantees that the user can only modify it's instances via it's public methods, i.e. no internal components of the algorithm (such as nodes in a list or tree) can't be modified externally.

* `Lost-wakeup problem` happens when special care is not taken and, due to concurrency, an thread does not receives a wake-up call from the OS, even though, the algorithm should have called it. To avoid this, you should invoke wake-up calls in all circumstances (not in very specific cases, such as in the first time there is no item on the list or the first time when the list is full) and/or specify a timeout. Otherwise, threads can hang forever (depending on the problem).

* `Linearization Point` is the code segment where the sequence of events/code stop from being concurrent and becomes sequencial. For example, right after a mutex.lock(), only one thread can execute at once. So the lock() becomes a linearization point.