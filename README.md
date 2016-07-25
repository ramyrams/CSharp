<a name="README">[<img src="https://s3-us-west-2.amazonaws.com/testdrivenlearningbucket/CSHARP.png" width="200px" height="200px" />](https://github.com/MartinChavez/Learn-CSharp)</a>

#TOC 
* [Types, Storage, and Variables](#Types, Storage, and Variables)
* [Classes](#classes)
* [Inheritance](#inheritance)
* [Interfaces](#interfaces)
* [Methods](#methods)
* [Expressions and Operators](#expressions-and-operators)
* [Statements](#statements)
* [Structs](#structs)
* [Enumerations](#enumerations)
* [Arrays](#arrays)
* [Delegates](#delegates)
* [Events](#events)
* [Conversions](#conversions)
* [Generics](#generics)
* [Enumerators and Iterators](#enumerators-and-iterators)
* [Exceptions](#exceptions)
* [Preprocessor Directives](#preprocessor-directives)
* [Reflection and Attributes ](#reflection-and-attributes )
* [Dynamic Binding](#dynamic-binding)
* [Disposal and Garbage Collection](#disposal-and-garbage-collection)
* [Serialization](#serialization)
* [Application Domains](#application-domains)
* [Collections](#collections)
* [Lambda](#lambda)
* [Asynchronous Programming](#asynchronous-programming)
* [Concurrency & Asynchrony](#concurrency-&-Asynchrony)
* [Native and COM Interoperability](#native-and-com-interoperability)
* [Parallel Programming](#parallel-programming)
* [Advanced Threading](#advanced-threading)
* [Security](#security)
* [Reflection and Metadata](#reflection-and-metadata)
* [Networking](#networking)
* [Streams and I/O](#streams-and-I/O)
* [Diagnostics and Code Contracts](#diagnostics-and-code-Contracts)

# Types, Storage, and Variables

## Numeric Types
```cs
//Integral literals
int x = 127;
long y = 0x7F;

//Real literals
double d = 1.5;
double million = 1E06;

float f = 4.5F;
decimal d = −1.23M; // Will not compile without the M suffix.

Console.WriteLine ( 1.0.GetType()); // Double (double)
Console.WriteLine ( 1E06.GetType()); // Double (double)
Console.WriteLine ( 1.GetType()); // Int32 (int)
Console.WriteLine ( 0xF0000000.GetType()); // UInt32 (uint)
```

### Numeric Conversions
```cs
int x = 12345; // int is a 32-bit integral
long y = x; // Implicit conversion to 64-bit integral
short z = (short)x; // Explicit conversion to 16-bit integral
```




## Boolean Type


## Strings and Characters
```cs
char c = 'A'; // Simple character
char newLine = '\n';
char backSlash = '\\';
char copyrightSymbol = '\u00A9';
char omegaSymbol = '\u03A9';
char newLine = '\u000A';


string a = "Heat";
string a = "test";
string b = "test";
Console.Write (a == b); // True

string a = "Here's a tab:\t";
string a1 = "\\\\server\\fileshare\\helloworld.cs";

string escaped = "First Line\r\nSecond Line";
string verbatim = @"First Line
Second Line";

//include the double-quote character
string xml = @"<customer id=""123""></customer>";
```



# Classes

## Classes
```cs
//public, internal, abstract, sealed, static, unsafe, and partial
class YourClassName
{
}
```

## Fields
```cs
//Static modifier: static
//Access modifiers: public internal private protected
//Inheritance modifier: new
//Unsafe code modifier: unsafe
//Read-only modifier: readonly
//Threading modifier: volatile

class Octopus
{
	string name;
	public int Age = 10;
}
```

## Methods
```cs
Static modifier: static
Access modifiers: public internal private protected
Inheritance modifiers: new virtual abstract override sealed
Partial method modifier: partial
Unmanaged code modifiers: unsafe extern



//Overloading methods
void Foo (int x) {...}
void Foo (double x) {...}
void Foo (int x, float y) {...}
void Foo (float x, int y) {...}

void Foo (int x) {...}
float Foo (int x) {...} // Compile-time error
void Goo (int[] x) {...}
void Goo (params int[] x) {...} // Compile-time error


//Pass-by-value versus pass-by-reference
void Foo (int x) {...}
void Foo (ref int x) {...} // OK so far
void Foo (out int x) {...} // Compile-time error

//Partial methods
partial class PaymentForm // In auto-generated file
{
	...
	partial void ValidatePayment (decimal amount);
}	

partial class PaymentForm // In hand-authored file
{
	...
	partial void ValidatePayment (decimal amount)
	{
		if (amount > 100)
		...
	}
}
```

## Constructors
```cs
Access modifiers: public internal private protected
Unmanaged code modifiers: unsafe extern

//Overloading constructors
public class Wine
{
	public decimal Price;
	public int Year;
	public Wine (decimal price) { Price = price; }
	public Wine (decimal price, int year) : this (price) { Year = year; }
}


public class Class1
{
	Class1() {} // Private constructor
	public static Class1 Create (...)
	{
		// Perform custom logic here to return an instance of Class1
		...
	}
}
```

## Static Constructors
```cs
class Test
{
	static Test() {
		Console.WriteLine ("Type Initialized"); 
	}
}
```

## The this Reference
```cs
public class Panda
{
	public Panda Mate;
	public void Marry (Panda partner)
	{
		Mate = partner;
		partner.Mate = this;
	}
}
```

## Properties


### Read-only and calculated properties

### Automatic properties

### get and set accessibility

### CLR property implementation
```cs
public decimal get_CurrentPrice {...}
public void set_CurrentPrice (decimal value) {...}
```
## Indexers


### Implementing an indexer
```cs
class Sentence
{
	string[] words = "The quick brown fox".Split();
	
	public string this [int wordNum] // indexer
	{
		get { return words [wordNum]; }
		set { words [wordNum] = value; }
	}
}

Sentence s = new Sentence();
Console.WriteLine (s[3]); // fox
s[3] = "kangaroo";
Console.WriteLine (s[3]); // kangaroo
```

### Constants
```cs
public class Test
{
	public const string Message = "Hello World";
}
```
### Finalizers
```cs
class Class1
{
	~Class1()
	{
		...
	}
}

//This is actually C# syntax for overriding Object’s Finalize method, 
//and the compiler expands it into the following method declaration:
protected override void Finalize()
{
	...
	base.Finalize();
}
```



# Inheritance
```cs
public class Asset
{
	public string Name;
}

public class Stock : Asset // inherits from Asset
{
	public long SharesOwned;
}

public class House : Asset // inherits from Asset
{
	public decimal Mortgage;
}

```

# Polymorphism
```cs
public static void Display (Asset asset)
{
	System.Console.WriteLine (asset.Name);
}


Stock msft = new Stock ... ;
House mansion = new House ... ;
Display (msft);
Display (mansion);
``

## Upcasting
```cs
Stock msft = new Stock();
Asset a = msft; // Upcast
Console.WriteLine (a == msft); // True
Console.WriteLine (a.Name); // OK
Console.WriteLine (a.SharesOwned); // Error: SharesOwned undefined
```

## Downcasting
```cs
Stock msft = new Stock();
Asset a = msft; // Upcast
Stock s = (Stock)a; // Downcast
Console.WriteLine (s.SharesOwned); // <No error>
Console.WriteLine (s == a); // True
Console.WriteLine (s == msft); // True
```

```cs
House h = new House();
Asset a = h; // Upcast always succeeds
Stock s = (Stock)a; // Downcast fails: a is not a Stock
```

## The as operator
```cs
Asset a = new Asset();
Stock s = a as Stock; // s is null; no exception thrown

int shares = ((Stock)a).SharesOwned; // Approach #1
int shares = (a as Stock).SharesOwned; // Approach #2
```

## The is operator
```cs

```




## Virtual Function Members
```cs
```

### Abstract Classes and Abstract Members
```cs
public abstract class Asset
{
	// Note empty implementation
	public abstract decimal NetValue { get; }
	}
	
	public class Stock : Asset
	{
		public long SharesOwned;
		public decimal CurrentPrice;
	
		// Override like a virtual method.
		public override decimal NetValue
		{
			get { return CurrentPrice * SharesOwned; }
		}
	}		
}
```


### Hiding Inherited Members
```cs
public class A { public int Counter = 1; }
public class B : A { public int Counter = 2; }

public class A { public int Counter = 1; }
public class B : A { public new int Counter = 2; }
```

### Sealing Functions and Classes
```cs
public sealed override decimal Liability { get { return Mortgage; } }
```

#### The base Keyword
```cs
public class House : Asset
{
	...
	public override decimal Liability
	{
		get { return base.Liability + Mortgage; }
	}
}
```

### Constructors and Inheritance
```cs
public class Baseclass
{
	public int X;
	public Baseclass () { }
	public Baseclass (int x) { this.X = x; }
}
public class Subclass : Baseclass { }

public class Subclass : Baseclass
{
	public Subclass (int x) : base (x) { }
}
```

### Boxing and Unboxing
```cs
int x = 9;
object obj = x; // Box the int

int y = (int)obj; // Unbox the int
```
### Copying semantics of boxing and unboxing



## Interfaces
```cs
public interface IEnumerator
{
	bool MoveNext();
	object Current { get; }
	void Reset();
}

internal class Countdown : IEnumerator
{
	int count = 11;
	public bool MoveNext () { return count-- > 0 ; }
	public object Current { get { return count; } }
	public void Reset() { throw new NotSupportedException(); }
}

IEnumerator e = new Countdown();
while (e.MoveNext())
	Console.Write (e.Current); // 109876543210
```	
	
### Extending an Interface	
```cs
public interface IUndoable { void Undo(); }
public interface IRedoable : IUndoable { void Redo(); }
```

### Explicit Interface Implementation
```cs
interface I1 { void Foo(); }
interface I2 { int Foo(); }

public class Widget : I1, I2
{
	public void Foo ()
	{
		Console.WriteLine ("Widget's implementation of I1.Foo");
	}
	
	int I2.Foo()
	{
		Console.WriteLine ("Widget's implementation of I2.Foo");
		return 42;
	}
}


Widget w = new Widget();
w.Foo(); // Widget's implementation of I1.Foo
((I1)w).Foo(); // Widget's implementation of I1.Foo
((I2)w).Foo(); // Widget's implementation of I2.Foo
```

### Implementing Interface Members Virtually
```cs
public interface IUndoable { void Undo(); }
public class TextBox : IUndoable
{
	public virtual void Undo()
	{
		Console.WriteLine ("TextBox.Undo");
	}

}

public class RichTextBox : TextBox
{
	public override void Undo()
	{
		Console.WriteLine ("RichTextBox.Undo");
	}
}

RichTextBox r = new RichTextBox();
r.Undo(); // RichTextBox.Undo
((IUndoable)r).Undo(); // RichTextBox.Undo
((TextBox)r).Undo(); // RichTextBox.Undo
```

### Reimplementing an Interface in a Subclass
```cs
public interface IUndoable { void Undo(); }
public class TextBox : IUndoable
{
void IUndoable.Undo() { Console.WriteLine ("TextBox.Undo"); }
}
public class RichTextBox : TextBox, IUndoable
{
public new void Undo() { Console.WriteLine ("RichTextBox.Undo"); }
}

RichTextBox r = new RichTextBox();
r.Undo(); // RichTextBox.Undo Case 1
((IUndoable)r).Undo(); // RichTextBox.Undo Case 2


public class TextBox : IUndoable
{
public void Undo() { Console.WriteLine ("TextBox.Undo"); }
}


RichTextBox r = new RichTextBox();
r.Undo(); // RichTextBox.Undo 				Case 1
((IUndoable)r).Undo(); // RichTextBox.Undo 	Case 2
((TextBox)r).Undo(); // TextBox.Undo		Case 3
```

### Alternatives to interface reimplementation
```cs
public class TextBox : IUndoable
{
	void IUndoable.Undo() { Undo(); } // Calls method below
	protected virtual void Undo() { Console.WriteLine ("TextBox.Undo"); }
}

public class RichTextBox : TextBox
{
	protected override void Undo() { Console.WriteLine("RichTextBox.Undo"); }
}
```
# Methods
# Expressions and Operators
# Statements
# Structs
# Enumerations
```cs
namespace Enums
{
    class Program
    {
        static void Main(string[] args)
        {
			Console.WriteLine(Color.Yellow);		//Output: Yellow
			Console.WriteLine((int)Color.Yellow);	//Output: 0
        }
    }

    enum Color
    {
        Yellow,
        Blue,
        Brown,
        Green
    }
}
```

### Underlying Data type & Inheritance

```cs
static void Main(string[] args)
{
	Console.WriteLine((byte)Color.Yellow);	//Output: 0
	Console.WriteLine((byte)Color.Blue);	//Output: 1
}

enum Color:byte
{
	Yellow,
	Blue,
	Brown,
	Green
}


```


### Inheritance in Enum
By default, enum is a sealed class and therefore sticks to all the rules that a sealed class follows, so no class can derive from enum, i.e., a sealed type.
```cs
enum Shades:Color
{

}
//Output
//Compile time error: 'Enums.Derived': cannot derive from sealed type 'Enums.Color'
```

```cs
internal enum Color: System.Enum
{
	Yellow,
	Blue
}
//Output
//Compile time error: Type byte, sbyte, short, ushort, int, uint, long, or ulong expected.

```

### IComparable
```cs
internal enum Color
{
	Yellow,
	Blue,
	Green
}

private static void Main(string[] args)
{
	Console.WriteLine(Color.Yellow.CompareTo(Color.Blue));
	Console.WriteLine((byte)Color.Yellow);
	Console.ReadLine();
}
		
//Output -1
```

### IFormattable
```cs
internal enum Color
{
	Yellow,
	Blue,
	Green
}

private static void Main(string[] args)
{
	System.Console.WriteLine(Color.Format(typeof(Color), Color.Green, "X"));
	System.Console.WriteLine(Color.Format(typeof(Color), Color.Green, "d"));
	Console.ReadLine();
}
//Output		
00000002
2	

```
	
	
### IConvertible	
```cs

enum Color
{
	Yellow,
	Blue,
	Green
}
	
private static void Main(string[] args)
{
	string[] names;
	names = Color.GetNames(typeof (Color));
	foreach (var name in names)
	{
		Console.WriteLine(name);
	}
	Console.ReadLine();
}
		
```	
	
	
	
	
```cs
using System;
namespace Enums
{
    class Program
    {
        static void Main(string[] args)
        {
            Console.WriteLine((int)Color.Yellow);
            Console.WriteLine((int)Color.Blue);
            Console.WriteLine((int)Color.Brown);
            Console.WriteLine((int)Color.Green);
            Console.ReadLine();
        }
    }

    enum Color
    {
        Yellow =2,
        Blue,
        Brown=9,
        Green,
		Red = Yellow

    }
}
//Output
2
3
9
10

```	

```cs
class Program
    {
        static void Main(string[] args)
        {
            Color.Yellow = 3;
        }
    }

    enum Color
    {
        Yellow = 2,
        Blue
    }

//Output
Compile time error: The left-hand side of an assignment must be a variable, property or indexer
```


```cs
enum Color:byte
    {
        Yellow =300 ,
        Blue,
        Brown=9,
        Green,
    }
::Output
Compile time error: Constant value '300' cannot be converted to a 'byte'


```	

```cs
enum Color
{
	Yellow,
	Blue,
	Brown,
	Green,
	Blue
}
//Output
Compile time error: The type 'Enums.Color' already contains a definition for 'Blue'	
```

### Circular Dependency
```cs
internal enum Color
{
	Yellow=Blue,
	Blue
}

//Output
Compile time error: The evaluation of the constant value for 'Enums.Color.Yellow' involves a circular definition
```
	
###  Diving Deep

```cs
enum Color
{

}

Color color = (Color) -1;

::Output
Compile time error: 
To cast a negative value, you must enclose the value in parentheses
'Enums.Color' is a 'type' but is used like a 'variable'
```


```cs
enum Color
{
  value__
}
//Output
Compile time error: The enumerator name 'value__' is reserved and cannot be used

```	
	
# Arrays

```cs
char[] vowels = new char[5]; // Declare an array of 5 characters

vowels[0] = 'a';
vowels[1] = 'e';
vowels[2] = 'i';
vowels[3] = 'o';
vowels[4] = 'u';
Console.WriteLine (vowels[1]); // e


char[] vowels = new char[] {'a','e','i','o','u'};

//or simply:
char[] vowels = {'a','e','i','o','u'};

//Default Element Initialization
int[] a = new int[1000];
Console.Write (a[123]); // 0

//Multidimensional Arrays
int[,] matrix = new int[3,3];

for (int i = 0; i < matrix.GetLength(0); i++)
	for (int j = 0; j < matrix.GetLength(1); j++)
		matrix[i,j] = i * 3 + j;

//Simplified Array Initialization Expressions
int[,] matrix = new int[,]
{
	{0,1,2},
	{3,4,5},
	{6,7,8}
};

// Jagged arrays
int[][] matrix = new int[3][];

for (int i = 0; i < matrix.Length; i++)
{
	matrix[i] = new int[3]; // Create inner array
	for (int j = 0; j < matrix[i].Length; j++)
	matrix[i][j] = i * 3 + j;
}

//Simplified Array Initialization Expressions
int[][] matrix = new int[][]
{
	new int[] {0,1,2},
	new int[] {3,4,5},
	new int[] {6,7,8,9}
};
```
# Delegates
# Events
# Conversions
# Generics
```cs
public class Stack<T>
{
	int position;
	T[] data = new T[100];
	public void Push (T obj) { data[position++] = obj; }
	public T Pop() { return data[--position]; }
}

Stack<int> stack = new Stack<int>();
stack.Push(5);
stack.Push(10);
int x = stack.Pop(); // x is 10
int y = stack.Pop(); // y is 5
```

#### Generic Constraints
```cs
where T : base-class // Base-class constraint
where T : interface // Interface constraint
where T : class // Reference-type constraint
where T : struct // Value-type constraint (excludes Nullable types)
where T : new() // Parameterless constructor constraint
where U : T // Naked type constraint

class SomeClass {}
interface Interface1 {}

class GenericClass<T,U> where T : SomeClass, Interface1
						where U : new()
{...}
```
#### Subclassing Generic Types
```cs
class Stack<T> {...}
class SpecialStack<T> : Stack<T> {...}

class IntStack : Stack<int> {...}

```

# Enumerators and Iterators
# Exceptions
# Preprocessor Directives
# Reflection and Attributes
# Dynamic Binding
# Disposal and Garbage Collection
# Serialization
# Application Domains
# Collections
# Lambda
# Asynchronous Programming
# Concurrency & Asynchrony
# Native and COM Interoperability
# Parallel Programming
# Advanced Threading
# Security
# Reflection and Metadata
# Networking
# Streams and I/O
# Diagnostics and Code Contracts

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

```cs
public class Employee
{

	//Constants
	//---------
	public const int months = 12, weeks = 52, days = 365;
	const double daysPerWeek = (double)days / (double)weeks;


	//Fields
	//---------
	// private field
	private DateTime date;

	// Instance field (Generally not recommended.)
	public string day;

	// static field 
	public static int NumberOfEmployees;
	
	public static volatile bool finished;
	
	//readonly readonly field
	public readonly int legs = 8, eyes = 2;



	//Property
	//---------
	private static int counter;
	private string name;


	// Auto-Impl Properties for trivial get and set
	public double TotalPurchases { get; set; }

	public abstract double Area
	{
		get;
		set;
	}

	// A read-write instance property:
	public string Name
	{
		get { return name; }
		set { name = value; }
	}

	// A read-only static property:
	public static int Counter
	{
		get { return counter; }
	}

	// A read-write instance property, with calculation
	private double seconds;
	public double Hours
	{
		get { return seconds / 3600; }
		set { seconds = value * 3600; }
	}


	// Public property exposes date field safely.
	public DateTime Date
	{
		get
		{
			return date;
		}
		set
		{
			// Set some reasonable boundaries for likely birth dates.
			if (value.Year > 1900 && value.Year <= DateTime.Today.Year)
			{
				date = value;
			}
			else
				throw new ArgumentOutOfRangeException();
		}

	}

	// Public method also exposes date field safely.
	// Example call: birthday.SetDate("1975, 6, 30");
	public void SetDate(string dateString)
	{
		DateTime dt = Convert.ToDateTime(dateString);

		// Set some reasonable boundaries for likely birth dates.
		if (dt.Year > 1900 && dt.Year <= DateTime.Today.Year)
		{
			date = dt;
		}
		else
			throw new ArgumentOutOfRangeException();
	}

	//Read only
	public TimeSpan GetTimeSpan(string dateString)
	{
		DateTime dt = Convert.ToDateTime(dateString);

		if (dt != null && dt.Ticks < date.Ticks)
		{
			return date - dt;
		}
		else
			throw new ArgumentOutOfRangeException();

	}

	public virtual int TestProperty
	{
		// Notice the accessor accessibility level.
		protected set { }

		// No access modifier is used here.
		get { return 0; }
	}
	
	
	
	
	// A Constructor:
	public Employee()
	{
		// Calculate the employee's number:
		counter = ++counter + NumberOfEmployees;
	}


	// protected method:
	protected void Pedal() { }

	// private field:
	private int wheels = 3;

	// protected internal property:
	protected internal int Wheels
	{
		get { return wheels; }
	}


	public override double GetTopSpeed()
	{
		return 108.4;
	}

}

public class Manager : Employee
{
	private string name;

	// Notice the use of the new modifier:
	public new string Name
	{
		get { return name; }
		set { name = value + ", Manager"; }
	}

	public double side;

	public override double Area
	{
		get
		{
			return side * side;
		}
		set
		{
			side = System.Math.Sqrt(value);
		}
	}

	public override int TestProperty
	{
		// Use the same accessibility level as in the overridden accessor.
		protected set { }

		// Cannot use access modifier here.
		get { return 0; }
	}
}


abstract class Motorcycle
{
	// Anyone can call this.
	public void StartEngine() {/* Method statements here */ }

	// Only derived classes can call this.
	protected void AddGas(int gallons) { /* Method statements here */ }

	// Derived classes can override the base class implementation.
	public virtual int Drive(int miles, int speed) { /* Method statements here */ return 1; }

	// Derived classes must implement this.
	public abstract double GetTopSpeed();
}


class TestEmployee
{
	static void Main()
	{
		
		Employee.NumberOfEmployees = 107;
		Employee e1 = new Employee();
		e1.Name = "Claude Vige";

		System.Console.WriteLine("Employee number: {0}", Employee.Counter);
		System.Console.WriteLine("Employee name: {0}", e1.Name);

		Manager m1 = new Manager();
		// Derived class property.
		m1.Name = "John";
		// Base class property.
		((Employee)m1).Name = "Mary";
	}
}
```


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

## Enumeration Types

```cs
enum Days { Sunday, Monday, Tuesday, Wednesday, Thursday, Friday, Saturday };
enum Months : byte { Jan, Feb, Mar, Apr, May, Jun, Jul, Aug, Sep, Oct, Nov, Dec }; 
enum Days {Sat=1, Sun, Mon, Tue, Wed, Thu, Fri};
enum Days : byte {Sat=1, Sun, Mon, Tue, Wed, Thu, Fri};
enum Range : long { Max = 2147483648L, Min = 255L };

Days today = Days.Monday;
int dayNumber =(int)today;
Console.WriteLine("{0} is day number #{1}.", today, dayNumber);

Months thisMonth = Months.Dec;
byte monthNumber = (byte)thisMonth;
Console.WriteLine("{0} is month number #{1}.", thisMonth, monthNumber);

// Output:
// Monday is day number #1.
// Dec is month number #11.


public class EnumTest
{
    enum Days { Sun, Mon, Tue, Wed, Thu, Fri, Sat };

    static void Main()
    {
        int x = (int)Days.Sun;
        int y = (int)Days.Fri;
        Console.WriteLine("Sun = {0}", x);
        Console.WriteLine("Fri = {0}", y);
    }
}
```


```cs
enum MachineState
{
    PowerOff = 0,
    Running = 5,
    Sleeping = 10,
    Hibernating = Sleeping + 5
}
```

### Enumeration Types as Bit Flags

```cs
[Flags]
enum Days2
{
    None = 0x0,
    Sunday = 0x1,
    Monday = 0x2,
    Tuesday = 0x4,
    Wednesday = 0x8,
    Thursday = 0x10,
    Friday = 0x20,
    Saturday = 0x40
}
class MyClass
{
    Days2 meetingDays = Days2.Tuesday | Days2.Thursday;
}


// Initialize with two flags using bitwise OR.
meetingDays = Days2.Tuesday | Days2.Thursday;

// Set an additional flag using bitwise OR.
meetingDays = meetingDays | Days2.Friday;

Console.WriteLine("Meeting days are {0}", meetingDays);
// Output: Meeting days are Tuesday, Thursday, Friday

// Remove a flag using bitwise XOR.
meetingDays = meetingDays ^ Days2.Tuesday;
Console.WriteLine("Meeting days are {0}", meetingDays);
// Output: Meeting days are Thursday, Friday

// Test value of flags using bitwise AND.
bool test = (meetingDays & Days2.Thursday) == Days2.Thursday;
Console.WriteLine("Thursday {0} a meeting day.", test == true ? "is" : "is not");
```

### Using the System.Enum Methods to Discover and Manipulate Enum Values
```cs
string s = Enum.GetName(typeof(Days), 4);
Console.WriteLine(s);

Console.WriteLine("The values of the Days Enum are:");
foreach (int i in Enum.GetValues(typeof(Days)))
    Console.WriteLine(i);

Console.WriteLine("The names of the Days Enum are:");
foreach (string str in Enum.GetNames(typeof(Days)))
    Console.WriteLine(str);
```	

## Indexers 
```cs
class SampleCollection<T>
{
    // Declare an array to store the data elements.
    private T[] arr = new T[100];

    // Define the indexer, which will allow client code
    // to use [] notation on the class instance itself.
    // (See line 2 of code in Main below.)        
    public T this[int i]
    {
        get
        {
            // This indexer is very simple, and just returns or sets
            // the corresponding element from the internal array.
            return arr[i];
        }
        set
        {
            arr[i] = value;
        }
    }
}

// This class shows how client code uses the indexer.
class Program
{
    static void Main(string[] args)
    {
        // Declare an instance of the SampleCollection type.
        SampleCollection<string> stringCollection = new SampleCollection<string>();

        // Use [] notation on the type.
        stringCollection[0] = "Hello, World";
        System.Console.WriteLine(stringCollection[0]);
    }
}
// Output:
// Hello, World.
```


## Delegates

### very basic Delegate
```cs
namespace Akadia.BasicDelegate
{
    // Declaration
    public delegate void SimpleDelegate();

    class TestDelegate
    {
        public static void MyFunc()
        {
            Console.WriteLine("I was called by delegate ...");
        }

        public static void Main()
        {
            // Instantiation
            SimpleDelegate simpleDelegate = new SimpleDelegate(MyFunc);

            // Invocation
            simpleDelegate();
        }
    }
}
```

### Calling Static Functions
```cs
namespace Akadia.SimpleDelegate
{
    // Delegate Specification
    public class MyClass
    {
        // Declare a delegate that takes a single string parameter
        // and has no return type.
        public delegate void LogHandler(string message);

        // The use of the delegate is just like calling a function directly,
        // though we need to add a check to see if the delegate is null
        // (that is, not pointing to a function) before calling the function.
        public void Process(LogHandler logHandler)
        {
            if (logHandler != null)
            {
                logHandler("Process() begin");
            }

            if (logHandler != null)
            {
                logHandler ("Process() end");
            }
        }
    }

    // Test Application to use the defined Delegate
    public class TestApplication
    {
        // Static Function: To which is used in the Delegate. To call the Process()
        // function, we need to declare a logging function: Logger() that matches
        // the signature of the delegate.
        static void Logger(string s)
        {
            Console.WriteLine(s);
        }

        static void Main(string[] args)
        {
            MyClass myClass = new MyClass();

            // Crate an instance of the delegate, pointing to the logging function.
            // This delegate will then be passed to the Process() function.
            MyClass.LogHandler myLogger = new MyClass.LogHandler(Logger);
            myClass.Process(myLogger);
        }
    }
}

Compile an test:

# csc SimpleDelegate2.cs
# SimpleDelegate2.exe
Process() begin
Process() end
```

### Calling Member Functions
```cs
namespace Akadia.SimpleDelegate
{
    // Delegate Specification
    public class MyClass
    {
        // Declare a delegate that takes a single string parameter
        // and has no return type.
        public delegate void LogHandler(string message);

        // The use of the delegate is just like calling a function directly,
        // though we need to add a check to see if the delegate is null
        // (that is, not pointing to a function) before calling the function.
        public void Process(LogHandler logHandler)
        {
            if (logHandler != null)
            {
                logHandler("Process() begin");
            }

            if (logHandler != null)
            {
                logHandler ("Process() end");
            }
        }
    }

    // The FileLogger class merely encapsulates the file I/O
    public class FileLogger
    {
        FileStream fileStream;
        StreamWriter streamWriter;

        // Constructor
        public FileLogger(string filename)
        {
            fileStream = new FileStream(filename, FileMode.Create);
            streamWriter = new StreamWriter(fileStream);
        }

        // Member Function which is used in the Delegate
        public void Logger(string s)
        {
            streamWriter.WriteLine(s);
        }

        public void Close()
        {
            streamWriter.Close();
            fileStream.Close();
        }
    }

    // Main() is modified so that the delegate points to the Logger()
    // function on the fl instance of a FileLogger. When this delegate
    // is invoked from Process(), the member function is called and
    // the string is logged to the appropriate file.
    public class TestApplication
    {
        static void Main(string[] args)
        {
            FileLogger fl = new FileLogger("process.log");

            MyClass myClass = new MyClass();

            // Crate an instance of the delegate, pointing to the Logger()
            // function on the fl instance of a FileLogger.
            MyClass.LogHandler myLogger = new MyClass.LogHandler(fl.Logger);
            myClass.Process(myLogger);
            fl.Close();
        }
    }
}

Compile an test:

# csc SimpleDelegate3.cs
# SimpleDelegate3.exe
# cat process.log
Process() begin
Process() end
```

### Multicasting
```cs
namespace Akadia.SimpleDelegate
{
    // Delegate Specification
    public class MyClass
    {
        // Declare a delegate that takes a single string parameter
        // and has no return type.
        public delegate void LogHandler(string message);

        // The use of the delegate is just like calling a function directly,
        // though we need to add a check to see if the delegate is null
        // (that is, not pointing to a function) before calling the function.
        public void Process(LogHandler logHandler)
        {
            if (logHandler != null)
            {
                logHandler("Process() begin");
            }

            if (logHandler != null)
            {
                logHandler ("Process() end");
            }
        }
    }

    // The FileLogger class merely encapsulates the file I/O
    public class FileLogger
    {
        FileStream fileStream;
        StreamWriter streamWriter;

        // Constructor
        public FileLogger(string filename)
        {
            fileStream = new FileStream(filename, FileMode.Create);
            streamWriter = new StreamWriter(fileStream);
        }

        // Member Function which is used in the Delegate
        public void Logger(string s)
        {
            streamWriter.WriteLine(s);
        }

        public void Close()
        {
            streamWriter.Close();
            fileStream.Close();
        }
    }

    // Test Application which calls both Delegates
    public class TestApplication
    {
         // Static Function which is used in the Delegate
        static void Logger(string s)
        {
            Console.WriteLine(s);
        }

        static void Main(string[] args)
        {
            FileLogger fl = new FileLogger("process.log");

            MyClass myClass = new MyClass();

            // Crate an instance of the delegates, pointing to the static
            // Logger() function defined in the TestApplication class and
            // then to member function on the fl instance of a FileLogger.
            MyClass.LogHandler myLogger = null;
            myLogger += new MyClass.LogHandler(Logger);
            myLogger += new MyClass.LogHandler(fl.Logger);

            myClass.Process(myLogger);
            fl.Close();
        }
    }
}
Compile an test:

# csc SimpleDelegate4.cs
# SimpleDelegate4.exe
Process() begin
Process() end
# cat process.log
Process() begin
Process() end
```

## Events

### Simple Event
```cs
namespace Akadia.SimpleEvent
{
    /* ========= Publisher of the Event ============== */
    public class MyClass
    {
        // Define a delegate named LogHandler, which will encapsulate
        // any method that takes a string as the parameter and returns no value
        public delegate void LogHandler(string message);
 
        // Define an Event based on the above Delegate
        public event LogHandler Log;
  
        // Instead of having the Process() function take a delegate
        // as a parameter, we've declared a Log event. Call the Event,
        // using the OnXXXX Method, where XXXX is the name of the Event.
        public void Process()
        {
            OnLog("Process() begin");
            OnLog("Process() end");
        }
 
        // By Default, create an OnXXXX Method, to call the Event
        protected void OnLog(string message)
        {
            if (Log != null)
            {
                Log(message);
            }
        }
    }
 
    // The FileLogger class merely encapsulates the file I/O
    public class FileLogger
    {
        FileStream fileStream;
        StreamWriter streamWriter;
 
        // Constructor
        public FileLogger(string filename)
        {
            fileStream = new FileStream(filename, FileMode.Create);
            streamWriter = new StreamWriter(fileStream);
        }
 
        // Member Function which is used in the Delegate
        public void Logger(string s)
        {
            streamWriter.WriteLine(s);
        }
 
        public void Close()
        {
            streamWriter.Close();
            fileStream.Close();
        }
    }
 
    /* ========= Subscriber of the Event ============== */
    // It's now easier and cleaner to merely add instances
    // of the delegate to the event, instead of having to
    // manage things ourselves
    public class TestApplication
    {
        static void Logger(string s)
        {
            Console.WriteLine(s);
        }
 
        static void Main(string[] args)
        {
            FileLogger fl = new FileLogger("process.log");
            MyClass myClass = new MyClass();
 
            // Subscribe the Functions Logger and fl.Logger
            myClass.Log += new MyClass.LogHandler(Logger);
            myClass.Log += new MyClass.LogHandler(fl.Logger);

            // The Event will now be triggered in the Process() Method
            myClass.Process();
 
            fl.Close();
        }
    }
}

Compile an test:

# csc SimpleEvent.cs
# SimpleEvent.exe
Process() begin
Process() end
# cat process.log
Process() begin
Process() end
```


### The Second Change Event Example
```cs
namespace SecondChangeEvent
{
   /* ======================= Event Publisher =============================== */

   // Our subject -- it is this class that other classes
   // will observe. This class publishes one event:
   // SecondChange. The observers subscribe to that event.
   public class Clock
   {
      // Private Fields holding the hour, minute and second
      private int _hour;
      private int _minute;
      private int _second;

      // The delegate named SecondChangeHandler, which will encapsulate
      // any method that takes a clock object and a TimeInfoEventArgs
      // object as the parameter and returns no value. It's the
      // delegate the subscribers must implement.
      public delegate void SecondChangeHandler (
         object clock,
         TimeInfoEventArgs timeInformation
      );

      // The event we publish
      public event SecondChangeHandler SecondChange;

      // The method which fires the Event
      protected void OnSecondChange(
         object clock,
         TimeInfoEventArgs timeInformation
      )
      {
         // Check if there are any Subscribers
         if (SecondChange != null)
         {
            // Call the Event
            SecondChange(clock,timeInformation);
         }
      }

      // Set the clock running, it will raise an
      // event for each new second
      public void Run()
      {
         for(;;)
         {
            // Sleep 1 Second
            Thread.Sleep(1000);

            // Get the current time
            System.DateTime dt = System.DateTime.Now;

            // If the second has changed
            // notify the subscribers
            if (dt.Second != _second)
            {
               // Create the TimeInfoEventArgs object
               // to pass to the subscribers
               TimeInfoEventArgs timeInformation =
                  new TimeInfoEventArgs(
                  dt.Hour,dt.Minute,dt.Second);

               // If anyone has subscribed, notify them
               OnSecondChange (this,timeInformation);
            }

            // update the state
            _second = dt.Second;
            _minute = dt.Minute;
            _hour = dt.Hour;

         }
      }
   }

   // The class to hold the information about the event
   // in this case it will hold only information
   // available in the clock class, but could hold
   // additional state information
   public class TimeInfoEventArgs : EventArgs
   {
      public TimeInfoEventArgs(int hour, int minute, int second)
      {
         this.hour = hour;
         this.minute = minute;
         this.second = second;
      }
      public readonly int hour;
      public readonly int minute;
      public readonly int second;
   }

   /* ======================= Event Subscribers =============================== */

   // An observer. DisplayClock subscribes to the
   // clock's events. The job of DisplayClock is
   // to display the current time
   public class DisplayClock
   {
      // Given a clock, subscribe to
      // its SecondChangeHandler event
      public void Subscribe(Clock theClock)
      {
         theClock.SecondChange +=
            new Clock.SecondChangeHandler(TimeHasChanged);
      }

      // The method that implements the
      // delegated functionality
      public void TimeHasChanged(
         object theClock, TimeInfoEventArgs ti)
      {
         Console.WriteLine("Current Time: {0}:{1}:{2}",
            ti.hour.ToString(),
            ti.minute.ToString(),
            ti.second.ToString());
      }
   }

   // A second subscriber whose job is to write to a file
   public class LogClock
   {
      public void Subscribe(Clock theClock)
      {
         theClock.SecondChange +=
            new Clock.SecondChangeHandler(WriteLogEntry);
      }

      // This method should write to a file
      // we write to the console to see the effect
      // this object keeps no state
      public void WriteLogEntry(
         object theClock, TimeInfoEventArgs ti)
      {
         Console.WriteLine("Logging to file: {0}:{1}:{2}",
            ti.hour.ToString(),
            ti.minute.ToString(),
            ti.second.ToString());
      }
   }

   /* ======================= Test Application =============================== */

   // Test Application which implements the
   // Clock Notifier - Subscriber Sample
   public class Test
   {
      public static void Main()
      {
         // Create a new clock
         Clock theClock = new Clock();

         // Create the display and tell it to
         // subscribe to the clock just created
         DisplayClock dc = new DisplayClock();
         dc.Subscribe(theClock);

         // Create a Log object and tell it
         // to subscribe to the clock
         LogClock lc = new LogClock();
         lc.Subscribe(theClock);

         // Get the clock started
         theClock.Run();
      }
   }
}
```


### Partial Types
```cs
// PaymentFormGen.cs - auto-generated
partial class PaymentForm { ... }

// PaymentForm.cs - hand-authored
partial class PaymentForm { ... }


//Each participant must have the partial declaration; the following is illegal:
partial class PaymentForm {}
class PaymentForm {}

//There are two ways to specify a base class with partial classes:
//• Specify the (same) base class on each participant. For example:
partial class PaymentForm : ModalForm {}
partial class PaymentForm : ModalForm {}

//• Specify the base class on just one participant. For example:
partial class PaymentForm : ModalForm {}
partial class PaymentForm {}
```

