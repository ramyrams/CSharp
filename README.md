# CSharp


```cs
//Multiple-Variable Declarations
// Variable declarations--some with initializers, some without
int var3 = 7, var4, var5 = 3;
double var6, var7 = 6.52;
```

## Nullable Types
```cs
bool myBool = null;	//you'd get a compiler error.
DateTime myDate = null;	//you'd get a compiler error.

//these statements will compile just fine
bool? myNulableInt = null;
DateTime? myNullableDate = null;


//You can always convert a value type to a nullable type:
DateTime myDate = DateTime.Now;
DateTime? myNullableDate = myDate;

myDate = (DateTime) myNullableDate;


myDate = myNullableDate.Value;

```

## Class
### Declaring Classes & Creating Objects
```cs
public class Customer
{
    //Fields, properties, methods and events go here...
}

Customer object3 = new Customer();
Customer object4 = object3;

```

### Class Inheritance
public class Manager : Employee
{
    // Employee fields, properties, methods and events are inherited
    // New Manager fields, properties, methods and events go here...
}


## Constructors 

```cs
public class Taxi
{
    public bool isInitialized;
    public Taxi()
    {
        isInitialized = true;
    }
}

class TestTaxi
{
    static void Main()
    {
        Taxi t = new Taxi();
        Console.WriteLine(t.isInitialized);
    }
}
```


### Prevent a class from being instantiated by making the constructor private, as follows:
```cs
class NLog
{
    // Private Constructor:
    private NLog() { }

    public static double e = Math.E;  //2.71828...
}
```


```cs
public class Employee
{
    public int salary;

    public Employee(int annualSalary)
    {
        salary = annualSalary;
    }

    public Employee(int weeklySalary, int numberOfWeeks)
    {
        salary = weeklySalary * numberOfWeeks;
    }
}

Employee e1 = new Employee(30000);
Employee e2 = new Employee(500, 52);
```


### A constructor can use the base keyword to call the constructor of a base class. 
```cs
public class Manager : Employee
{
    public Manager(int annualSalary)
        : base(annualSalary)
    {
        //Add further instructions here.
    }
}
```


```cs
public Employee(int weeklySalary, int numberOfWeeks)
    : this(weeklySalary * numberOfWeeks)
{
}
```


## Destructors 

### a declaration of a destructor for the class Car:
```csclass Car
{
    ~Car()  // destructor
    {
        // cleanup statements...
    }
}
```

### The destructor implicitly calls Finalize on the base class of the object. 
```cs
protected override void Finalize()
{
    try
    {
        // Cleanup statements...
    }
    finally
    {
        base.Finalize();
    }
}
```

### creates three classes that make a chain of inheritance
```cs
class First
{
    ~First()
    {
        System.Diagnostics.Trace.WriteLine("First's destructor is called.");
    }
}

class Second : First
{
    ~Second()
    {
        System.Diagnostics.Trace.WriteLine("Second's destructor is called.");
    }
}

class Third : Second
{
    ~Third()
    {
        System.Diagnostics.Trace.WriteLine("Third's destructor is called.");
    }
}

class TestDestructors
{
    static void Main()
    {
        Third t = new Third();
    }

}
/* Output (to VS Output Window):
    Third's destructor is called.
    Second's destructor is called.
    First's destructor is called.
*/
```



## Object and Collection Initializers
```cs
class Cat
{
    // Auto-implemented properties.
    public int Age { get; set; }
    public string Name { get; set; }
}

Cat cat = new Cat { Age = 10, Name = "Fluffy" };
```

### Object Initializers with anonymous types
```cs
var pet = new { Age = 10, Name = "Fluffy" };

var productInfos =
    from p in products
    select new { p.ProductName, p.UnitPrice };
```	

### Object initializers with nullable types	
```cs
List<int> digits = new List<int> { 0, 1, 2, 3, 4, 5, 6, 7, 8, 9 };
List<int> digits2 = new List<int> { 0 + 1, 12 % 3, MakeInt() };

List<Cat> moreCats = new List<Cat>
{
    new Cat(){ Name = "Furrytail", Age=5 },
    new Cat(){ Name = "Peaches", Age=4 },
    null
};
```


### Access a Collection Class with foreach
```cs
Tokens f = new Tokens("This is a sample sentence.", new char[] {' ','-'});

// Display the tokens.
foreach (string item in f)
{
    System.Console.WriteLine(item);
}
```

## Nested Types
```cs
class Container
{
    class Nested
    {
        Nested() { }
    }
}
```

## Partial Classes and Methods
```cs
public partial class Employee
{
    public void DoWork()
    {
    }
}

public partial class Employee
{
    public void GoToLunch()
    {
    }
}
```

### At compile time, attributes of partial-type definitions are merged.
```cs
[SerializableAttribute]
partial class Moon { }

[ObsoleteAttribute]
partial class Moon { }
```

//For example, consider the following declarations:
```cs
partial class Earth : Planet, IRotate { }
partial class Earth : IRevolve { }

//They are equivalent to the following declarations:
class Earth : Planet, IRotate, IRevolve { }

### Partial Methods

```cs
// Definition in file1.cs
partial void onNameChanged();

// Implementation in file2.cs
partial void onNameChanged()
{
  // method body
}
```

## Anonymous Types

```cs
var v = new { Amount = 108, Message = "Hello" };

// Rest the mouse pointer over v.Amount and v.Message in the following
// statement to verify that their inferred types are int and string.
Console.WriteLine(v.Amount + v.Message);
```

```cs
var productQuery = 
    from prod in products
    select new { prod.Color, prod.Price };

foreach (var v in productQuery)
{
    Console.WriteLine("Color={0}, Price={1}", v.Color, v.Price);
}
```

```cs
var anonArray = new[] { new { name = "apple", diam = 4 }, new { name = "grape", diam = 1 }};
```



## Polymorphism
```cs
public class Shape
{
    // A few example members
    public int X { get; private set; }
    public int Y { get; private set; }
    public int Height { get; set; }
    public int Width { get; set; }

    // Virtual method
    public virtual void Draw()
    {
        Console.WriteLine("Performing base class drawing tasks");
    }
}

class Circle : Shape
{
    public override void Draw()
    {
        // Code to draw a circle...
        Console.WriteLine("Drawing a circle");
        base.Draw();
    }
}
class Rectangle : Shape
{
    public override void Draw()
    {
        // Code to draw a rectangle...
        Console.WriteLine("Drawing a rectangle");
        base.Draw();
    }
}
class Triangle : Shape
{
    public override void Draw()
    {
        // Code to draw a triangle...
        Console.WriteLine("Drawing a triangle");
        base.Draw();
    }
}

class Program
{
    static void Main(string[] args)
    {
        // Polymorphism at work #1: a Rectangle, Triangle and Circle
        // can all be used whereever a Shape is expected. No cast is
        // required because an implicit conversion exists from a derived 
        // class to its base class.
        System.Collections.Generic.List<Shape> shapes = new System.Collections.Generic.List<Shape>();
        shapes.Add(new Rectangle());
        shapes.Add(new Triangle());
        shapes.Add(new Circle());

        // Polymorphism at work #2: the virtual method Draw is
        // invoked on each of the derived classes, not the base class.
        foreach (Shape s in shapes)
        {
            s.Draw();
        }

        // Keep the console open in debug mode.
        Console.WriteLine("Press any key to exit.");
        Console.ReadKey();
    }

}

/* Output:
    Drawing a rectangle
    Performing base class drawing tasks
    Drawing a triangle
    Performing base class drawing tasks
    Drawing a circle
    Performing base class drawing tasks
 */
 ```
 
### Virtual Members
```cs
public class BaseClass
{
    public virtual void DoWork() { }
    public virtual int WorkProperty
    {
        get { return 0; }
    }
}
public class DerivedClass : BaseClass
{
    public override void DoWork() { }
    public override int WorkProperty
    {
        get { return 0; }
    }
}

DerivedClass B = new DerivedClass();
B.DoWork();  // Calls the new method.

BaseClass A = (BaseClass)B;
A.DoWork();  // Also calls the new method.

```

### Hiding Base Class Members with New Members
```cs
public class BaseClass
{
    public void DoWork() { WorkField++; }
    public int WorkField;
    public int WorkProperty
    {
        get { return 0; }
    }
}

public class DerivedClass : BaseClass
{
    public new void DoWork() { WorkField++; }
    public new int WorkField;
    public new int WorkProperty
    {
        get { return 0; }
    }
}


DerivedClass B = new DerivedClass();
B.DoWork();  // Calls the new method.

BaseClass A = (BaseClass)B;
A.DoWork();  // Calls the old method.

```

### Preventing Derived Classes from Overriding Virtual Members
```cs
public class A
{
    public virtual void DoWork() { }
}
public class B : A
{
    public override void DoWork() { }
}

public class C : B
{
    public sealed override void DoWork() { }
}

public class D : C
{
    public new void DoWork() { }
}
```
### Accessing Base Class Virtual Members from Derived Classes
```cs
public class Base
{
    public virtual void DoWork() {/*...*/ }
}
public class Derived : Base
{
    public override void DoWork()
    {
        //Perform Derived's work here
        //...
        // Call DoWork on base class
        base.DoWork();
    }
}
```


### Versioning with the Override and New Keywords
```cs

class GraphicsClass
{
    public virtual void DrawLine() { }
    public virtual void DrawPoint() { }
    public virtual void DrawRectangle() { }
}


class YourDerivedGraphicsClass : GraphicsClass
{
    public override void DrawRectangle() { }
}


base.DrawRectangle();


class YourDerivedGraphicsClass : GraphicsClass
{
    public new void DrawRectangle() { }
}


```

### Override and Method Selection
```cs
public class Derived : Base
{
    public override void DoWork(int param) { }
    public void DoWork(double param) { }
}

int val = 5;
Derived d = new Derived();
d.DoWork(val);  // Calls DoWork(double).

((Base)d).DoWork(val);  // Calls DoWork(int) on Derived.

```



```cs
// Define the base class, Car. The class defines two methods,
// DescribeCar and ShowDetails. DescribeCar calls ShowDetails, and each derived
// class also defines a ShowDetails method. The example tests which version of
// ShowDetails is selected, the base class method or the derived class method.
class Car
{
    public void DescribeCar()
    {
        System.Console.WriteLine("Four wheels and an engine.");
        ShowDetails();
    }

    public virtual void ShowDetails()
    {
        System.Console.WriteLine("Standard transportation.");
    }
}

// Define the derived classes.

// Class ConvertibleCar uses the new modifier to acknowledge that ShowDetails
// hides the base class method.
class ConvertibleCar : Car
{
    public new void ShowDetails()
    {
        System.Console.WriteLine("A roof that opens up.");
    }
}

// Class Minivan uses the override modifier to specify that ShowDetails
// extends the base class method.
class Minivan : Car
{
    public override void ShowDetails()
    {
        System.Console.WriteLine("Carries seven people.");
    }
}
```


## Abstract and Sealed Classes and Class Members

### Abstract Classes and Class Members
```cs

public abstract class A
{
    public abstract void DoWork(int i);
}

```



```cs
public class D
{
    public virtual void DoWork(int i)
    {
        // Original implementation.
    }
}

public abstract class E : D
{
    public abstract override void DoWork(int i);
}

public class F : E
{
    public override void DoWork(int i)
    {
        // New implementation.
    }
}
```


### Sealed Classes and Class Members
```cs
public sealed class D
{
    // Class members here.
}

public class D : C
{
    public sealed override void DoWork() { }
}

```

## Static Classes and Static Class Members
```cs
UtilityClass.MethodA();

```


### Static Members

```cs

public static class TemperatureConverter
{
    public static double CelsiusToFahrenheit(string temperatureCelsius)
    {
        return (temperatureCelsius * 9 / 5) + 32;;
    }

    public static double FahrenheitToCelsius(string temperatureFahrenheit)
    {
        return (fahrenheit - 32) * 5 / 9;;
    }
}

class TestTemperatureConverter
{
    static void Main()
    {
		double F, C = 0;
		F = TemperatureConverter.CelsiusToFahrenheit(Console.ReadLine());
        Console.WriteLine("Temperature in Fahrenheit: {0:F2}", F);
		
        C = TemperatureConverter.FahrenheitToCelsius(Console.ReadLine());
        Console.WriteLine("Temperature in Celsius: {0:F2}", C);
    }
}

```

```cs
public class Automobile
{
    public static int NumberOfWheels = 4;
    public static int SizeOfGasTank
    {
        get
        {
            return 15;
        }
    }
    public static void Drive() { }
    public static event EventType RunOutOfGas;

    // Other non-static fields and properties...
}

Automobile.Drive();
int i = Automobile.NumberOfWheels;

```
