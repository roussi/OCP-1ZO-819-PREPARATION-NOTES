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
6- An inner class can extend it's outer class.
7- Member variables of the outer class can be accessibles to the inner class **ONLY IF THEY ARE NOT SHADOWED** in the inner class.
8- More than one inner class can be associated to the outer class.

### Inheritence 
Constructors and static initializers are not members and therefore are not inherited.

### If statement
The only time we can the `=` operator in an `if statement` without having compile/runtime error is when both operands are booleans (since `if(a=b)` get the value that is assigned, thus `if(a=b)` is equivalent to `if(b)`).

The expression (a = b) does not compare the variables a and b, but rather assigns the value of b to the variable a. **The result of the expression is the value being assigned**. Since a and b are boolean variables, the value returned by the expression is also boolean. This allows the expressions to be used as the condition for an if-statement.  if-clause and the else-clause can have empty statements. Empty statement ( i.e. just ; ) is a valid statement. However, the following is illegal:  if (true) else; because the if part doesn't contain any valid statement. (A statement cannot start with an else!) But the following is valid:  if(true) if(false); because if(false); is a valid statement.

### Literals : What does need a casting
- Conversion from short to char & from char to short (they don't have the same range).
- Conversion from float to int.
- conversion from double to long ?

> Further, if you have a final variable and its value fits into a smaller type, then you can assign it without a cast because compiler already knows its value and realizes that it can fit into the smaller type. This is called **implicit narrowing** and is allowed between byte, int, char, and, short but not for long, float, and double.

```java
byte b = 20;
final int i = 10;
b = i; // is OK, since i is final; constant

final float f = 10.0;
i = f; // will not compile, even after changing 10.0 to 10.0f
```

### String manipulation
- `char charAt(int index)`, take int (or lower : char, short, byte), and return the char at the given position starting from 0. It can take up to length-1 as argument. if we pass an invalid index it throws an `IndexOutOfBoundsException` (not necessary a `java.lang.StringIndexOutOfBoundsException`), so pay attention to some question in the exam that could trick you, like :
> `charAt` throws StringIndexOutOfBoundsException if passed a value higher than or equal to the length of the string (or less than 0).

It is not a valid option because the implementation is free to throw some other exception as long as it is an `IndexOutOfBoundsException`. 

### Functional interface
Is an interface that contains exaclty **ONE `abstract` method**, and it may contain zero or more default methods and/or static methods in addition to the abstract method. **Functional interfaces** are usefull in the context of lambda expression, since a functional interface contains exactly one abstract method, you can omit the name of that method when you implement it using a lambda expression.

### Scope restriction
The order of scope restriction is as follow :
public < protected < package (or default) < private.
(here, public is least restrictive and private is most restrictive).

