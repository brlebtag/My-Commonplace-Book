* For me, a good piece of code must be (SOC): (i) simple (it solves one problem), (ii) obvious (the author's intentions must be clear to anyone that reads it) and (iii) concise (the simplest possible solution that do the trick unless there is a performance incentive to do differently

* When designing a complex software, divide into two parts: (i) the framework (take the common parts and add to the project's library, use some scaffolding tool to optimize some common tasks, and so one)  (ii) the client code (it will use the framework and other libraries to implement the final software). Keep constantly moving common, repeatable and fallible (susceptible to human error) parts of the system into the framework. Make programmers's live easy as the main goal.

* When designing the framework, all main use cases must be accessible with zero or few lines of code (and well documented). However, always provie a "hatch" for any other possible scenarios. Do not make it hard to adapt. This will discourage developers to use it.

* TDD is a good approach to "feel" your framework or client code. That's the whole point of TDD. Otherwise it would be called Test first development.

* Fluent code is very goode to use and adheres to the SOC principles (unless there is a performance reason not to do so).

* Functional programming (FP) principles such as pure functions and avoiding or controlling side-effects makes code more roboust.

* I like to mix OOP and functional programming. I design my classes like OOP but internally I use FP.

* One important lesson from FP that I constantly use is to think the problem as a sequence of sub-problems. Each problem is composed of sub-problems. Each sub-problem is a function/classes that solves only a single problem. The final solution is the composible of the sub-problems.
  
