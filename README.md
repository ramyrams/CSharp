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
