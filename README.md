# OCA-8/OCP-11 PREPARATION NOTES 

## Introduction
This repository contains notes about OCA 1ZO-808 and OCP 1ZO-819 certifications, you can contribute to it either adding/updating notes by raising PRs

## Resources

### Books

* Oracle Certified Professional 11 Developer Complete : [Amazon link](https://www.amazon.com/Oracle-Certified-Professional-Developer-Complete/dp/1119619130)

## Notes

> Module 1 : Primitive ...

| Note | Example     |
| ------ | ------    |
| Note 1 | Example 1 |

### Chapter 2: Java building blocks "you have to learn to walk before you can run"

##### Constructors
A constructor allow us to create instance object for a given class. There are two rules that a constructor should match :
    1. the name of the constructor matches the name of the class.
    2. there’s no return type
The compiler provide a "default" constructor that do nothing ! 

##### Instance initializers
Is a block {} that appears *outside* a method, example : 

```java
public class Post {
    public static void main(String... args) {
        System.out.println("I'm the main method");
        Post post = new Post();
    }
    public Post() {
        System.out.println("Hello I'm the constructore");
    }

    {
        System.out.println("Hello I'm an instance block, Before the constructor! I can call fields like name=" + name);
    }
}
```
Instance initializers are executed before the main method.
Any variable that is declared inside a block will not be accessible from outside.

##### Static blocks
Are blocks {} that are prefixed with static, at class level, theys are executed before anything else on the class. Exemple : 

```java
public class Test {
    String name = "Abdel";
    public static void main(String... args) {
        System.out.println("I'm executed before anything in the main");
        Test testObj = new Test();
    }

    public Test() {
        System.out.println("Hello I'm the constructore");
    }

    {
        System.out.println("Hello I'm an instance block, Before the constructor! I can call fields like name=" + name);
    }

    static {
        System.out.println("I'm a static block, I'm executed before instance initializers");
    }
}

```

##### Order of initialization
    1. Static blocks 
    2. Field and initializer blocks (in the order in which they appear in the file).
    3. Constructor

##### Data types
Java support two types of data: 
    * primitive types.
    * reference types

Java has 8 built-in data-types (the Java primitive types).
A primitive is just a single value in memory, such as number or character.

boolean | true/false
byte    | 8 bit     => signed (-/+) number [-128,127]
char    | 16 bit    => unsigned number; only positive number are supported
short   | 16 bit    => signed number 
int     | 32 bit
long    | 64 bit
float    | 32 bit   => require f following the number
double  | 64 bit

When a number is declared, example: `int sum;` java will reserve 32 bits memory.
We can use long values with capital 'L' (prefered) or 'l' if the value > int ; otherwise we can ommit the suffix ! 

you can use *literals*, which are the _ in the numbers; example : 

```java
int million = 1_000_000;
```


