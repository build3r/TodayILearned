## Coroutine Exception Handling
1. By default if an exception occurs in child coroutines, the parent coroutine and all sibling coroutines are cancelled.
2. You have catch the exception where it occurs, wrapping builder is useless.
3. If you want parent and siblings to continue use `SupervisorJob` . Don't use this as argument to coroutine builder.
4. You can also wrap coroutine builders in `supervisorScope` to stop exception propagation.
5. In case of async/await builder wrap await in try/catch.
6. If a coroutine throw a subclass on `CancellationException`, the exception will not be propagated.
7. `CoroutineExceptionHandler` is good way to catch exception if you need to handle all exception in the same way.
[Source](https://kt.academy/article/cc-exception-handling)