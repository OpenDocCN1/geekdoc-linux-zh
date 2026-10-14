# OBJECT FUNCTION RESULTS

It is often necessary to create functions that pass back objects—you might think of them as object-factory functions. A function might return a class object in one of three ways: by value, as a pointer, or as a reference. The first method is probably the least common but is sometimes useful. For example, here's a function that returns a TDate object by value:

```
TDate any_function()
{
    TDate temp(5, 8, 2003);
    return temp;  // Return copy of object ???
}
```

The function constructs a local TDate object named temp and then returns that object as the function's value. Be aware, however, that this type of code actually returns a copy of the object, which might be assigned to a variable using this statement elsewhere in the program:

```
TDate new_date = any_function();
```

The function works, but consider all the wasted effort that this code produces. First, any_function() constructs the temp object. Next, it returns that object by value, causing another temporary object to be created. Finally, new_date is constructed using the returned temporary object, which is then finally deleted. That's three constructor calls and two copies of an object where only one is needed! And once again, if the objects own pointers, their class must have a copy constructor and an operator=() function, or a serious bug could raise its ugly head in even simple code like this.

Often, a better method is to return a pointer to an object. Here's a new version of any_function() that demonstrates the technique:

```
TDate *any_function()
{
    return new TDate(5, 8, 2003);
}
```

The function uses the new operator to construct a new instance of the TDate class and then returns the resulting TDate pointer as the function result. Elsewhere in the program, a statement can call any_function() to obtain a new TDate object:

```
TDate *tdp = any_function();
```

That statement actually performs three actions. It declares tdp as a TDate pointer, it calls any_function() to construct a TDate object, and it assigns the resulting object address to tdp. This is more efficient than returning an object by value because only one object is constructed. However, it’s important to understand that the use of new inside any_function() creates an object of global scope. Somewhere, somehow, that object must be deleted. For