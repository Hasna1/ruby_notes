!SLIDE subsection
# Introduction to Ruby for Programmers

<img src="ruby-logo.jpg" width="250">

!SLIDE

## Ruby is a Language
<img src="ruby-logo.jpg" height="125" width="125">

## Rails is a Framework
<img src="rails_logo.jpg" height="125" width="125">

<!SLIDE incremental>

"People want to express themselves when they program."

"They don't want to fight with the language."

"Programming languages must feel natural to programmers."

"I tried to make people enjoy programming and concentrate on the fun and creative part of programming when they use Ruby."

&nbsp;- Matz (Yukihiro Matsumoto)

!SLIDE incremental
# Oh, the humanity

Ruby has a *humane interface*

(contrast to *minimal interface*)

readability and variety over concision and perfection

sometimes makes code hard to understand (but usually makes it easier)

!SLIDE

## Ruby 1.0 released in 1996
## Open Source
## Many implementations
  * MRI
    * REE
    * Kiji
  * JRuby
  * Rubinius
  * MagLev
  * MacRuby
  * IronRuby


# Ruby Language Overview
* Dynamically typed
* Interpreted
* Can be modified at runtime
* Object oriented
* Blocks / lambdas / closures
* Perl-like regular expressions
* Closely tied to shell & OS

!SLIDE

# IRB: Interactive RuBy

!SLIDE

    @@@ ruby
    $ irb
    >> 4
    => 4
    >> 4+4
    => 8

!SLIDE

# Everything is an object

!SLIDE

    @@@ ruby
    "test".upcase   #=> "TEST"
    "test".class    #=> String

    "test".methods
    2.methods
    
    1.to_s       #=> "1"
    "1".to_i     #=> 1
    :hello.class #=> Symbol

!SLIDE

# Everything evaluates to something

!SLIDE

    @@@ ruby
    >> 2 + 2
    => 4
    >> (2+2).zero?
    => false
    >> "foo" if false
    => nil

!SLIDE

# Methods are messages

!SLIDE

    @@@ ruby
    thing.do(4)
    thing.do 4
    thing.send "do", 4

!SLIDE

# Operators are Methods

!SLIDE

    @@@ ruby
    1 + 2
    1.+(2)
    1.send "+", 2

!SLIDE
# Hash mark comments, like perl

    @@@ ruby
    # is a comment
    2 + 2 # is a comment

!SLIDE

Ruby aims to be elegant and readable

so punctuation and boilerplate are minimal

!SLIDE

# Optional semicolons, parens, and `return`

These are equivalent:

    @@@ ruby
    def inc x
      x + 1
    end

    def inc(x)
      return x + 1;
    end

    def inc(x); x + 1; end
    
# Gotcha

    @@@ ruby
    x = 1 + 2
    x #=> 3
    
    x = 1
      + 2      
    x #=> 1

    x = 1 +
        2      
    x #=> 3

!SLIDE

# Use parens when you need them

!SLIDE

    @@@ ruby
    >> "Hello".gsub 'H', 'h'
    => "hello"

    >> "Hello".gsub("H", "h").reverse
    => "olleh"

!SLIDE
# Variables

variables are implicitly declared

    @@@ ruby
    first_name = "Santa"
    last_name = "Claus"
    full_name = first_name + last_name
    #=> "SantaClaus"

!SLIDE bullets

# Built-in Types

* Symbols
* Arrays
* Hashes
* Strings
* Ranges
* Numbers
* Boolean

!SLIDE

# Symbols
## :a_symbol

There is only one representation of a given symbol in memory, so it really
means "the thing named :a_symbol" to the ruby interpreter.

In Ruby, we prefer symbols over hardcoded globals or strings. They're very lightweight.

!SLIDE
# Array

* sized dynamically
* can contain mixed types
* zero-indexed
* can be defined *literally* (inline) e.g.

      @@@ ruby
      fruits = ["apple", "banana"]

!SLIDE

    @@@ ruby
    a = [1, 2, 3]
    a.push "four" #=> [1, 2, 3, "four"]
    a.pop         #=> "four"
    a             #=> [1, 2, 3]
    a[0]          #=> 1

!SLIDE incremental

# Hash

* also known as...
  * Map
  * Associative Array
  * Dictionary
  * Name/Value Pair Store
  * Key/Value Pair Store
* can be defined *literally* (inline) e.g.

        @@@ ruby
        letter_fruits = {"A" => "apple",
          "B" => "banana"}


!SLIDE

    @@@ ruby
    states = {"MA" => "Massachusetts",
              "CA" => "California"}

    states["MA"] #=> "Massachusetts"

!SLIDE

    @@@ ruby
    my_hash = {:a_symbol => 3, "a string" => 4}
    my_hash[:a_symbol] #=> 3
    
    my_hash[:foo] = "bar"
    my_hash #=> {:a_symbol => 3, "a string" => 4, :foo => "bar"}
    

!SLIDE
# String

[todo]

!SLIDE

# String interpolation

    @@@ ruby
    "boyz #{1 + 1} men"
    => "boyz 2 men"

Any Ruby code can go inside the braces

It gets evaluated and stuck inside the string

same as:

    @@@ ruby
    "boyz " + (1 + 1).to_s + " men"


!SLIDE

    @@@ ruby
    >> a = "world"
    >> puts "hello #{a}"
    hello world

    >> a = 2
    >> puts "hello #{a}"
    hello 2

    >> a = nil
    >> puts "hello #{a} there"
    hello  there


!SLIDE subsection

# Iterators

!SLIDE

    @@@ ruby
    my_array = ["cat", "dog", "world"]
    my_array.each do |item|
      puts "hello " + item
    end

!SLIDE

    @@@ ruby
    my_hash = { :type => "cat",
                :name => "Beckett",
                :breed => "alley cat" }
    my_hash.each do |key, value|
      puts "My " + key.to_s + " is " + value
    end


!SLIDE incremental
# The Default Block

* Methods can take block arguments
* Use either `do...end` or `{...}` at the very end of the argument list
* Inside the method, call the default block with `yield`

!SLIDE

    @@@ ruby
    fruits = ["apple, "banana", "cherry", "date"]
    my_array.each do |item|        #<< start of default block
      puts "Yum! I love #{item}!"
    end                            #<< end of default block   

!SLIDE

    @@@ ruby
    def twice
       yield
       yield
    end

    twice do
      puts "hi"
    end
    
"twice do" kind of almost resembles English a little, right?

!SLIDE
Blocks can also take parameters or return a value

The `map` iterator translates each item in an array into a new array


    @@@ ruby
    >> ["hello", "world"].map{ |string| string.upcase }
    => ["HELLO", "WORLD"]

!SLIDE
# Variable Scoping

    @@@ ruby
    var
    @var
    @@var
    $var
    VAR

!SLIDE
# Variable Scoping

    @@@ ruby
    var   # could be a local variable
    @var  # instance variable
    @@var # class variable
    $var  # global variable
    VAR   # constant

!SLIDE subsection

# Classes and methods

!SLIDE

    @@@ ruby
    class Thing
      def return_something
        "something"
      end
    end

!SLIDE

    @@@ ruby
    class Thing
      def do_something(a,b)
        a + b
      end
    end


!SLIDE subsection

# more neat things about ruby

!SLIDE incremental

# duck typing

If it looks like a duck, and quacks like a duck...

We don't care what an object is as long as it does what we want

!SLIDE

    @@@ ruby
    def print_even_or_odd(array_like_thing)
      array_like_thing.each do |item|
        puts "#{item} is #{item.even? ? "even" : "odd"}."
      end
    end

!SLIDE

    @@@ ruby
    print_even_or_odd [1, 2, 3]
    print_even_or_odd 1..3

!SLIDE incremental

# Modules and Mixins

* Any class (or object) can *include* a Module
  * also known as *mixing in*
  * so Modules are also called *mixins*
* Modules provide *behavior* but no *state*
  * more precisely, they affect the extending object's state
* Provides most of the power of multiple inheritance, but less confusing

!SLIDE
# Array Assignment

    @@@ ruby
    @width, @height = width, height
    @width, @height = [width, height]

    def dimensions
      [10, 20]
    end
    @width, @height = dimensions

!SLIDE

# Metaprogramming

* macros (class methods)
  * `attr_accessor`
  * `has_many`

!SLIDE incremental
# Classes are objects

* class methods are really just methods on the class object
* code evaluated in the scope of a class definition acts on the class object

!SLIDE
# Domain-Specific Languages (DSLs)

* Rails
* Rake
* Cucumber
* Rspec
* etc.

!SLIDE

# the `method_missing` method

!SLIDE incremental

# private vs public

* Private really just means "please don't come in."
* If someone has access to your runtime environment, they are trusted.
* Spend your time writing code (and testing it), not protecting yourself from other code

!SLIDE
# bang and question methods

* method names can end with `!` or `?`
  * `!` means "watch out!"
  * `?` means "boolean"

!SLIDE
# Reopening classes

    @@@ ruby
    class Fixnum
      def even?
        self % 2 == 0
      end
    end

    1.even? #=> false

!SLIDE
# or-equals

    def name
      @name ||= "Anonymous"
    end
    
* Means "if @name has a value, use it, but otherwise make it 'Anonymous'"
* Relies on "logical or" and "nil is false" semantics
* There's also "plus-equals" (`+=`) and so forth

!SLIDE
# Credits

* Based upon [Ruby Quickstart for Refugees](https://gist.github.com/190567)
* Improved by Sarah Allen, Alex Chaffee, and others


