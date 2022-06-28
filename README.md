# Instance Methods

## Learning Goals

- Describe an instance method.
- Call instance methods on an object.
- Build instance methods for an object.

***

## Key Vocab

- **Class**: a bundle of data and functionality. Can be copied and modified to
accomplish a wide variety of programming tasks.
- **Initialize**: create a working copy of a class using its `__init__()`
method.
- **Instance**: one specific working copy of a class. It is created when a
class's `__init__()` method is called.
- **Object**: the more common name for an instance. The two can usually be used
interchangeably.
- **Object-Oriented Programming**: programming that is oriented around data
(made mobile and changeable in **objects**) rather than functionality. Python
is an object-oriented programming language.
- **Procedural Programming**: programming that is oriented around procedures
that are called in sequential order. Fortran and C are procedural programming
languages.
- **Function**: a series of steps that create, transform, and move data.
- **Method**: a function that is defined inside of a class.
- **Magic Method**: a special type of method in Python that starts and ends
with double underscores. These methods are called on objects under certain
conditions without needing to use their names explicitly. Also called **dunder
methods** (for **d**ouble **under**score).
- **Attribute**: variables that belong to an object.
- **Property**: attributes that are controlled by methods.

***

## Introduction

We know that classes are a collection of data and functionality that act as a
factory for our objects. We create those objects by calling our class just as
we would a function, with closed parentheses:

```py
class Dog:
    pass

fido = Dog()
# <__main__.Dog object at 0x1027f07f0>
```

But what can this instance of a dog stored in the local variable `fido` do? In
fact, how do we even ask this object to do something?

***

## The Behavior of Objects

Objects on their own don't do very much. In order to see the behavior of an
object, we need to interact with it to elicit a response. There are certain
strategies for interacting with objects that allow us to access their data and
functionality from the outside.

### Dot Notation

We send objects messages asking them to perform an operation or task through a
syntax known as "Dot Notation".

```py
class Dog:
    pass

fido = Dog()
# <__main__.Dog object at 0x1027f07f0>

fido.__dir__()
# ['__module__', '__dict__', '__weakref__', '__doc__', '__repr__', '__hash__',
# '__str__', '__getattribute__', '__setattr__', '__delattr__', '__lt__',
# '__le__', '__eq__', '__ne__', '__gt__', '__ge__', '__init__', '__new__',
# '__reduce_ex__', '__reduce__', '__subclasshook__', '__init_subclass__',
# '__format__', '__sizeof__', '__dir__', '__class__']
```

When we interact with an object through dot notation, we are calling the
variable or function that is defined inside of the object. We call these
instance variables **attributes** and these instance functions **methods**.
Unless otherwise specified, all of an object's methods are considered
**instance methods**. **Instance methods** can access and modify the
attributes of an instance.

In the example above, we access the `fido` instance's `__dir__()` method by
separating the object, `fido` and the method, `__dir__()` by a dot
(`.`).

The `__dir__()` method provides you with a list of the object's methods and
attributes. You'll notice that even though we didn't provide the `Dog` class
with any attributes or methods, it has many by default!

> I thought of objects being like biological cells and/or individual computers
> on a network, only able to communicate with messages. - Alan Kay

```py
"Strings are objects too.".upper()
# 'STRINGS ARE OBJECTS TOO.'
```

### Exploring Instance Methods

All objects respond to methods (messages), like `#object_id` in the example
above. One interesting method that is available on all objects in Ruby is the
`#methods` method. Calling `#methods` on an object returns an array of all the
methods (messages) an object responds to. We can invoke this method via
dot-notation.

One of the great things you can ask every object in Ruby is "What methods do you
respond to?" To see for yourself, try this out in IRB:

```ruby
class Dog
end

fido = Dog.new
fido.methods
#=> [:psych_to_yaml, :to_yaml, :to_yaml_properties, :local_methods, :try, :nil?,
# :===, :=~, :!~, :eql?, :hash, :<=>, :class, :singleton_class, :clone, :dup,
# :itself, :taint, :tainted?, :untaint, :untrust, :untrusted?, :trust, :freeze,
# :frozen?, :to_s, :inspect, :methods, :singleton_methods, :protected_methods,
# :private_methods, :public_methods, :instance_variables,
# :instance_variable_get, :instance_variable_set, :instance_variable_defined?,
# :remove_instance_variable, :instance_of?, :kind_of?, :is_a?, :tap, :send,
# :public_send, :respond_to?, :extend, :display, :method, :public_method,
# :singleton_method, :define_singleton_method, :object_id, :to_enum, :enum_for,
# :==, :equal?, :!, :!=, :instance_eval, :instance_exec, :__send__, :__id__]
```

As you can see, out of the box, our objects can do a lot of things. Where these
things come from and what they do are not so important right now because all of
that functionality is very low level and not interesting to our Dogs.

### Building Your Own Instance Methods

If you haven't already, fork and clone this lab to your local environment and
run `learn test`. Follow along below to get the first few tests for the `Dog`
class to pass. Once you have those passing, you will complete the remaining
tasks on your own.

How do we add our own methods to our classes? In our Dog example, can we teach
our Dog a new trick? Can we teach our Dog to bark for example?

We can. We're used to defining methods already with the `def` keyword. If we
place this method definition within the body of a class, that method becomes a
specific behavior of instances of that class, not a generic procedure we can
just call whenever we want.

We call the methods defined within the object's class **Instance Methods**
because they are methods that belong to any instance of the class.

Let's create our `Dog` class in `lib/dog.rb`. It's a convention among Rubyists
to define each class in its own file, using the class name to determine the file
name.

In the `Dog` class, let's define our `#bark` instance method:

```ruby
class Dog
  # Class body

  # Instance Method Definition
  def bark
    puts "Woof!"
  end
end
```

With this code in place, if you run the tests you should now be passing the
first three tests.

Now let's create an instance of `Dog` and verify that our `Dog` object knows how
to bark:

```ruby
class Dog
  def bark
    puts "Woof!"
  end
end

fido = Dog.new
fido.bark #=> "Woof!"
```

If you execute this code in the terminal by running `ruby lib/dog.rb`, you
should see "Woof!" written out.

By defining `#bark` within the `Dog` class, `bark` becomes a method of all
instances of Dogs. Let's create a second instance of `Dog`, `snoopy`, and verify
that snoopy also knows how to bark by running `ruby lib/dog.rb` again.

```ruby
class Dog
  def bark
    puts "Woof!"
  end
end

fido = Dog.new
fido.bark #=> "Woof!"

snoopy = Dog.new
snoopy.bark #=> "Woof!"
```

Objects can only do what we teach them to do via the code we write and the
methods we define. For example, currently, Dogs do not know how to sit.

```ruby
class Dog
  def bark
    puts "Woof!"
  end
end

fido = Dog.new
fido.bark #=> "Woof!"
fido.sit #=> NoMethodError: undefined method `sit' for #<Dog:0x007fa4e9a9e8a0>
```

In the same manner, instance methods, the methods that belong to particular
instances of particular classes, cannot be used globally like procedural
methods. They cannot be called without an instance.

```ruby
class Dog
  def bark
    puts "Woof!"
  end
end

fido = Dog.new

# Let's try just calling bark without fido
bark #=> NameError: undefined local variable or method `bark' for main:Object
```

***

## Instructions

Complete the following tasks to get the rests of the tests passing:

1. Add an instance method `#sit` to your `Dog` class that will puts "The Dog is sitting".
2. Define a `Person` class in `lib/person.rb`
3. Add an instance method `#talk` to your Person class that will puts "Hello World!"
4. Add an instance method `#walk` to your Person class that will puts "The Person is walking".

### Additional Note on Lab Testing

In this lab, we asked that you code your two classes in separate `dog.rb` and
`person.rb` files. You could, in theory, code both classes in the same file, or
even _code them in opposite files_ and still pass all tests. Why do you think
that is?

...

...

When the tests are run in this lab, RSpec loads both the `dog.rb` and
`person.rb` files (this happens in the first two lines of `spec/spec_helper.rb`
using [`require_relative`][]). As long as you place your classes in one of the
files that RSpec loads, the tests will have access to them.

[`require_relative`]: https://apidock.com/ruby/Kernel/require_relative

While it isn't enforced, we do encourage you to separate classes into
individual, accurately named files. In a larger application, you might not
always need to load the `Dog` class when loading the `Person` class. As classes
get larger, it also becomes easier to manage your code if you know each file
contains _one_ class. Keeping to these conventions makes it easier in the future
to go back and read code you've previously written.

***

## Conclusion

With all tests passing, you have successfully written multiple instance methods
and _two_ different classes!

The ability to define methods and behaviors in our classes for our instances
makes Ruby classes behave not just as factories, capable of instantiating new
individual instances, but also as a blueprint, defining what those instances can
do.

***

## Resources

- [Python documentation][python docs]
- [Object-Oriented Programming (OOP) in Python 3](https://realpython.com/python3-object-oriented-programming/)
- [Differences Between Procedural and Object-Oriented Programming](https://www.geeksforgeeks.org/differences-between-procedural-and-object-oriented-programming/#:~:text=Object%2Doriented%20programming%20is%20based,the%20concept%20of%20procedure%20abstraction.)

[python docs]: https://docs.python.org/3/
