# EXERCICE NOTES

## Foundation Test 1 

### Callable vs Runnable uses cases :
`Callable<T>` and `Runnable` are both functional interfaces that can be used to run asynchronous tasks in separate threads. The main difference between them is that :

|Callable|Runnable|
|------|------|
|   Has the method `T call() throws Exception;` | Has the method `void run();`|
|   Is used for tasks that return a result| Is used when task doesn't return a result|
|   Is used for tasks that throws checked exceptions| Is used for tasks that doesn't throws checked exceptions|

`Callable<T>` and `Runnable` can be used in multiple ways:
 - Callable using one of `ExecutorService` methods :
```java
<T> Future<T> submit(Callable<T> task);
<T> T invokeAny(Collection<? extends Callable<T>> tasks);
<T> List<Future<T>> invokeAll(Collection<? extends Callable<T>> tasks) throws InterruptedException;
```
- Runnable can be used to **directly** create a `Thread`, or via ExecutorService :
```java
/**
 * Using Thread
 */
Thread t1 = new Thread(aRunnable); 
// the above is equivalent to :
Thread t2 = new Thread(() -> {
    // do somthing
}); 

/**
 * Using ExecutorService
 */
<T> Future<T> submit(Runnable task, T result); // Submits a Runnable task for execution and returns a Future containing the result
Future<?> submit(Runnable task); // submit a task and returns null on succeful execution 
```

### Connection

When a connection is created, it is in `auto-commit` mode by default. This means that each individual SQL statement is treated as a transaction and is automatically committed right after it is completed. Thus **To enable a set of statement to be grouped in the same transaction we should disable the auto-commit mode**, right after creating the `Connection` calling `conn.setAutoCommit(false);`

### Switch statement rules

Here are the rules for a switch statement:
1- Only String, byte, char, short, int, (and their wrapper classes Byte, Character, Short, and Integer), and enums can be used as types of a switch variable. (String is allowed only since Java 7). 
2- The case constants must be assignable to the switch variable. For example, if your switch variable is of class String, your case labels must use Strings as well.
3- **The switch variable must be big enough to hold all the case constants**. For example, if the switch variable is of type char, then none of the case constants can be greater than 65535 because a char's range is from 0 to 65535.
4- All case labels should be COMPILE TIME CONSTANTS. 
5- No two of the case constant expressions associated with a switch statement may have the same value.
6- At most one default label may be associated with the same switch statement.


### Static nested class/interface

Note the difference between an inner class and a static nested class. Inner class means a NON STATIC class defined inside a class. Remember:
1- **A NESTED CLASS** is any class whose declaration occurs within the body of another class or interface.
2- A top level class is a class that is not a nested class.
3- **AN INNER CLASS** is a nested class that **IS NOT EXPLICITLY OR IMPLICITLY DECLARED STATIC**.
4- A class/interface defined inside an interface is **implicitly static**.
5- **NESTED CLASSES** doesn have the access to the outer class instance **since it's static**.

