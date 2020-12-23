# Week 4

## Wrap up

- Remaining section from Previous Week
- Standard Type Hierarchy (Continued)
- Special Method Names

## Standard Type Hierarchy (Part 2)

### Callable Types

#### User Defined Functions

``` py
def some_function():
    return

def some_function(a, b, c):
    return
```
##### Scopes and Namespaces Example

This is an example demonstrating how to reference the different scopes and
namespaces, and how `global` and `nonlocal` affect variable
binding.

``` py
    def scope_test():
        def do_local():
            spam = "local spam"

        def do_nonlocal():
            nonlocal spam
            spam = "nonlocal spam"

        def do_global():
            global spam
            spam = "global spam"

        spam = "test spam"
        do_local()
        print("After local assignment:", spam)
        do_nonlocal()
        print("After nonlocal assignment:", spam)
        do_global()
        print("After global assignment:", spam)

    scope_test()
    print("In global scope:", spam)
```

Note how the *local* assignment (which is default) didn't change *scope_test*\'s
binding of *spam*.  The `nonlocal` assignment changed *scope_test*\'s
binding of *spam*, and the `global` assignment changed the module-level
binding.

You can also see that there was no previous binding for *spam* before the
`global` assignment.

#### Generators

Generators are a simple and powerful tool for creating iterators. An example shows that generators can be trivially
easy to create

``` py
   def reverse(data):
       for index in range(len(data)-1, -1, -1):
           yield data[index]



   >>> for char in reverse('golf'):
   ...     print(char)
   ...
   f
   l
   o
   g
```


##### Generator Expressions

Some simple generators can be coded succinctly as expressions using a syntax
similar to list comprehensions but with parentheses instead of square brackets.

``` py
   >>> sum(i*i for i in range(10))                 # sum of squares
   285

   >>> xvec = [10, 20, 30]
   >>> yvec = [7, 5, 3]
   >>> sum(x*y for x,y in zip(xvec, yvec))         # dot product
   260

   >>> unique_words = set(word for line in page  for word in line.split())

   >>> valedictorian = max((student.gpa, student.name) for student in graduates)

   >>> data = 'golf'
   >>> list(data[i] for i in range(len(data)-1, -1, -1))
   ['f', 'l', 'o', 'g']

```

##### Iterators

By now you have probably noticed that most container objects can be looped over
using a `for` statement

``` py
   for element in [1, 2, 3]:
       print(element)
   for element in (1, 2, 3):
       print(element)
   for key in {'one':1, 'two':2}:
       print(key)
   for char in "123":
       print(char)
   for line in open("myfile.txt"):
       print(line, end='')
```

how it all works for iterator.

``` py
   >>> s = 'abc'
   >>> it = iter(s)
   >>> it
   <iterator object at 0x00A1DB50>
   >>> next(it)
   'a'
   >>> next(it)
   'b'
   >>> next(it)
   'c'
   >>> next(it)
   Traceback (most recent call last):
     File "<stdin>", line 1, in <module>
       next(it)
   StopIteration
```

Having seen the mechanics behind the iterator protocol, it is easy to add
iterator behavior to your classes.  Define an :meth:`__iter__` method which
returns an object with a :meth:`~iterator.__next__` method.  If the class
defines :meth:`__next__`, then :meth:`__iter__` can just return ``self``

``` py
   class Reverse:
       """Iterator for looping over a sequence backwards."""
       def __init__(self, data):
           self.data = data
           self.index = len(data)

       def __iter__(self):
           return self

       def __next__(self):
           if self.index == 0:
               raise StopIteration
           self.index = self.index - 1
           return self.data[self.index]

   >>> rev = Reverse('spam')
   >>> iter(rev)
   <__main__.Reverse object at 0x00A1DB50>
   >>> for char in rev:
   ...     print(char)
   ...
   m
   a
   p
   s

```

#### Coroutine Functions

``` py
```

#### Asynchronous generator functions

``` py
```

#### Builtin Functions

``` py
```

#### Builtin Methods

``` py
```

#### Classes

Classes provide a means of bundling data and functionality together. 

- Creating a new class creates a new *type* of object, allowing new *instances* of that type to be made.  
- Each class instance can have attributes attached to it for
maintaining its state. 
- Class instances can also have methods (defined by its
class) for modifying its state.

##### Class Definition Syntax

The simplest form of class definition looks like this:

``` py
   class ClassName:
       <statement-1>
       .
       .
       .
       <statement-N>
```

Some examples would be

``` py
class A:
    pass

class A(object):
    def function_a(self):

```

##### Class Objects

Class objects support 2 kinds of operations: 

- attribute references 
- instantiation.

*Attribute references* use the standard syntax used for all attribute references
in Python: `obj.name`.  Valid attribute names are all the names that were in
the class's namespace when the class object was created.  So, if the class
definition looked like this:

``` py
   class MyClass:
       """A simple example class"""
       i = 12345

       def f(self):
           return 'hello world'
```

then ``MyClass.i`` and ``MyClass.f`` are valid attribute references, returning
an integer and a function object, respectively. Class attributes can also be
assigned to, so you can change the value of ``MyClass.i`` by assignment.
:attr:`__doc__` is also a valid attribute, returning the docstring belonging to
the class: ``"A simple example class"``.

Class *instantiation* uses function notation.  Just pretend that the class
object is a parameterless function that returns a new instance of the class.
For example (assuming the above class):

``` py
   x = MyClass()
```

creates a new *instance* of the class and assigns this object to the local
variable ``x``.

The instantiation operation ("calling" a class object) creates an empty object.
Many classes like to create objects with instances customized to a specific
initial state. Therefore a class may define a special method named
:meth:`__init__`, like this:

``` py
   def __init__(self):
       self.data = []
``` 

When a class defines an :meth:`__init__` method, class instantiation
automatically invokes :meth:`__init__` for the newly-created class instance.  So
in this example, a new, initialized instance can be obtained by:

``` py
    x = MyClass()
```
Of course, the :meth:`__init__` method may have arguments for greater
flexibility.  In that case, arguments given to the class instantiation operator
are passed on to :meth:`__init__`.  For example,

``` py
   >>> class Complex:
   ...     def __init__(self, realpart, imagpart):
   ...         self.r = realpart
   ...         self.i = imagpart
   ...
   >>> x = Complex(3.0, -4.5)
   >>> x.r, x.i
   (3.0, -4.5)
```

#####  Instance Objects

Operations understood by instance objects are attribute references. There are two kinds of valid
attribute names: 

- data attributes
- methods.

Data attributes need not be declared; like local variables, they spring into existence when they are first assigned to.  For example, if ``x`` is the instance of `MyClass` created above, the following piece of
code will print the value ``16``, without leaving a trace

``` py
    x.counter = 1
    while x.counter < 10:
        x.counter = x.counter * 2
    print(x.counter)
    del x.counter
```

The other kind of instance attribute reference is a *method*. A method is a
function that "belongs to" an object.  (In Python, the term method is not unique
to class instances: other object types can have methods as well.  For example,
list objects have methods called append, insert, remove, sort, and so on.
However, in the following discussion, we'll use the term method exclusively to
mean methods of class instance objects, unless explicitly stated otherwise.)

Valid method names of an instance object depend on its class.  By definition,
all attributes of a class that are function objects define corresponding
methods of its instances.  So in our example, 

- ``x.f`` is a valid method reference
- ``MyClass.f`` is a function, but ``x.i`` is not, 
- ``MyClass.i`` is not.  
- ``x.f`` is not the same thing as ``MyClass.f`` --- it is a *method object*, not a function object.

##### Method Objects

Usually, a method is called right after it is bound

``` py
    x.f()
```

In the `MyClass` example, this will return the string ``'hello world'``.
However, it is not necessary to call a method right away: ``x.f`` is a method
object, and can be stored away and called at a later time.  

For example
``` py
    xf = x.f
    while True:
        print(xf())
```

will continue to print ``hello world`` until the end of time.


##### Class and Instance Variables

Generally speaking, 
- instance variables are for data unique to each instance
- class variables are for attributes and methods shared by all instances of the class

``` py
    class Dog:

        kind = 'canine'         # class variable shared by all instances

        def __init__(self, name):
            self.name = name    # instance variable unique to each instance

    >>> d = Dog('Fido')
    >>> e = Dog('Buddy')
    >>> d.kind                  # shared by all dogs
    'canine'
    >>> e.kind                  # shared by all dogs
    'canine'
    >>> d.name                  # unique to d
    'Fido'
    >>> e.name                  # unique to e
    'Buddy'
```

As discussed in `tut-object`, shared data can have possibly surprising
effects with involving `mutable` objects such as lists and dictionaries.
For example, the *tricks* list in the following code should not be used as a
class variable because just a single list would be shared by all *Dog*
instances

``` py
    class Dog:

        tricks = []             # mistaken use of a class variable

        def __init__(self, name):
            self.name = name

        def add_trick(self, trick):
            self.tricks.append(trick)

    >>> d = Dog('Fido')
    >>> e = Dog('Buddy')
    >>> d.add_trick('roll over')
    >>> e.add_trick('play dead')
    >>> d.tricks                # unexpectedly shared by all dogs
    ['roll over', 'play dead']
```

Correct design of the class should use an instance variable instead

``` py
    class Dog:

        def __init__(self, name):
            self.name = name
            self.tricks = []    # creates a new empty list for each dog

        def add_trick(self, trick):
            self.tricks.append(trick)

    >>> d = Dog('Fido')
    >>> e = Dog('Buddy')
    >>> d.add_trick('roll over')
    >>> e.add_trick('play dead')
    >>> d.tricks
    ['roll over']
    >>> e.tricks
    ['play dead']
```

##### Random Remarks

If the same attribute name occurs in both an instance and in a class,
then attribute lookup prioritizes the instance

``` py
    >>> class Warehouse:
            purpose = 'storage'
            region = 'west'

    >>> w1 = Warehouse()
    >>> print(w1.purpose, w1.region)
    storage west
    >>> w2 = Warehouse()
    >>> w2.region = 'east'
    >>> print(w2.purpose, w2.region)
    storage east
```

Methods may call other methods by using method attributes of the ``self``
argument:

``` py
   class Bag:
       def __init__(self):
           self.data = []

       def add(self, x):
           self.data.append(x)

       def addtwice(self, x):
           self.add(x)
           self.add(x)
```

Often, the first argument of a method is called ``self``.  This is nothing more
than a convention: the name ``self`` has absolutely no special meaning to
Python.  Note, however, that by not following the convention your code may be
less readable to other Python programmers, and it is also conceivable that a
*class browser* program might be written that relies upon such a convention.

``` py
   class Bag:
       def __init__(classself):
           classself.data = []

       def add(self, x):
           classself.data.append(x)

       def addtwice(self, x):
           classself.add(x)
           classself.add(x)
```

##### Odds and Ends

Sometimes it is useful to have a data type similar to the Pascal "record" or C
"struct", bundling together a few named data items.  An empty class definition
will do nicely

``` py
   class Employee:
       pass

   john = Employee()  # Create an empty employee record

   # Fill the fields of the record
   john.name = 'John Doe'
   john.dept = 'computer lab'
   john.salary = 1000
```

### Modules

TBD

### I/O objects (also known as file objects)

TBD

### *Args and **Kwargs

``` py
    def some_function(*args, **kwargs):
        # get the first item from args
        item1 = args[0]
        return

    def some_function(a, b, c, *args, **kwargs):
        # get the first item from kwargs
        item1 = kwargs.get('some_value', None)
        return
```

## Special Method Names

TBD

## References

- [The standard type hierarchy](https://docs.python.org/3/reference/datamodel.html#the-standard-type-hierarchy)
- [Classes](https://docs.python.org/3/tutorial/classes.html)
