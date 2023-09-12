* For me, a good piece of code must be (SOC): (i) (s)imple (it solves one problem), (ii) (o)bvious (the author's intentions must be clear to anyone that reads it) and (iii) (c)oncise (the simplest possible solution that do the trick unless there is a performance incentive to do differently

* When designing a complex software, divide into two parts: (i) the framework (take the common parts and add to the project's library, use some scaffolding tool to optimize some common tasks, and so one)  (ii) the client code (it will use the framework and other libraries to implement the final software). Keep constantly moving common, repeatable and fallible (susceptible to human error) parts of the system into the framework. Make programmers's live easy as the main goal.

* When designing the framework, all main use cases must be accessible with zero or few lines of code (and well documented). However, always provie a "hatch" for any other possible scenarios. Do not make it hard to adapt. This will discourage developers to use it.

* Test driven development (TDD) is a good approach to "feel" your framework or client code. That's the whole point of TDD. Otherwise it would be called Test first development.

* Fluent code is very goode to use and adheres to the SOC principles (unless there is a performance reason not to do so).

* Functional programming (FP) principles such as pure functions and avoiding or controlling side-effects makes code more roboust.

* I like to mix Object-oriented Programming (OOP) and functional programming. I design my classes like OOP but internally I use FP.

* One important lesson from FP that I constantly use is to think the problem as a sequence of sub-problems. Each problem is composed of sub-problems. Each sub-problem is a function/classes that solves only a single problem. The final solution is the composible of the sub-problems.

* Idempotent is a powerful technique. It help creating safer code together with pure functions and avoiding/controlling side-effects. Use it whenever is possible.

* Exceptions should be used in exceptional cases (i.e. unexpected events) otherwise it is better to return a Result/Optional/Monoid/Boolean value when error _can_ occur (e.g. validation). Some people, like chrome team, avoids exception altogether.

* An excellent tip I once learned is: `only deal with a single problem per time`. Don't try to do more than one problem per time. So, for instance, create a new system that the company has never worked before, using a new language with a new framework, is a huge red flag. Too much unknowns.

* It is also good practice to determine the invarients of your code as well as the pre and pos conditions (function or class) needs/will provide.

* Your whole code should be read as a sentence. You should be able to read your code and see very clearly the functional requirements (that's why fluent API's are good).

* Your code/API/Framework should be modeled to be used by others, not just you. We should always consider: "if someone else reads this code, will they understand?". That's an obvious code is a essencial principle.

* Follow the network (I think) design principle: be open to what you will consume/receive but be restrictive to what you will produce/return (i.e. be robust to erroneous input but follow the agreed rules). The final software will be more robust.

* Sentinels can make code more easy to implement and less error-prone.

* Mutability is fairly ok in a non-concurrent environment. However, in a concurrent environment, you should pay very close attention to mutability. Reactor or Actor model (from erlang/elixir) is the best way I know to develop concurrent code. It is just perfection (as close as you can get) and it is very performatic (as the old saying goes, whatsup uses erlang and only have a few servers to billion users world-wide).

* Single thread like javascript does not have concurrent accesses but it still has concurrent problems due to async/await primitives.

* I will, most of the time, prefer orchestration code/architecture over choreography. It is safer, more stable and most importantly easier to reason. (unless there is a very good reason otherwise).

* Avoid Mutex and Semaphores (it causes performance issues). Prefer more to do more parallel work, whenever is possible. Better yet, use/implemenet a lock-free or wait-free data structure/algorithm.

* Avoid, at all costs, sleep or delay directives. This will cause temporal dependencies and lots of hard to catch bugs.

* Single thread like javascript is a very useful and performatic architecture. I like to emulate this architecture every once in a while because it is easy and you don't have to worry about concurrent memory access.

* Concurrecy affects everywhere in the code. I perfer to assume that there is no order when using mutex or semaphores (avoid using them) (although, as far as I know, they are first-in-first-out).

* Sometimes "do not repeat yourself" (DRY) is more complex than worth it. Personally I prefer single source of truth (SST) (i.e. the business rule will be in a single place only).

* Split the code increases structural complexity (be aware of it). Only increase structural complexity when needed.

* It is super important to keep refactoring the code, to reduce entropy (chaos, mess) and to make life easier (perhaps some code could go to the framework code?).

* The system is constantly changing, perfection is impossible in this scenario.

* Break the code into semantic elements, not just break the code because "it is too big". Always think about the language. You should approach development as you approach writing (literature).

* Sub-problem classes/functions does not any hard-coded parameters. Parent class/function calls child with parameters needed. Even the root class/function should avoid hard-coded parameters and use enviroment variables or something else instead.

* Some important attributes of a good code are: (i) semantic consistent (you don't write/name A but it's actually B), (ii) linear (you can follow the code as much as possible) and (iii) deterministic (as much as possible)

* Avoid trusting 3-party APIs/code. Wrap them into a protection layer.

* Always assume something will go wrong. Add treatment to that.

* I like to structure my code in the following order: Firstly all invalid cases (preconditions) guarded by guard clauses in the order of the most critical to least critial (sometimes you can even add recover mechanisms in the least critical clauses and move on). Then, lastly, the happy path. it is easy to find all the precondictions to run your code and, in the happy path, the code is simpler because all necessary conditions were already treated. You only do the happy path. It is also more robust.
