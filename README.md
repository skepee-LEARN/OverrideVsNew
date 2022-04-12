# Override vs. New

Let us run the code and analyze each example:

```
Example 1: Base class invokes its virtual method.
Base Class constructor
Base Class virtual method called
----------------------------------------------------------------------------
Example 2: Base class invokes its method that is hidden in the derived class.
Base Class method called (hidden in the derived class)
----------------------------------------------------------------------------
Example 3: Derived class overrides base class method.
Base Class constructor
Child Class constructor
Child Class overrides
----------------------------------------------------------------------------
Example 4: Base class method invoked (the method is hidden in the derived class).
Base Class method called (hidden in the derived class)
----------------------------------------------------------------------------
Example 5: Derived class overrides base class method.
Base Class constructor
Child Class constructor
Child Class overrides
Child Class hides base class method.
----------------------------------------------------------------------------
```

Let us consider the following base class:

```
   public class BaseClass
    {
        public BaseClass()
        {
            Console.WriteLine("Base Class constructor");
        }

        public virtual void GetMethodOwnerName()
        {
            Console.WriteLine("Base Class virtual method called");
        }

        public void GetMethodOwnerNameNew()
        {
            Console.WriteLine("Base Class method called (hidden in the derived class)");
        }
    }
```

and its derived class:

```
    public class ChildClass : BaseClass
    {
        public ChildClass()
        {
            Console.WriteLine("Child Class constructor");
        }

        public override void GetMethodOwnerName()
        {
            Console.WriteLine("Child Class overrides");
        }

        public new void GetMethodOwnerNameNew()
        {
            Console.WriteLine("Child Class hides base class method.");
        }
    }
```


The base class has the following methods:
- constructor, 
- ```GetMethodOwnerName``` that is a virtual method
- ```GetMethodOwnerNameNew``` that is not virtual but will be hidden in the derived class.


## Example 1: invoking virtual method in the base class
Let us instatiante the class:

```
  BaseClass b = new BaseClass();
```

the following code invokes the methods in the base class.

```
  b.GetMethodOwnerName();
```
I can call the method of base class. Because it's a virtual method I can call the method only in the base class.


## Example 2: invoking virtual method in the base class
By invoking the method:
```
  b.GetMethodOwnerNameNew();
```
the method in the base class is invoked even if it is hidden in the derived class.



## Example 3: Derived class overrides base class method
Let us now define the class in this way:

```
  BaseClass c = new ChildClass();
```
The base class is instatiated by using child class constructor.
Even if c is of type BaseClass but the value is ChildClass so the overriden method will be called.

Here a call of methodsnew in the child class that hides the method in the base class.
The hiding is performed by using the new keyword.
If the 'new' keyword is not used, the code will work in the same way because
the compiler interprets the code in the same way but a warning meesage will appear:

It just appear the following warning:
```
Severity Code    Description Project File Line    Suppression State
Warning CS0108  'ChildClass.GetMethodOwnerNameNew()' hides inherited member 'BaseClass.GetMethodOwnerNameNew()'.Use the new keyword if hiding was intended.	
Override C:\Override\Program.cs  61  Active
```

So 'new' keyword is not mandatory but for a compilation with no errors it is suggested to use. The compiler interprets the code in the same way.


## Example 4: Base class method invoked (the method is hidden in the derived class).
With following code:
```            
  c.GetMethodOwnerNameNew();
```
this is the way to call the method in the base class hidden by the child.


## Example 5: Derived class overrides base class method
With the following code:
```
ChildClass c2 = new ChildClass();
c2.GetMethodOwnerName();
```
This is the way to call the overriden method in the child class.
And finally: 
```
c2.GetMethodOwnerNameNew();
```            
This is the way to call the method in the child class that hides the method in the base class.



