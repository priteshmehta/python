
# Python Tips & Tricks

### Scope of List:
```
def extendList(val, list=[]):
  list.append(val)
  return list

#it extends same list
extendList(1)
extendList(2)
print(extendList(3))
```

### Functions References
```
def b():
  print "b() called "
  return c
def c():
  print "C() called"

def a():
  print "a() Called"
  return b

a()()()
```

### Object References:
```
import sys
print("get reference count:", sys.getrefcount(tmp))

a = "10"
print ("get reference count:", sys.getrefcount(a))
```

## Decorator Concept

https://realpython.com/primer-on-python-decorators/#decorating-classes

#### Without decorator 

```
def welcome_message(name):
    def get_message():
        return "Hello! "
    return get_message() + name

print(welcome_message("Pritesh"))
```

#### With decorator
```
def greet(greet_str):
    def _greet(fn):
        def __greet(*args, **kwargs):
            return greet_str  + " " + fn(*args, **kwargs)
        return __greet
    return _greet

@greet("Hello!")
def welcome_message(name):
    return name


print(welcome_message("Pritesh"))

####### using functools #############
import functools
def greet(greet_str):
    def _greet(fn):
        @functools.wraps(fn)
        def __greet(*args, **kwargs):
            return greet_str + " " + fn(*args, **kwargs)

        return __greet

    return _greet


@greet("Hello!")
def welcome_message(name):
    return name

####### class as decorator #############
import functools

class CountCalls:
    def __init__(self, func):
        functools.update_wrapper(self, func)
        self.func = func
        self.num_calls = 0

    def __call__(self, *args, **kwargs):
        self.num_calls += 1
        print(f"Call {self.num_calls} of {self.func.__name__!r}")
        return self.func(*args, **kwargs)

@CountCalls
def say_whee():
    print("Whee!")
```

### Other types Decorator on classes
```
Decorators on classes
Several decorators on one function
Stateful decorators
Classes as decorators
```

### Assign function in variable

```
a = my_func
a()
print("Name of function: {}".format(a.__name__))
```

### Determin function name withing function

```

import inspect
whoami = lambda: inspect.stack()[1][3]

def my_func():
    print ("hello! {}".format(whoami())

my_func()
```

## Megic Methods
```

class MyClass(object):
  
  #This method gets called on object instantiation
  def __new__(cls):
    print "__new__ Called."
  
  #It always gets called on instancetiating class ( my_class_obj = MyClass() or MyClass().any_class_method())
  def __init__(self):
    print "__init__ Called."

  #It always gets called on calling object ( e.g. my_class_obj())
  def __call__(self):
    pass

  #It gets called when deleting object (e.g. del my_class_object). We don't normaly do it in python. 
  #python's garbage collector (gc) takes care of it.
  def __del__(self):
    pass

  #Defines behaviour for the equality operators
  def __eq__(self, obj):
    pass
  
  def __ne__(self, obj):
    pass

  def __lt__(self, obj): 
    pass

  def __gt__(self, obj):
    pass

  def __ge__(self, obj):
    pass

  def __le__(self, obj):
    pass


  #Unary operators and functions 

  def __neg__(self):
    pass

  def __abs__(self): 
    pass #same as built in abs()

  __floor__ (same as built in floor())

  __ceil__ (same as built in ceil())



```

### Variable scope withing python class

```
class MyClass(object):
  def __init__(self):
    self.normal_variable=1      
    self._local_variable=1      
    self.__private_variable=1   #only accessible by class methods


  def _local_method(self):
    """weak "internal use" indicator. 
       e.g. "from x import *" does not import object whose name starts with an underscore.
    """
    pass

  def local_method(self):
    """Accessible by objects
    """
    pass

  def __private_local_method(self):
    """internal use only. can't be accessible by an object.
        However there is way to call but should not advisable to do so
        MyClass()._MyClass__private_local_method() - This is called 'Name Mangling'

    """
    pass


```


###  Static Methods And Class Methods


```
class MyClass(object):
  @staticmethod
  def the_static_method():
    print "Static method called"

  @classmethod
  def the_class_method(cls):
    print "Class method called"


MyClass.the_class_method()
the_static_method()

```


#### Properties (getter & setter) concept

```
class C (object):
  def __init__(self):
      self._age=10

  @property
  def age(self):
    return self._age

  @age.setter
  def age(self, value):
    print("Setting value")
    self._age = value

c1= C()
print c1.age 

```



### Python Peculiarity

## Run following commands in Python shell
```
import this
import __hello__ 
import __phello__
import antigravity
```

## List extend vs append
```

my_list = []
my_list.extend("string")

my_list2 = []
my_list2.append("string")

print("Extends: {}".format(my_list))
print("Appends: {}".format(my_list2))
```


## Reverse a string in pythoninc way

```
a = "Python"
print "Reverse is",a[::-1]
```

## Passing reference

```
a = [1]

def change_value():
  a.append(2)

change_value()
print a
```

## Shallow copy of list

```
a = [1,2,3]
b = a
b.append(10)
print "Value of a: ",a
print "Value of b: ",b

```


## String comparison using numeric operator

```
if "this"> "that":
  print "True"

```

## Convert Nested list into single list

```

import itertools
nested_list = [[1, 2], [3, [10], 4], [5, 6]]
flat_list = list(itertools.chain.from_iterable(a))
print flat_list

```

## Further Reading

1. [Useful Tips](https://sahandsaba.com/thirty-python-language-features-and-tricks-you-may-not-know.html#multisets-and-multiset-operations-)
2. [Python Challenge](http://www.pythonchallenge.com)



