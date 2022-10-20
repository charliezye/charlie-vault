Generics are parameterized types - in other words type as a parameter to methods, classes, and interfaces.
- With this, it's possible to create classes that work with different data types called generic entities

### Generic Class
Like C++, we use <> to specify parameter types in generic class creation. To create objects of a generic class, we use the following syntax. 

``` java
// To create an instance of generic class 
BaseType <Type> obj = new BaseType <Type>()
```

- Cannot use primitives, only object types
	- Primitive type arrays can be passed as these are array objects
- Can also use multiple type parameters

### Generic Functions
```
// A Generic method example
    static <T> void genericDisplay(T element)
    {
        System.out.println(element.getClass().getName()
                           + " = " + element);
    }
```

### Type Safety

Two objects of the same class with references to different types will throw errors if called in any type-specific operation due to different type parameters

```
 // instance of Integer type
        Test<Integer> iObj = new Test<Integer>(15);
        System.out.println(iObj.getObject());
  
        // instance of String type
        Test<String> sObj
            = new Test<String>("GeeksForGeeks");
        System.out.println(sObj.getObject());
        iObj = sObj; // This results an error
```


### Naming Conventions
-   T – Type
-   E – Element
-   K – Key
-   N – Number
-   V – Value

### Advantages

**1. Code Reuse:** We can write a method/class/interface once and use it for any type we want.

**2. Type Safety:** Generics make errors to appear compile time than at run time (It’s always better to know problems in your code at compile time rather than making your code fail at run time). Suppose you want to create an ArrayList that store name of students, and if by mistake the programmer adds an integer object instead of a string, the compiler allows it. But, when we retrieve this data from ArrayList, it causes problems at runtime.

**3. Individual Type Casting is not needed:** If we do not use generics, then, in the above example, every time we retrieve data from ArrayList, we have to typecast it. Typecasting at every retrieval operation is a big headache. If we already know that our list only holds string data, we need not typecast it every time.

**4.** **Generics Promotes Code Reusability:** With the help of generics in Java, we can write code that will work with different types of data. For example,
```
public <T> void genericsMethod (T data) {...}
```
Here, we have created a generics method. This same method can be used to perform operations on integer data, string data, and so on.

**5. Implementing Generic Algorithms:** By using generics, we can implement algorithms that work on different types of objects, and at the same, they are type-safe too.