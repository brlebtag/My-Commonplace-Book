# multiprocessor programming

*Disclaimer:* many of the information here presented I learned from the book "the art of multiprocessor programming"

* In a multiprocessor environment, multiple function calls can be executed simultaneously from different threads. Thus, one question arises: what will be the final order of execution (imagine a queue data structure: what will be the first element, the second element, and so on...). Therefore, we have some `consistency models` (order scheme) to decide/to model our data structure.

*`Quiescent consistency` guarantees that two sets of concurrent function calls (like two events of bursts of concurrent function calls) separated by a period of relatively calm will be ordered, i.e. in the first burst, the calls themselves will be inserted (again, imagine a queue data structure) in any particular order *but* they will inserted firstly than the elements inserted in the second burst of concurrent function calls.
