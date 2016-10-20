

**Neen’s OOP Glossary**
===================

>Please feel free to suggest edits! I'd really appreciate if this list grows and grows! 

----------


##Abstraction

The inner implementation details and showing only outer details. Hides all but the relevant data about an object in order to reduce complexity and increase efficiency

Abstraction is hiding the information or providing only necessary details to the client.

e.g Car Brakes- You just know that pressing the pedals will stop the vehicle but you don't need to know how it works internally.


----------


##AbstractClass


A class primarily intended to define an instance, but can not be instantiated without additional methods.


----------


##Aggregation

Objects that are made up of other objects are known as aggregations. The relationship is generally of one of two types:


 1. **Composition** – the object is composed of other objects. This form of aggregation is a form of code reuse.
    E.g. A Car is composed of Wheels, a Chassis and an Engine

 2. **Collection** – the object contains other objects.
    E.g. a List contains several Items; A Set several Members.


----------

##Classes

A class can be thought of as a template to create many objects with similar qualities. Classes are a fundamental component of object-oriented programming (OOP).

A category of objects, classified according to the members that they have.

Their primary function is as factories for objects in the category


----------


##Closure

A closure is an inner function that has access to the outer (enclosing) function’s variables—scope chain. The closure has three scope chains: it has access to its own scope (variables defined between its curly brackets), it has access to the outer function’s variables, and it has access to the global variables.

Closures have access to the outer function’s variable even after the outer function returns

Closures store references to the outer function’s variables; they do not store the actual value. Closures get more interesting when the value of the outer function’s variable changes before the closure is called.


----------


##ConstructorFunctions

Constructors are like regular functions, but we use them with the "new" keyword. A constructor is useful when you want to create multiple similar objects with the same properties and methods. It’s a convention to capitalize the name of constructors to distinguish them from regular functions.

    function Book() {
      // unfinished code
    }
    var myBook = new Book();

----------


##Composition
not to be confused with function composition - is a way to combine simple objects or data types into more complex ones.

when a class is composed of other classes; or to say it another way, an instance of an object has references to instances of other objects.


----------


##Delegation

JavaScript’s method of implementing inheritance: delegation.
When we call capybara.size, JavaScript first looks for that property in the capybara object. If not found, it looks for the property in capybara.__proto__. If it didn’t find it in capybara.__proto__, it would look incapybara.__proto__.__proto__. This is known as the prototype chain.


----------


##Encapsulation

Is the process of combining data and functions into a single unit called class. In Encapsulation, the data is not accessed directly; it is accessed through the functions present inside the class. In simpler words, attributes of the class are kept private and public getter and setter methods are provided to manipulate these attributes. Thus, encapsulation makes the concept of data hiding possible.


----------


##ExecutionContexts

 The environment / scope the current code is being evaluated in.

 ![Execution Context image](http://tinyimg.io/i/FGaO53x.png)


----------

##Inheritance

Enables new objects to take on the properties of existing objects. A class that is used as the basis for inheritance is called a superclass or base class. A class that inherits from a superclass is called a subclass or derived class. The terms parent class and child class are also acceptable terms to use respectively. A child inherits visible properties and methods from its parent while adding additional properties and methods of its own.
Subclasses and superclasses can be understood in terms of the is a relationship. A subclass is a more specific instance of a superclass. For example, an orange is a citrus fruit, which is a fruit. A shepherd is a dog, which is an animal.


----------


##Instantiation
--
Instantiation is the creation of an instance of an object class (also known as a template). Each instance created by instantiation is unique depending on the variation of the elements within the object. Until an object becomes instantiated, none of the code within the relevant class declarations is used.


----------


##InstantiationPatterns

- Functional Instantiation
- Functional-shared instantiation
- Prototypal instantiation
- Pseudoclassical instantiation


----------


##FunctionalInstantiation

We create a function, and inside it, we can create an empty object, some scoped variables, some instance variables, and some instance methods. At the end of it all, we can return that instance, so that every time the function is called, we have access to those methods.

    // Set up
    var Func = function() {
      var someInstance = {};
      var a = 0;
      var b = 1;

      someInstance.logA = function() {
        return a;
      }
      return someInstance;
    }

    // Usage
    var myFunc = Func();
    myFunc.logA(); // returns a

>**Pros:** This pattern is the easiest to follow, as everything exists inside the function. It's instantly obvious that those methods and variables belong to that function.


>**Cons:** This pattern creates a new set of functions in memory for each instance of the function Func. If you're creating a big app, it's ultimately just not suitable in terms of memory.


----------


##Functional-sharedInstantiation**

Functional-shared instantiation is similar to functional instantiation, but the methods are an extension of the function instead.

    // Set up
    var Func = function() {
      var someInstance = {};
      someInstance.a = 0;
      someInstance.b = 1;
      extend(someInstance, funcMethods);

      return someInstance;
    }

    var extend = function(to, from) {
      for (var key in from) {
        to[key] = from[key];
      }
    }

    var funcMethods = {};

    funcMethods.method1 = function() {
      // code for method1 here...
    }

    funcMethods.method2 = function() {
      // code for method2 here...
    }

    funcMethods.logA = function() {
      return this.a;
    }

    // Usage
    var myFunc = Func();
    myFunc.logA(); // returns a


>**Pros:** Tn this instantiation pattern, the object methods are referenced in memory, so object instances refer to those references when being called. This allows for great memory management.

>**Cons: ** **strong text**If we choose to edit some of the funcMethods at some point and then create a new object instance, the old and new instances will refer to different references of the method in memory. This can get confusing for some, but is a minor caveat once you're aware of it.


----------

##PrototypalInstantiation

Prototypal instantiation (which doesn't actually use the keyword prototype) is done by attaching methods directly to the object's prototype using the Object.create() method.

    // Set up
    var Func = function() {
      var someInstance = Object.create(funcMethods);
      someInstance.a = 0;
      someInstance.b = 1;

      return someInstance;
    }

    var funcMethods = {};

    funcMethods.method1 = function() {
      // code for method1 here...
    }

    funcMethods.method2 = function() {
      // code for method2 here...
    }

    funcMethods.logA = function() {
      return this.a;
    }

    // Usage
    var myFunc = Func();
    myFunc.logA(); // returns a



>**Pros:** This pattern attaches methods directly to the object's prototype, rather than as attachments to the returned objects like before.

>**Cons:** In my opinion, there is room for improvement on this pattern. Even though the pros are great, it's still a bit of a long-winded implementation.

-----

##PsuedoClassicalInstantiation

Takes a bit of the long-windedness out of the prototypal pattern. It does, as before, attach methods directly to the object's prototype. Another point of interest is the fact that the object's constructor is automatically included. This means that we can create new instances using the new keyword.

    this = Object.create(Object.prototype); and return this; get run in the background


    // Set up
    var Func = function() {
      this.a = 0;
      this.b = 1;
    }

    Func.prototype.method1 = function() {
      // code for method1 here...
    }

    Func.prototype.method2 = function() {
      // code for method2 here...
    }

    Func.prototype.logA = function() {
      return this.a;
    }

    var myFunc = new Func();
    myFunc.logA(); // returns a


___

##LexicalScopes/In-memoryScopes

Lexical scoping (sometimes known as static scoping ) is a convention used with many programming languages that sets the scope (range of functionality) of a variable so that it may only be called (referenced) from within the block of code in which it is defined. The scope is determined when the code is compiled. A variable declared in this fashion is sometimes called a private variable.

![Lexical Scopes in Action](http://tinyimg.io/i/FpZCf6h.png)

---

##DynamicScoping
The opposite approach is known as dynamic scoping . Dynamic scoping creates variables that can be called from outside the block of code in which they are defined. A variable declared in this fashion is sometimes called a public variable.

---

##MessagePassing
In an object oriented approach, objects do things themselves. A "message" is the terminology used when telling an object to do something.

The opposite is a procedural approach, where code gets some information elsewhere, and then acts based on the information provided.

---

##Method

JavaScript methods are the actions that can be performed on objects. A JavaScript method is a property containing a function definition. Property.

---

##Modules

Good authors divide their books into chapters and sections; good programmers divide their programs into modules.

Like a book chapter, modules are just clusters of words (or code, as the case may be).
Good modules, however, are highly self-contained with distinct functionality, allowing them to be shuffled, removed, or added as necessary, without disrupting the system as a whole.

---

##Polymorphism

Polymorphism is one of the tenets of Object Oriented Programming (OOP). It is the practice of designing objects to share behaviors and to be able to override shared behaviors with specific ones. Polymorphism takes advantage of inheritance in order to make this happen.

So in order to facilitate this, we will first write out the super class (Person)

    function Person(age,weight){
     this.age = age;
     this.weight = weight;
    }

And we will give Person the ability to share their information


    Person.prototype.getInfo = function(){
     return "I am " + this.age + " years old " +
        "and weighs " + this.weight +" kilo.";
    };



Next we wish to have a subclass of Person, Employee

    function Employee(age,weight,salary){
     this.age = age;
     this.weight = weight;
     this.salary = salary;
    }
    Employee.prototype = new Person();

And we will override the behavior of getInfo by defining one which is more fitting to an Employee

    Employee.prototype.getInfo = function(){
     return "I am " + this.age + " years old " +
        "and weighs " + this.weight +" kilo " +
        "and earns " + this.salary + " dollar.";
    };

---

##PrototypeDelegation/Chains

What some developers refer to as a "class", is actually just a function, with other functions assigned to its .prototype property; which, in turn, is called with new in order to treat the function like a constructor


    // Not a 'class', just a function
    function Person(name) {
      this.name = name;
    }
    Person.prototype.hello = function() {
      console.log("Hello, my name is " + this.name);
    };

    // invoke our function with `new` for magical constructor behavior
    var dave = new Person("Dave");
    dave.hello();
    // "Hello, my name is Dave"

The .prototype property of Person above is an actual property on the Person function (functions are objects). This property is treated as an object and used to create the actual prototype to which our new object is linked.

![Graph of the delegation chain](http://tinyimg.io/i/v55sxJv.png)

---

##Recursion
The calling of a function from within that same function.A recursive function must always check for a condition to determine if it should call itself again or not.

---

##RefactoringCode

Code refactoring is the process of restructuring existing computer code—changing the factoring—without changing its external behaviour.
setter method

Getters and Setters allow you to build useful shortcuts for accessing and mutating data within an object. Generally, this can be seen as an alternative to having two functions with an object that are used to get and set a value.



    function Name(first, last) {
        this.first = first;
        this.last = last;
    }

    Name.prototype = {
        get fullName() {
            return this.first + " " + this.last;
        },

    set fullName(name) {
        var names = name.split(" ");
        this.first = names[0];
        this.last = names[1];
    }





##Stack

The JavaScript interpreter in a browser is implemented as a single thread. What this actually means is that only 1 thing can ever happen at one time in the browser, with other actions or events being queued in what is called the Execution Stack. The diagram below is an abstract view of a single threaded stack:


![dat stack tho](http://tinyimg.io/i/k8YJnU7.png)








