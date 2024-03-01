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


## Q35: What is delegates in C# and uses of delegates? ⭐⭐⭐

**Answer:**

 In C#, a delegate is a type that represents references to methods with a particular parameter list and return type. Delegates are similar to function pointers in C and C++ but are type-safe and secure. They allow methods to be passed as parameters, returned from methods, and stored in variables.

### Uses of Delegates:

1. **Callback Mechanism:** Delegates are commonly used to implement callback mechanisms, where a method is called when a particular event occurs.

2. **Event Handling:** Delegates are extensively used in event handling to define and raise events.

3. **Asynchronous Programming:** Delegates can be used to invoke methods asynchronously, allowing for parallel execution of tasks.

4. **LINQ Queries:** Delegates are used in LINQ (Language Integrated Query) to filter, sort, and manipulate collections of objects.

5. **Decoupling Components:** Delegates help in decoupling components of an application, allowing for more flexible and maintainable code.

6. **Dynamic Method Invocation:** Delegates can be used to dynamically invoke methods at runtime, based on certain conditions.

Here's a basic example of a delegate declaration and its usage:

```csharp
// Declare a delegate
delegate int MathOperation(int x, int y);

// Define methods that match the delegate signature
static int Add(int x, int y) { return x + y; }
static int Subtract(int x, int y) { return x - y; }

// Usage
MathOperation addDelegate = Add;
MathOperation subtractDelegate = Subtract;

Console.WriteLine(addDelegate(5, 3));       // Output: 8
Console.WriteLine(subtractDelegate(5, 3));  // Output: 2
```

In this example, `MathOperation` is a delegate type that can reference methods with the signature `int MethodName(int x, int y)`. The `addDelegate` and `subtractDelegate` variables are assigned references to the `Add` and `Subtract` methods, respectively, and can be used to invoke these methods through the delegate.

## Q36: What is sealed class in C#? ⭐⭐⭐

 **Answer:**
In C#, a `sealed` class is a class that cannot be inherited. It is used to prevent other classes from deriving from it. When you declare a class as `sealed`, you are essentially saying that it is complete and cannot be extended further. 

Here's an example of a sealed class:

```csharp
sealed class SealedClass
{
    // Class members and methods
}
```

You cannot inherit from a sealed class, so the following code would result in a compilation error:

```csharp
class DerivedClass : SealedClass  // Compilation error: Cannot derive from sealed type 'SealedClass'
{
    // Class members and methods
}
```

Sealing a class can be useful when you want to ensure that the class behavior is not modified or extended by other classes. It also allows the compiler to optimize certain aspects of the sealed class, as it knows that no other class will inherit from it.

## Q37: What is the difference between overloading and overriding? ⭐⭐⭐

 **Answer:**
In C#, overloading and overriding are both mechanisms to change the behavior of methods, but they are used in different contexts and have different purposes:

1. **Method Overloading:**
   - Method overloading is a feature that allows a class to have multiple methods with the same name but different signatures within the same scope.
   - Signatures can differ in the number of parameters, the type of parameters, or the order of parameters.
   - Overloaded methods are differentiated based on their signatures at compile time, and the appropriate method is called based on the arguments provided.
   - Overloading is used to provide multiple ways to call a method with different parameters, making the code more readable and flexible.

   Example of method overloading:
   ```csharp
   class MathOperations
   {
       public int Add(int x, int y)
       {
           return x + y;
       }

       public double Add(double x, double y)
       {
           return x + y;
       }
   }
   ```

2. **Method Overriding:**
   - Method overriding is a feature that allows a subclass to provide a specific implementation of a method that is already provided by its superclass.
   - The overridden method in the subclass must have the same signature (name, parameters, and return type) as the method in the superclass.
   - Overriding is used to provide a specialized implementation of a method in a subclass, allowing for polymorphic behavior.

   Example of method overriding:
   ```csharp
   class Shape
   {
       public virtual void Draw()
       {
           Console.WriteLine("Drawing a shape");
       }
   }

   class Circle : Shape
   {
       public override void Draw()
       {
           Console.WriteLine("Drawing a circle");
       }
   }
   ```

In summary, method overloading allows multiple methods with the same name but different signatures, while method overriding allows a subclass to provide a specific implementation of a method defined in its superclass.

## Q38: What is difference between Throw Exception and Throw Clause? ⭐⭐⭐

 **Answer:**
In C#, "throw exception" and "throw clause" are not standard terminologies. It seems there might be a misunderstanding or confusion regarding these terms. Here's a clarification:

1. **Throw Clause:** In C#, the `throw` keyword is used to explicitly throw an exception. When you use the `throw` keyword, you are throwing an exception object. This is commonly referred to as throwing an exception or using a throw clause. For example:

   ```csharp
   throw new Exception("Something went wrong");
   ```

2. **Catch Clause:** On the other hand, a catch clause is used to catch exceptions that are thrown in a try block. When an exception is thrown, the runtime looks for a catch block that can handle that exception. If it finds one, it executes the code in that catch block. For example:

   ```csharp
   try
   {
       // Code that might throw an exception
   }
   catch (Exception ex)
   {
       // Handle the exception
       Console.WriteLine("An error occurred: " + ex.Message);
   }
   finally
   {
		// It --RUN ALWAYS
   }
   ```

In summary, the `throw` keyword is used to throw an exception, and a catch clause is used to catch and handle exceptions that are thrown. There isn't a direct comparison between "throw exception" and "throw clause" because "throw clause" is not a standard term in C#.

## Q39: What is the difference between Equality Operator (==) and Equals() Method in C#? ⭐⭐⭐

 **Answer:**
In C#, the equality operator (`==`) and the `Equals()` method are used for comparison, but they behave differently depending on the context and the types being compared:

1. **Equality Operator (`==`):**
   - The equality operator (`==`) is used to compare the equality of two objects or values.
   - For reference types (classes), the `==` operator compares the references (memory addresses) of the objects. It checks if two references point to the same object in memory.
   - For value types (structs), the `==` operator compares the values of the objects. It checks if the values of two objects are equal.

   Example:
   ```csharp
   string str1 = "hello";
   string str2 = "hello";
   Console.WriteLine(str1 == str2);  // Output: True
   ```

2. **`Equals()` Method:**
   - The `Equals()` method is used to compare the contents or values of two objects.
   - The `Equals()` method is a virtual method defined in the `Object` class, so all classes inherit it. Classes can override this method to provide their own implementation of equality comparison.
   - The default implementation of `Equals()` in the `Object` class compares references for reference types, similar to the `==` operator.

   Example:
   ```csharp
   string str1 = "hello";
   string str2 = "hello";
   Console.WriteLine(str1.Equals(str2));  // Output: True
   ```

   Note: Some types, like `string`, override the `Equals()` method to compare values instead of references. So, for `string` objects, using `Equals()` is equivalent to using the `==` operator for value comparison.

In summary, the `==` operator compares references for reference types and values for value types, while the `Equals()` method can be overridden by classes to provide custom equality comparison logic and is used for value comparison by some types like `string`.

## Q40: What is Virtual Method in C#? ⭐⭐⭐

 **Answer:**
In C#, a virtual method is a method that is declared in a base class and can be overridden in derived classes. The `virtual` keyword is used to declare a method as virtual in the base class, and the `override` keyword is used in the derived class to provide a specific implementation of the virtual method. This allows for polymorphic behavior, where the method called is determined by the runtime type of the object.

Here's an example to illustrate the concept of virtual methods:

```csharp
class Animal
{
    public virtual void MakeSound()
    {
        Console.WriteLine("Animal makes a sound");
    }
}

class Dog : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("Dog barks");
    }
}

class Cat : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("Cat meows");
    }
}

class Program
{
    static void Main()
    {
        Animal animal1 = new Dog();
        Animal animal2 = new Cat();

        animal1.MakeSound(); // Output: Dog barks
        animal2.MakeSound(); // Output: Cat meows
    }
}
```

In this example, the `Animal` class defines a virtual method `MakeSound()`. The `Dog` and `Cat` classes override this method with their specific implementations. When the `MakeSound()` method is called on an instance of `Animal`, the actual implementation that is executed is determined by the runtime type of the object (`Dog` or `Cat`), demonstrating polymorphic behavior.

## Q41: What are the uses of “using” in C# ⭐⭐⭐

 **Answer:**
In C#, the `using` keyword has several important uses:

1. **Namespace Importing:** The `using` directive is used to import namespaces in C#. It allows you to use types from a particular namespace without specifying the fully qualified name of the type every time. For example:

   ```csharp
   using System;
   ```

   This allows you to use types from the `System` namespace, such as `Console`, without writing `System.Console` every time.

2. **Resource Management (IDisposable):** The `using` statement is used to ensure that objects that implement the `IDisposable` interface are properly disposed of after use. The `using` statement creates a scope within which the object is valid, and at the end of the scope, the `Dispose()` method of the object is called automatically. For example:

   ```csharp
   using (var file = new FileStream("file.txt", FileMode.Open))
   {
       // Read or write to the file
   } // file.Dispose() is called automatically here
   ```

3. **Alias Directives:** The `using` directive can also be used to create alias directives, which allow you to refer to a type or namespace with a different name. This can be useful to avoid name conflicts. For example:

   ```csharp
   using Project = CompanyName.ProjectName;
   ```

   This allows you to use `Project` instead of `CompanyName.ProjectName` in your code.

4. **Static Class Access:** If you have a static class with static members, you can use a `using static` directive to avoid specifying the class name each time you access a static member. For example:

   ```csharp
   using static System.Math;
   ```

   This allows you to use `Sin` and `Cos` directly instead of `Math.Sin` and `Math.Cos`.

Overall, the `using` keyword plays a crucial role in simplifying the use of namespaces, managing resources, creating aliases, and accessing static members in C#.

## Q42: Explain Anonymous type in C# ⭐⭐⭐

 **Answer:**
In C#, an anonymous type is a type that is defined dynamically at compile time without explicitly defining a class. Anonymous types are typically used to encapsulate a set of read-only properties into a single object without the need to define a formal class. Anonymous types are created using the `new` keyword along with an object initializer syntax.

Here's a basic example of creating an anonymous type:

```csharp
var person = new { Name = "John", Age = 30 };
Console.WriteLine($"Name: {person.Name}, Age: {person.Age}");
```

In this example, `person` is an anonymous type with two properties: `Name` and `Age`. The compiler infers the property names and types based on the initializer values provided.

Anonymous types are useful for temporary data structures and are often used in LINQ queries to project query results into a new shape. For example:

```csharp
var query = from p in people
            select new { p.Name, p.Age };
```

In this LINQ query, `select new { p.Name, p.Age }` creates an anonymous type with properties `Name` and `Age` based on the `Name` and `Age` properties of objects in the `people` collection.

Anonymous types have the following characteristics:

- They are read-only and cannot be modified once created.
- They have compiler-generated names, which makes them inaccessible outside the method or scope where they are defined.
- They override the `Equals` and `GetHashCode` methods to provide value-based equality comparisons.
- They can contain only public properties.

While anonymous types are convenient for certain scenarios, they are limited in their usage and are not suitable for all situations. They are best used for short-lived objects with a limited scope where the properties are known at compile time.

## Q43: What is Reflection in C#.Net? ⭐⭐⭐

 **Answer:**
Reflection in C# allows you to inspect and manipulate types, methods, properties, and other members of your program at runtime. It provides the ability to dynamically create instances of types, invoke methods, access properties, and perform other operations that would normally require compile-time knowledge of the types involved.

Here are some common uses of reflection in C#:

1. **Inspecting Types:** You can use reflection to examine the metadata of types, such as class hierarchies, interfaces implemented, methods, and properties.

2. **Dynamic Instantiation:** Reflection allows you to create instances of types dynamically, even if the type is not known at compile time.

3. **Invoking Methods:** You can use reflection to invoke methods on types dynamically, including methods with different signatures.

4. **Accessing and Modifying Properties:** Reflection enables you to access and modify properties of objects at runtime.

5. **Dynamic Loading of Types:** Reflection can be used to dynamically load types from assemblies, allowing for more flexible and extensible applications.

Here's a simple example of using reflection to create an instance of a type and invoke a method:

```csharp
using System;
using System.Reflection;

public class MyClass
{
    public void MyMethod()
    {
        Console.WriteLine("Hello, Reflection!");
    }
}

public class Program
{
    public static void Main()
    {
        Type type = typeof(MyClass);
        object instance = Activator.CreateInstance(type);
        
        MethodInfo method = type.GetMethod("MyMethod");
        method.Invoke(instance, null);
    }
}
```

In this example, the `typeof(MyClass)` statement gets the `Type` object representing the `MyClass` type. We then use `Activator.CreateInstance` to create an instance of `MyClass`. Next, we use `GetMethod` to get the `MethodInfo` object representing the `MyMethod` method, and finally, we use `Invoke` to invoke the method on the instance.

## Q44: What is difference between constants and readonly? ⭐⭐⭐

 **Answer:**
In C#, constants (`const`) and readonly fields (`readonly`) are both used to define values that cannot be changed. However, there are some key differences between them:

1. **Value Assignment:**
   - Constants must be assigned a value at the time of declaration and cannot be changed afterward.
   - Readonly fields can be assigned a value either at the time of declaration or within the constructor of the class. Once assigned, their value cannot be changed.

2. **Scope:**
   - Constants are implicitly static and are always considered to be static members of their containing type. They are also implicitly `const` and can only be defined at the class level.
   - Readonly fields can be static or instance-level and can be defined at any level (class, struct, or interface).

3. **Usage:**
   - Constants are used for values that are known at compile time and will not change throughout the lifetime of the program. They are replaced with their literal values at compile time.
   - Readonly fields are used when the value needs to be calculated at runtime or when the value may change during the lifetime of the program, but you want to restrict where and how it can be changed.

4. **Compilation:**
   - Constants are replaced with their literal values at compile time wherever they are used in the code.
   - Readonly fields retain their reference to the object or value they were assigned, and the actual value is accessed at runtime.

Here's an example to illustrate the difference:

```csharp
public class MyClass
{
    public const int MyConstant = 100;
    public readonly int MyReadOnlyField;

    public MyClass(int value)
    {
        MyReadOnlyField = value;
    }
}
```

In this example, `MyConstant` is a constant with a value of `100`, which is known at compile time and cannot be changed. `MyReadOnlyField` is a readonly field that can be assigned a value in the constructor, but once assigned, it cannot be changed.

## Q45: Explain Code compilation in C# ⭐⭐⭐

 **Answer:**
In C#, code compilation is the process of translating C# source code into an executable form that can be run by the computer. The compilation process involves several steps:

1. **Preprocessing:** In this step, the preprocessor directives (e.g., `#define`, `#if`, `#endif`) in the source code are processed. These directives are used to conditionally include or exclude portions of code or to define constants.

2. **Lexical Analysis (Lexing):** The source code is broken down into tokens, such as keywords, identifiers, literals, and operators. This step is performed by the lexer (lexical analyzer).

3. **Syntax Analysis (Parsing):** The tokens produced by the lexer are analyzed to ensure that they conform to the rules of the C# language syntax. This step is performed by the parser.

4. **Semantic Analysis:** The compiler checks the semantics of the code, such as type checking, to ensure that the code is semantically correct. This step also resolves references to variables, methods, and types.

5. **Intermediate Code Generation:** The compiler generates an intermediate representation of the code, such as Intermediate Language (IL) in .NET. IL is a platform-independent code that can be executed by the Common Language Runtime (CLR).

6. **Optimization:** The compiler performs various optimizations on the intermediate code to improve performance, such as removing dead code, inlining methods, and reordering instructions.

7. **Code Generation:** Finally, the compiler generates machine code (e.g., native code or Just-In-Time compiled code) from the optimized intermediate code. This machine code is specific to the target platform and can be executed by the CPU.

8. **Linking (for multi-file programs):** In some cases, if the program consists of multiple source files, the compiler may also perform linking to combine the compiled code into a single executable or library.

The compiled code can then be executed by the runtime environment (e.g., CLR in .NET) to produce the desired output.

## Q46: What is the difference between Virtual method and Abstract method? ⭐⭐⭐

 **Answer:**
In object-oriented programming, both virtual and abstract methods play important roles in defining the behavior of classes, but they have different purposes and characteristics.

1. **Virtual Method:**
   - A virtual method is a method in a base class that can be overridden in derived classes.
   - It provides a default implementation in the base class, which can be optionally overridden in derived classes.
   - Virtual methods allow for polymorphism, where the method called is determined by the type of the object at runtime.
   - The `virtual` keyword is used to declare a method as virtual in the base class.

Example:
```csharp
public class Animal
{
    public virtual void MakeSound()
    {
        Console.WriteLine("Some sound");
    }
}

public class Dog : Animal
{
    public override void MakeSound()
    {
        Console.WriteLine("Woof!");
    }
}
```

2. **Abstract Method:**
   - An abstract method is a method in an abstract class that has no implementation in the base class.
   - It must be overridden in derived classes to provide the implementation.
   - Abstract methods are used to define a common interface for all derived classes, but the specific implementation is left to each derived class.
   - The `abstract` keyword is used to declare a method as abstract in the base class.

Example:
```csharp
public abstract class Shape
{
    public abstract double Area();
}

public class Circle : Shape
{
    public double Radius { get; set; }

    public override double Area()
    {
        return Math.PI * Radius * Radius;
    }
}
```

In summary, virtual methods provide a default implementation that can be overridden, while abstract methods require derived classes to provide their own implementations.

## Q47: What is a Destructor in C#? ⭐⭐⭐

 **Answer:**
In C#, a destructor is a special method in a class that is automatically called when an object is destroyed or goes out of scope. It is used to release resources or perform cleanup operations before the object is removed from memory. 

In C#, the destructor is defined using the tilde (~) followed by the class name, and it cannot have any parameters or modifiers. Unlike constructors, destructors cannot be called explicitly; they are invoked automatically by the garbage collector when the object is no longer reachable.

Here's an example of a destructor in C#:

```csharp
using System;

public class MyClass
{
    // Constructor
    public MyClass()
    {
        Console.WriteLine("Object created");
    }

    // Destructor
    ~MyClass()
    {
        Console.WriteLine("Object destroyed");
    }
}

class Program
{
    static void Main()
    {
        MyClass obj = new MyClass();
        // The object is destroyed automatically when it goes out of scope
    }
}
```

In the above example, the destructor in `MyClass` will be called automatically when the `obj` object is no longer reachable. It's important to note that in C#, destructors are less commonly used compared to constructors, as C# provides automatic memory management through the garbage collector.

## Q48: What is the difference between dynamic type variables and object type variables? ⭐⭐⭐

 **Answer:**
In C#, both `dynamic` and `object` types are used to handle situations where the type of a variable is not known at compile time, but they have different behaviors and use cases:

1. **Dynamic Type:**
   - The `dynamic` type was introduced in C# 4.0 and is used to represent any type at runtime.
   - Variables declared as `dynamic` bypass compile-time type checking. Instead, type checking is performed at runtime, which can lead to runtime errors if the types are not compatible.
   - Using `dynamic` can simplify code in certain scenarios, such as when working with COM objects, dynamic languages, or when dealing with complex type inference scenarios.
   - Example:
     ```csharp
     dynamic dynamicVariable = 10;
     dynamicVariable = "Hello";
     ```

2. **Object Type:**
   - The `object` type is a reference type that can refer to any other type in C#. It is the base type for all other types in the C# type system.
   - Variables declared as `object` require explicit casting to access their members or convert them to other types, which can lead to less readable code.
   - Using `object` is useful when you need to store objects of different types in a collection or when the specific type is not known at compile time.
   - Example:
     ```csharp
     object obj = 10;
     obj = "Hello";
     ```

In summary, `dynamic` is used when you need to work with types that are resolved at runtime, while `object` is used when you need a reference to an object of any type. Using `dynamic` can make your code more flexible but less type-safe, while `object` provides more type safety at the cost of less flexibility.

## Q49: How encapsulation is implemented in C#? ⭐⭐⭐

 **Answer:**
Encapsulation in C# is implemented using access modifiers and properties. Encapsulation is the principle of bundling the data (fields) and methods (functions) that operate on the data into a single unit (class) and restricting access to some of the object's components. This allows for better control over the access to the data, which helps prevent accidental modification and ensures data integrity. 

Access Modifiers:
- C# provides access modifiers like `public`, `private`, `protected`, and `internal` to control the visibility of classes, methods, and variables.
- `public`: The member is accessible from any other class.
- `private`: The member is accessible only within the same class.
- `protected`: The member is accessible within the same class and by derived classes.
- `internal`: The member is accessible within the same assembly (i.e., .dll or .exe file).

Properties:
- Properties in C# are used to encapsulate fields by providing a controlled way to access or modify them.
- They allow for additional logic to be executed when getting or setting the value of a field (e.g., validation).
- Properties are declared using a `get` accessor (to retrieve the value) and a `set` accessor (to set the value).

Example of encapsulation in C#:

```csharp
public class Person
{
    private string name; // private field

    public string Name // public property
    {
        get { return name; } // get accessor
        set { name = value; } // set accessor
    }

    private int age; // private field

    public int Age // public property
    {
        get { return age; } // get accessor
        set { age = value; } // set accessor
    }
}

class Program
{
    static void Main()
    {
        Person person = new Person();
        person.Name = "John"; // set the Name property
        person.Age = 30; // set the Age property

        Console.WriteLine("Name: " + person.Name); // get the Name property
        Console.WriteLine("Age: " + person.Age); // get the Age property
    }
}
```

In the above example, the `name` and `age` fields are encapsulated within the `Person` class, and access to them is controlled through properties. This ensures that the `name` and `age` can only be accessed and modified through the defined property accessors, providing encapsulation.

## Q50: What is scope of a Internal member variable of a C# class? ⭐⭐⭐

 **Answer:**
In C#, the `internal` access modifier is used to specify that a member (such as a variable, method, or property) is accessible within the same assembly (i.e., .dll or .exe file), but not outside of it. 

When a member variable is declared as `internal` within a class, it means that the variable can be accessed from other classes within the same assembly, including classes in the same namespace or different namespaces. However, it cannot be accessed from classes in other assemblies.

Example:

```csharp
// Assembly1.dll
using System;

namespace MyNamespace
{
    public class MyClass
    {
        internal int internalVariable = 10;

        public void DisplayInternalVariable()
        {
            Console.WriteLine("Internal Variable: " + internalVariable);
        }
    }
}
```

In the above example, the `internalVariable` is accessible within the `MyClass` and any other class within the same assembly (Assembly1.dll). However, if you were to create another assembly (e.g., Assembly2.dll) and try to access `internalVariable` from a class in that assembly, you would get a compilation error.

## Q51: What is the use of Null Coalescing Operator (??) in C#? ⭐⭐⭐

 **Answer:**
The null-coalescing operator (`??`) in C# is used to provide a default value for nullable types or reference types. It returns the left-hand operand if the operand is not null; otherwise, it returns the right-hand operand.

Syntax:
```csharp
result = expression1 ?? expression2;
```

- `expression1`: The value to be returned if it is not null.
- `expression2`: The value to be returned if `expression1` is null.

Example with reference types:
```csharp
string name = null;
string displayName = name ?? "Guest";
Console.WriteLine(displayName); // Output: Guest
```

In this example, if `name` is `null`, the `??` operator returns the default value `"Guest"`, which is then assigned to `displayName`.

Example with nullable types:
```csharp
int? x = null;
int y = x ?? -1;
Console.WriteLine(y); // Output: -1
```

In this example, if `x` is `null`, the `??` operator returns the default value `-1`, which is then assigned to `y`.

The null-coalescing operator is useful for providing default values or handling null values in a concise and readable way.

## Q52: Given an array of ints, write a C# method to total all the values that are even numbers. ⭐⭐⭐

 **Answer:**


## Q53: What is the output of the program below? Explain your answer. ⭐⭐⭐

**Questions Details:**

Consider:
```csharp
delegate void Printer();

static void Main()
{
        List<Printer> printers = new List<Printer>();
        int i=0;
        for(; i < 10; i++)
        {
            printers.Add(delegate { Console.WriteLine(i); });
        }

        foreach (var printer in printers)
        {
            printer();
        }
}
```


 **Answer:**


## Q54: Refactor the code ⭐⭐⭐

**Questions Details:**

```csharp
class ClassA
{
  public ClassA() { }

  public ClassA(int pValue) {  }
}

// client program
class Program
{
  static void Main(string[] args)
  {
    ClassA refA = new ClassA();
  }
}
```
Is there a way to modify `ClassA` so that you can you call the constructor with parameters, when the Main method is called, without creating any other new instances of the `ClassA`?




 **Answer:**


## Q55: What is lambda expressions in C#? ⭐⭐⭐

 **Answer:**


## Q56: What is an anonymous function in C#? ⭐⭐⭐

 **Answer:**


## Q57: What is marshalling and why do we need it? ⭐⭐⭐⭐

 **Answer:**


## Q58: What is the difference between dispose and finalize methods in c#? ⭐⭐⭐⭐

 **Answer:**


## Q59: What is difference between late binding and early binding in C#? ⭐⭐⭐⭐

 **Answer:**


## Q60: What is the Constructor Chaining in C#? ⭐⭐⭐⭐

 **Answer:**


## Q61: What is Indexer in C#? ⭐⭐⭐⭐

 **Answer:**


## Q62: Name difference between "is" and "as" operator in C# ⭐⭐⭐⭐

 **Answer:**


## Q63: What is an Object Pool in .Net? ⭐⭐⭐⭐

 **Answer:**


## Q64: When to use ArrayList over array[] in c#? ⭐⭐⭐⭐

 **Answer:**


## Q65: What are the differences between a multidimensional array and an array of arrays in C#? ⭐⭐⭐⭐

**Questions Details:**

What are the differences between multidimensional arrays `double[,]` and array-of-arrays `double[][]` in C#?


 **Answer:**


## Q66: Describe the accessibility modifier "protected internal". ⭐⭐⭐⭐

 **Answer:**


## Q67: What are the different ways a method can be overloaded? ⭐⭐⭐⭐

 **Answer:**


## Q68: What are pointer types in C#? ⭐⭐⭐⭐

 **Answer:**


## Q69: What is scope of a Protected Internal member variable of a C# class? ⭐⭐⭐⭐

 **Answer:**


## Q70: Can you create a function in C# which can accept varying number of arguments? ⭐⭐⭐⭐

 **Answer:**


## Q71: Is operator overloading supported in C#? ⭐⭐⭐⭐

 **Answer:**


## Q72: What is the use of conditional preprocessor directive in C#? ⭐⭐⭐⭐

 **Answer:**


## Q73: What is the difference between System.ApplicationException class and System.SystemException class? ⭐⭐⭐⭐

 **Answer:**


## Q74: Can we have only “try” block without “catch” block in C#? ⭐⭐⭐⭐

 **Answer:**


## Q75: In try block if we add return statement whether finally block is executed in C#? ⭐⭐⭐⭐

 **Answer:**


## Q76: What's the difference between StackOverflowError and OutOfMemoryError? ⭐⭐⭐⭐

 **Answer:**


## Q77: What are the uses of delegates in C#? ⭐⭐⭐⭐

 **Answer:**


## Q78: Why to use lock statement in C#? ⭐⭐⭐⭐

 **Answer:**


## Q79: Can Multiple Inheritance implemented in C# ? ⭐⭐⭐⭐

 **Answer:**


## Q80: What is the output of the short program below? Explain your answer. ⭐⭐⭐⭐

**Questions Details:**

Consider:
```csharp
class Program {
  static String location;
  static DateTime time;
 
  static void Main() {
    Console.WriteLine(location == null ? "location is null" : location);
    Console.WriteLine(time == null ? "time is null" : time.ToString());
  }
}
```


 **Answer:**


## Q81: Is the comparison of time and null in the if statement below valid or not? Why or why not? ⭐⭐⭐⭐

**Questions Details:**

Consider:
```csharp
static DateTime time;
/* ... */
if (time == null)
{
	/* do something */
}
```


 **Answer:**


## Q82: What is the output of the program below? Explain your answer. ⭐⭐⭐⭐

**Questions Details:**

Consider:
```csharp
class Program {
  private static string result;
 
  static void Main() {
    SaySomething();
    Console.WriteLine(result);
  }
 
  static async Task<string> SaySomething() {
    await Task.Delay(5);
    result = "Hello world!";
    return “Something”;
  }
}
```
Also, would the answer change if we were to replace `await Task.Delay(5);` with `Thread.Sleep(5)`? Why or why not?


 **Answer:**


## Q83: What is the output of the program below? ⭐⭐⭐⭐

**Questions Details:**

Consider:
```csharp
public class TestStatic {
 public static int TestValue;

 public TestStatic() {
  if (TestValue == 0) {
   TestValue = 5;
  }
 }
 static TestStatic() {
  if (TestValue == 0) {
   TestValue = 10;
  }

 }

 public void Print() {
  if (TestValue == 5) {
   TestValue = 6;
  }
  Console.WriteLine("TestValue : " + TestValue);

 }
}

public void Main(string[] args) {

 TestStatic t = new TestStatic();
 t.Print();
}
```


 **Answer:**


## Q84: What is the "yield" keyword used for in C#? ⭐⭐⭐⭐

**Questions Details:**

Consider:
```csharp
IEnumerable<object> FilteredList()
{
    foreach( object item in FullList )
    {
        if( IsItemInPartialList( item )
            yield return item;
    }
}
```
Could you explain what does the `yield` keyword do there?


 **Answer:**


## Q85: What interface should your data structure implement to make the "Where" method work? ⭐⭐⭐⭐

 **Answer:**


## Q86: IEnumerable vs List - What to Use? How do they work? ⭐⭐⭐⭐

 **Answer:**


## Q87: What is the difference between Func<string,string> and delegate? ⭐⭐⭐⭐

**Questions Details:**

Consider:
```csharp
Func<string, string> convertMethod = lambda; // A
public delegate string convertMethod(string value); // B
```
Are they both delegates? What's the difference?


 **Answer:**


## Q88: Explain the difference between Select and Where ⭐⭐⭐⭐

**Questions Details:**

Consider:
```csharp
ContextSet().Select(x=> x.FirstName == "John") // A
ContextSet().Where(x=> x.FirstName == "John") // B
```
When should I use .Select vs .Where?


 **Answer:**


## Q89: Explain what is short-circuit evaluation in C# ⭐⭐⭐⭐

 **Answer:**


## Q90: What is the best practice to have best performance using Lazy<T> objects?  ⭐⭐⭐⭐

 **Answer:**


## Q91: What are the differences between IEnumerable and IQueryable? ⭐⭐⭐⭐⭐

 **Answer:**


## Q92: What is deep or shallow copy concept in C#? ⭐⭐⭐⭐⭐

 **Answer:**


## Q93: What's the difference between the System.Array.CopyTo() and System.Array.Clone()? ⭐⭐⭐⭐⭐

 **Answer:**


## Q94: What is multicast delegate in C#? ⭐⭐⭐⭐⭐

 **Answer:**


## Q95: What is the method MemberwiseClone() doing? ⭐⭐⭐⭐⭐

 **Answer:**


## Q96: List some different ways for equality check in .Net ⭐⭐⭐⭐⭐

 **Answer:**


## Q97: What are circular references? ⭐⭐⭐⭐⭐

 **Answer:**


## Q98: What is jagged array in C#.Net and when to prefer jagged arrays over multi-dimensional arrays? ⭐⭐⭐⭐⭐

 **Answer:**


## Q99: Could you explain the difference between destructor, dispose and finalize method? ⭐⭐⭐⭐⭐

 **Answer:**


## Q100: Can you create sealed abstract class in C#? ⭐⭐⭐⭐⭐

 **Answer:**


## Q101: What is a preprocessor directives in C#? ⭐⭐⭐⭐⭐

 **Answer:**


## Q102: What is the use of static constructors? ⭐⭐⭐⭐⭐

 **Answer:**


## Q103: Calculate the circumference of the circle ⭐⭐⭐⭐⭐

**Questions Details:**

Given an instance circle of the following class:

```csharp
public sealed class Circle {
  private double radius;
  
  public double Calculate(Func<double, double> op) {
    return op(radius);
  }
}

write code to calculate the circumference of the circle, without modifying the `Circle` class itself.
```


 **Answer:**


## Q104: What are the benefits of a Deferred Execution in LINQ? ⭐⭐⭐⭐⭐

 **Answer:**


## Q105: What is the difference between lambdas and delegates? ⭐⭐⭐⭐⭐

 **Answer:**


## Q106: Could you explain the difference between Func vs. Action vs. Predicate? ⭐⭐⭐⭐⭐

 **Answer:**


## Q107: Explain the difference between IQueryable, ICollection, IList & IDictionary interfaces? ⭐⭐⭐⭐⭐

 **Answer:**


## Q108:  in C#, when should we use abstract classes instead of interfaces with extension methods? ⭐⭐⭐⭐⭐

 **Answer:**


## Q109: Can you add extension methods to an existing static class? ⭐⭐⭐⭐⭐

 **Answer:**


## Q110: Implement the "Where" method in C# ⭐⭐⭐⭐⭐

 **Answer:**


## Q111: What is the “volatile” keyword used for? ⭐⭐⭐⭐⭐

 **Answer:**


## Q112: Explain what is weak reference in C#? ⭐⭐⭐⭐⭐

 **Answer:**
