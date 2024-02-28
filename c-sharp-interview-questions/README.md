# C# Interview Questions and Answers

Preparing for a Senior C# Developer interview? No worries, we've got you covered! Check out our list of advanced C# interview questions for experienced developers and ace your next job interview in style!
 

## Q1: What is C#? ⭐

**Answer:**

C# is the programming language for writing Microsoft .NET applications. C# provides the rapid application development found in Visual Basic with the power of C++. Its syntax is similar to C++ syntax and meets 100% of the requirements of OOPs like the following: 
* Abstraction
* Encapsulation
* Polymorphism
* Inheritance

🔗 **Source:** [c-sharpcorner.com](https://www.c-sharpcorner.com/UploadFile/8ef97c/C-Sharp-net-interview-questions-and-answers/)


## Q2: What is an Object? ⭐

**Answer:**

According to MSDN, "_a class or struct definition is like a blueprint that specifies what the type can do. An object is basically a block of memory that has been allocated and configured according to the blueprint. A program may create many objects of the same class. Objects are also called instances, and they can be stored in either a named variable or in an array or collection. Client code is the code that uses these variables to call the methods and access the public properties of the object. In an object-oriented language such as C#, a typical program consists of multiple objects interacting dynamically"._

Objects helps us to access the member of a class or struct either they can be fields, methods or properties, by using the dot. 

🔗 **Source:** [c-sharpcorner.com](https://www.c-sharpcorner.com/UploadFile/8ef97c/C-Sharp-net-interview-questions-and-answers/)


## Q3: What is the difference between "continue" and "break" statements in C#? ⭐

**Answer:**

* using **break** statement, you can jump out of a loop
* using **continue** statement, you can jump over one iteration and then resume your loop execution

🔗 **Source:** [c-sharpcorner.com](https://www.c-sharpcorner.com/UploadFile/8ef97c/C-Sharp-net-interview-questions-and-answers/)


## Q4: What are property Accessors? ⭐

**Answer:**

The _get_ and _set_ portions or blocks of a property are called accessors. These are useful to restrict the accessibility of a property, the set accessor specifies that we can assign a value to a private field in a property and without the set accessor property it is like a read-only field. By the get accessor we can access the value of the private field, in other words it returns a single value. A Get accessor specifies that we can access the value of a field publically.

🔗 **Source:** [c-sharpcorner.com](https://www.c-sharpcorner.com/UploadFile/8ef97c/C-Sharp-net-interview-questions-and-answers/)


## Q5: What is Managed or Unmanaged Code? ⭐⭐

**Answer:**

* **Managed Code**  - The code, which is developed in .NET framework is known as managed code. This code is directly executed by CLR with the help of managed code execution. Any language that is written in .NET Framework is managed code.
* **Unmanaged Code** - The code, which is developed outside .NET framework is known as unmanaged code. Applications that do not run under the control of the CLR are said to be unmanaged, and certain languages such as C++ can be used to write such applications, which, for example, access low - level functions of the operating system. Background compatibility with the code of VB, ASP and COM are examples of unmanaged code.


🔗 **Source:** [c-sharpcorner.com](https://www.c-sharpcorner.com/UploadFile/8ef97c/C-Sharp-net-interview-questions-and-answers/)


## Q6: What is Boxing and Unboxing? ⭐⭐

**Answer:**

Boxing and Unboxing both are used for type conversion but have some difference:

* **Boxing** - Boxing is the process of converting a value type data type to the object or to any interface data type which is implemented by this value type. When the CLR boxes a value means when CLR is converting a value type to Object Type, it wraps the value inside a System.Object and stores it on the heap area in application domain.

* **Unboxing** - Unboxing is also a process which is used to extract the value type from the object or any implemented interface type. Boxing may be done implicitly, but unboxing have to be explicit by code. 

The concept of boxing and unboxing underlines the C# unified view of the type system in which a value of any type can be treated as an object.

🔗 **Source:** [c-sharpcorner.com](https://www.c-sharpcorner.com/UploadFile/8ef97c/C-Sharp-net-interview-questions-and-answers/)


## Q7: What is the difference between a struct and a class in C#? ⭐⭐

**Answer:**

Class and struct both are the user defined data type but have some major difference:  
**  
Struct**

* The struct is value type in C# and it inherits from System.Value Type.
* Struct is usually used for smaller amounts of data.
* Struct can't be inherited to other type.
* A structure can't be abstract.
* No need to create object by new keyword.
* Do not have permission to create any default constructor.

**Class**

* The class is reference type in C# and it inherits from the System.Object Type.
* Classes are usually used for large amounts of data.
* Classes can be inherited to other class.
* A class can be abstract type.
* We can't use an object of a class with using new keyword.
* We can create a default constructor.

🔗 **Source:** [c-sharpcorner.com](https://www.c-sharpcorner.com/UploadFile/8ef97c/C-Sharp-net-interview-questions-and-answers/)


## Q8: What is enum in C#? ⭐⭐

**Answer:**

An **enum** is a value type with a set of related named constants often referred to as an enumerator list. The enum keyword is used to declare an enumeration. It is a primitive data type, which is user defined. An enum is used to create numeric constants in .NET framework. All the members of enum are of enum type. Their must be a numeric value for each enum type.

**Some points about enum**

* Enums are enumerated data type in C#.  
* Enums are strongly typed constant. They are strongly typed, i.e. an enum of one type may not be implicitly assigned to an enum of another type even though the underlying value of their members are the same.  
* Enumerations (enums) make your code much more readable and understandable.  
* Enum values are fixed. Enum can be displayed as a string and processed as an integer.  
* The default type is int, and the approved types are byte, sbyte, short, ushort, uint, long, and ulong.  
* Every enum type automatically derives from System.Enum and thus we can use System.Enum methods on enums.  
* Enums are value types and are created on the stack and not on the heap.

🔗 **Source:** [c-sharpcorner.com](https://www.c-sharpcorner.com/UploadFile/8ef97c/C-Sharp-net-interview-questions-and-answers/)


## Q9: Can "this" be used within a static method? ⭐⭐

**Answer:**

We can't use _this_ in static method because keyword _this_ returns a reference to the current instance of the class containing it. Static methods (or any static member) do not belong to a particular instance. They exist without creating an instance of the class and call with the name of a class not by instance so we can't use this keyword in the body of static Methods, but in case of Extension Methods we can use it as the functions parameters.

🔗 **Source:** [c-sharpcorner.com](https://www.c-sharpcorner.com/UploadFile/8ef97c/C-Sharp-net-interview-questions-and-answers/)


## Q10: Define Property in C#? ⭐⭐

**Answer:**

**Properties** are members that provide a flexible mechanism to read, write or compute the values of private fields, in other words by the property we can access private fields. In other words we can say that a property is a return type function/method with one parameter or without a parameter. These are always public data members. It uses methods to access and assign values to private fields called accessors.

🔗 **Source:** [c-sharpcorner.com](https://www.c-sharpcorner.com/UploadFile/8ef97c/C-Sharp-net-interview-questions-and-answers/)


## Q11: What is the difference between string and StringBuilder in c#? ⭐⭐

**Answer:**

**String**
* It's an immutable object that hold string value.
* Performance wise string is slow because its' create a new instance to override or change the previous value.
* String belongs to System namespace.

**StringBuilder**
* StringBuilder is a mutable object.  
* Performance wise StringBuilder is very fast because it will use same instance of StringBuilder object to perform any operation like insert value in existing string.  
* StringBuilder belongs to System.Text.Stringbuilder namespace.

🔗 **Source:** [c-sharpcorner.com](https://www.c-sharpcorner.com/UploadFile/8ef97c/C-Sharp-net-interview-questions-and-answers/)


## Q12: What are partial classes? ⭐⭐

**Answer:**

A **partial** class is only use to splits the definition of a class in two or more classes in a same source code file or more than one source files. You can create a class definition in multiple files but it will be compiled as one class at run time and also when you'll create an instance of this class so you can access all the methods from all source file with a same object. Partial classes can be create in the same namespace it's doesn't allowed to create a partial class in different namespace. 

🔗 **Source:** [c-sharpcorner.com](https://www.c-sharpcorner.com/UploadFile/8ef97c/C-Sharp-net-interview-questions-and-answers/)


## Q13: What are generics in C#? ⭐⭐

**Answer:**

**Generics** allow you to delay the specification of the data type of programming elements in a class or a method, until it is actually used in the program. In other words, generics allow you to write a class or method that can work with any data type.

🔗 **Source:** [c-sharpcorner.com](https://www.c-sharpcorner.com/UploadFile/8ef97c/C-Sharp-net-interview-questions-and-answers/)


## Q14: What you understand by Value types and Reference types in C#.Net? ⭐⭐

**Answer:**

In C# data types can be of two types: **Value Types** and **Reference Types**. Value type variables contain their object (or data) directly. If we copy one value type variable to another then we are actually making a copy of the object for the second variable. Value Type member will located into Stack and reference member will located in Heap always.  

🔗 **Source:** [stackoverflow.com](https://stackoverflow.com/questions/412813/when-to-use-arraylist-over-array-in-c)


## Q15: What is Serialization? ⭐⭐

**Answer:**

**Serialization** means saving the state of your object to secondary memory, such as a file.

1.  Binary serialization (Save your object data into binary format).  
2.  Soap Serialization (Save your object data into binary format; mainly used in network related communication).  
3.  XmlSerialization (Save your object data into an XML file).

🔗 **Source:** [c-sharpcorner.com](https://www.c-sharpcorner.com/UploadFile/8ef97c/C-Sharp-net-interview-questions-and-answers/)


## Q16: What is LINQ in C#? ⭐⭐

**Answer:**

**LINQ** stands for Language Integrated Query. LINQ has a great power of querying on any source of data. The data source could be collections of objects, database or XML files. We can easily retrieve data from any object that implements the `IEnumerable<T>` interface. 

🔗 **Source:** [c-sharpcorner.com](https://www.c-sharpcorner.com/UploadFile/8ef97c/C-Sharp-net-interview-questions-and-answers/)


## Q17: Can multiple catch blocks be executed? ⭐⭐

**Answer:**

No, Multiple catch blocks can't be executed. Once the proper catch code executed, the control is transferred to the finally block and then the code that follows the finally block gets executed.

🔗 **Source:** [guru99.com](https://www.guru99.com/c-sharp-interview-questions.html)


## Q18: What are Custom Exceptions? ⭐⭐

**Answer:**

Sometimes there are some errors that need to be handeled as per user requirements. Custom exceptions are used for them and are used defined exceptions.

🔗 **Source:** [guru99.com](https://www.guru99.com/c-sharp-interview-questions.html)


## Q19: Why can't you specify the accessibility modifier for methods inside the interface? ⭐⭐

**Answer:**

In an interface, we have virtual methods that do not have method definition. All the methods are there to be overridden in the derived class. That's why they all are public.

🔗 **Source:** [guru99.com](https://www.guru99.com/c-sharp-interview-questions.html)


## Q20: What are the different types of classes in C#? ⭐⭐

**Answer:**

The different types of class in C# are:

*   **Partial class** – Allows its members to be divided or shared with multiple .cs files. It is denoted by the keyword _Partial._
*   **Sealed class** – It is a class which cannot be inherited. To access the members of a sealed class, we need to create the object of the class.  It is denoted by the keyword _Sealed_.
*   **Abstract class** – It is a class whose object cannot be instantiated. The class can only be inherited. It should contain at least one method.  It is denoted by the keyword _abstract._
*   **Static class** – It is a class which does not allow inheritance. The members of the class are also static.  It is denoted by the keyword _static_. This keyword tells the compiler to check for any accidental instances of the static class.

🔗 **Source:** [softwaretestinghelp.com](https://www.softwaretestinghelp.com/c-sharp-interview-questions/)


## Q21: How is Exception Handling implemented in C#? ⭐⭐

**Answer:**

Exception handling is done using four keywords in C#:

*   **try** – Contains a block of code for which an exception will be checked.
*   **catch** – It is a program that catches an exception with the help of exception handler.
*   **finally** – It is a block of code written to execute regardless whether an exception is caught or not.
*   **Throw** – Throws an exception when a problem occurs.

🔗 **Source:** [softwaretestinghelp.com](https://www.softwaretestinghelp.com/c-sharp-interview-questions/)


## Q22: What is an Abstract Class? ⭐⭐

**Answer:**

An **Abstract class** is a class which is denoted by abstract keyword and can be used only as a Base class. An Abstract class should always be inherited. An instance of the class itself cannot be created. If we do not want any program to create an object of a class, then such classes can be made abstract.

Any method in the abstract class does not have implementations in the same class. But they must be implemented in the child class.

🔗 **Source:** [softwaretestinghelp.com](https://www.softwaretestinghelp.com/c-sharp-interview-questions/)


## Q23: Can you return multiple values from a function in C#? ⭐⭐

**Answer:**

Yes! Using output parameters. A return statement can be used for returning only one value from a function. However, using output parameters, you can return two values from a function.

🔗 **Source:** [tutorialspoint.com](https://www.tutorialspoint.com/csharp/csharp_interview_questions.htm)


## Q24: In how many ways you can pass parameters to a method? ⭐⭐

**Answer:**

There are three ways that parameters can be passed to a method:

*   **Value parameters** − This method copies the actual value of an argument into the formal parameter of the function. In this case, changes made to the parameter inside the function have no effect on the argument.
*   **Reference parameters** − This method copies the reference to the memory location of an argument into the formal parameter. This means that changes made to the parameter affect the argument.
*   **Output parameters** − This method helps in returning more than one value.

🔗 **Source:** [tutorialspoint.com](https://www.tutorialspoint.com/csharp/csharp_interview_questions.htm)


## Q25: What is namespace in C#? ⭐⭐

**Answer:**

A **namespace** is designed for providing a way to keep one set of names separate from another. The class names declared in one namespace does not conflict with the same class names declared in another.

🔗 **Source:** [tutorialspoint.com](https://www.tutorialspoint.com/csharp/csharp_interview_questions.htm)


## Q26: What are reference types in C#? ⭐⭐

**Answer:**

The **reference types** do not contain the actual data stored in a variable, but they contain a reference to the variables.

In other words, they refer to a memory location. Using multiple variables, the reference types can refer to a memory location. If the data in the memory location is changed by one of the variables, the other variable automatically reflects this change in value. Example of built-in reference types are: object, dynamic, and string.

🔗 **Source:** [tutorialspoint.com](https://www.tutorialspoint.com/csharp/csharp_interview_questions.htm)


## Q27: What are dynamic type variables in C#? ⭐⭐

**Answer:**

You can store any type of value in the dynamic data type variable. Type checking for these types of variables takes place at run-time.

🔗 **Source:** [tutorialspoint.com](https://www.tutorialspoint.com/csharp/csharp_interview_questions.htm)


## Q28: What are nullable types in C#? ⭐⭐

**Answer:**

C# provides a special data types, the **nullable types**, to which you can assign normal range of values as well as null values.

For example, you can store any value from -2,147,483,648 to 2,147,483,647 or null in a `Nullable<Int32>` variable. Similarly, you can assign true, false, or null in a `Nullable<bool>` variable.

🔗 **Source:** [tutorialspoint.com](https://www.tutorialspoint.com/csharp/csharp_interview_questions.htm)


## Q29: Why to use “finally” block in C#? ⭐⭐

**Answer:**

**Finally** block will be executed irrespective of exception. So while executing the code in try block when exception is occurred, control is returned to catch block and at last `finally` block will be executed. So closing connection to database / releasing the file handlers can be kept in `finally` block.

🔗 **Source:** [a4academics.com](http://a4academics.com/interview-questions/52-dot-net-interview-questions/417-c-oops-interview-questions-and-answers?showall=&start=1)


## Q30: Filter out the first 3 even numbers from the list using LINQ ⭐⭐

**Answer:**

```csharp
var evenNumbers = List
   .Where(x => x % 2 ==0)
   .Take(3)
```

🔗 **Source:** [medium.com/](https://medium.com/sears-israel/my-number-one-c-interview-question-39cdaac16c)


## Q31: What is the difference between Interface and Abstract Class? ⭐⭐⭐

**Answer:**

An interface in C# is like a contract. It defines a set of methods and properties that a class must implement. An interface can't have any implementation; it only declares the methods and properties that must be present in the implementing class.

On the other hand, an abstract class is a class that can have both implemented and unimplemented members (methods and properties). It can also have constructors and other types of members that interfaces cannot have. An abstract class is meant to be a base class that provides common functionality to derived classes, but it cannot be instantiated on its own.

In summary, an interface provides a contract for what a class must implement, while an abstract class can provide some implementation along with the ability to define abstract members that must be implemented by derived classes


## Q32: What is the difference between constant and readonly in c#? ⭐⭐⭐

**Answer:**

In C#, both const and readonly are used to create values that cannot be changed once they are assigned, but there are some key differences between them:

###Initialization:

Constants (const) must be initialized at the time of declaration. The value of a const is determined at compile time and cannot be changed afterwards.
Readonly fields (readonly) can be initialized either at the time of declaration or within the constructor of the class. The value of a readonly can be set at runtime, but once set, it cannot be changed.

###Scope:

Constants are implicitly static, which means they are available at the class level and can be accessed using the class name. They are treated as compile-time constants within the scope they are defined.
Readonly fields are instance members, which means they are tied to a specific instance of a class. Each instance of the class will have its own copy of a readonly field.

###Value Type:

Constants are always treated as compile-time constants. This means that the value of a const is substituted at compile time wherever it is used in the code.
Readonly fields are not treated as compile-time constants. Their value is evaluated at runtime and can vary based on the logic in the constructor.

In summary, const is used for values that are known at compile time and are the same for all instances of a class, while readonly is used for values that can vary by instance and are known only at runtime or when the class is initialized

## Q33: What is the difference between ref and out keywords? ⭐⭐⭐

**Answer:**

In C#, both `ref` and `out` are used to pass arguments to methods by reference, but they have some differences:

1. **Initialization**:
   - With `ref`, the variable must be initialized before it is passed to the method. This means that the value of the variable passed to the method must already be set.
   - With `out`, the variable does not need to be initialized before it is passed to the method. The method is responsible for initializing the variable before it assigns a value to it.

2. **Use Inside the Method**:
   - With `ref`, the method can read and write to the variable. Any changes made to the variable inside the method will be reflected outside the method.
   - With `out`, the method must assign a value to the variable before it exits. The method cannot read the initial value of the variable, so it must provide a new value for the variable.

3. **Compiler Requirement**:
   - When using `ref`, the variable must be initialized before it is passed to the method, or else the compiler will generate an error.
   - When using `out`, the variable does not need to be initialized before it is passed to the method, but the method must assign a value to the variable before it exits, or else the compiler will generate an error.

In summary, `ref` is used when you want to pass a variable to a method by reference and you want the method to be able to read and write to the variable, while `out` is used when you want the method to initialize the variable before it assigns a value to it.


## Q34:  What is extension method in C# and how to use them? ⭐⭐⭐

**Answer:**

An extension method in C# allows you to add methods to existing types without modifying the original type, its source code, or its dependencies. Extension methods are static methods defined in a static class and are used as if they were instance methods of the extended type. They are especially useful for adding new functionality to existing types, including types from third-party libraries or .NET framework types.

To define an extension method, follow these steps:

1. Create a static class to contain the extension methods.
2. Define a static method within the static class. The first parameter of the method specifies the type that the method operates on, preceded by the `this` modifier.
3. Use the `this` modifier followed by the type you are extending to specify that the method is an extension method for that type.

Here's an example of an extension method that adds a method called `IsWeekend` to the `DateTime` type to check if a given date falls on a weekend:

```csharp
using System;

public static class DateTimeExtensions
{
    public static bool IsWeekend(this DateTime date)
    {
        return date.DayOfWeek == DayOfWeek.Saturday || date.DayOfWeek == DayOfWeek.Sunday;
    }
}
```

To use this extension method, follow these steps:

1. Ensure the namespace containing the extension method class is included with a `using` directive.
2. Call the extension method on an instance of the extended type as if it were an instance method.

```csharp
using System;

public class Program
{
    public static void Main()
    {
        DateTime date = new DateTime(2024, 2, 24);
        Console.WriteLine(date.IsWeekend()); // Output: False
    }
}
```

In this example, the `IsWeekend` method appears to be an instance method of the `DateTime` type, even though it is defined in a separate static class.
