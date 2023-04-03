[View code on GitHub](https://github.com/misbahsy/the-algorithm/src/java/com/twitter/search/earlybird/util/ParallelUtil.java)

The `ParallelUtil` class provides utility methods for running functions in parallel across a list of inputs. The `parmap` method takes a function that maps an input of type `T` to an output of type `R`, and applies it to each element of a list of inputs of type `T`. The method returns a list of outputs of type `R`, one for each input. The function is executed in parallel across multiple threads, with each thread processing one input at a time. 

The `parmap` method has two overloaded versions. The first version takes a thread name, a function, and a list of inputs, and uses as many threads as there are elements in the input list. The second version takes a thread name, a thread pool size, a function, and a list of inputs, and uses a fixed-size thread pool with the specified number of threads. The second version is useful when the input list is large and the number of threads needs to be limited to avoid overwhelming the system.

The `parmap` method uses the `FuturePool` class from the Twitter `util` library to execute the function in parallel. The `FuturePool` class provides a way to execute a function asynchronously on a thread pool and obtain a `Future` object that represents the result of the computation. The `Future` object can be used to wait for the computation to complete and obtain the result.

The `parmap` method first creates an executor service with the specified number of threads, using the `Executors.newFixedThreadPool` method. It then creates a `FuturePool` object from the executor service, using the `FuturePool$.MODULE$.apply` method. It then maps each input in the input list to a `Future` object that represents the result of applying the function to the input, using the `futurePool.apply` method. The function is wrapped in a lambda expression that catches any exceptions thrown by the function and rethrows them as `RuntimeExceptions`. The `map` method returns a list of `Future` objects.

The `parmap` method then waits for all the `Future` objects to complete and returns a list of results. It does this by calling the `Future$.MODULE$.collect` method on the list of `Future` objects, which returns a `Future` object that represents the list of results. It then calls the `Await.result` method on the `Future` object to wait for the computation to complete and obtain the list of results. Finally, it shuts down the executor service using the `executor.shutdownNow` method.

The `ParallelUtil` class also defines a `CheckedFunction` interface that represents a function that takes an input of type `T` and returns an output of type `R`, and may throw a checked exception. This interface is used as the type of the function parameter in the `parmap` method. 

Overall, the `ParallelUtil` class provides a convenient way to execute a function in parallel across a list of inputs, using a fixed-size thread pool. It is useful for tasks that require significant CPU for each input, and have less inputs than the number of cores.
## Questions: 
 1. What is the purpose of the `parmap` method?
- The `parmap` method runs a function in parallel across the elements of a list and returns the results, or throws an exception if any of the functions throws.

2. What is the purpose of the `CheckedFunction` interface?
- The `CheckedFunction` interface defines a function from T to R that throws checked Exceptions.

3. What is the purpose of the `buildThreadFactory` method?
- The `buildThreadFactory` method creates a new `ThreadFactory` that produces threads with a given name format and daemon status.