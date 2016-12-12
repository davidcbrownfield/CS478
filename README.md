# Program Languages

----
### <a name="top"></a>Index

#### Terms
[Covariance](#covariance)  
[Contravariance](#contravariance)  
[Class](#class)  
[Subclass](#subclass)  
[Subtype](#subtype)  
[Inheritance](#inheritance)  
[Object](#object)  
[Dynamic Polymorphism](#dynamicpolymorphism)  
[Parametric Polymorphism / Generics](#generics)  
[Overloading](#overloading)  
[Stub / Abstract Method](#stub)  
[Abstract Class](#abstractclass)  
[Trait](#trait)  
[Object Identity](#objectidentity)

#### Scala
[foldRight](#foldRight)  
[Map](#map)  

----
## <a name="covariance"></a>Covariance
```scala
class One {
    var name = "Fred"
    def f: Animal
}

class Two extends class One {
    override var name = "Steve"
    def f: Animal
}
```
- Is-a relationship
- Class Two is child class of Class One
- Same public methods and fields

#### [^Return to Index](#top)  
----
## <a name="contravariance"></a>Contravariance
Parameter and output variance

```scala
class One {
    def f(x: Dog): Animal
}

class Two extends class One {
    def f(x: Animal): Dog
}
```

Class Two needs to have a higher or equal parameter with an equal or lower result

#### [^Return to Index](#top)  
----
## <a name="object"></a>Object  

An object is a run-time value, usually an instance of a class. Like other values, such as integers, an object be can stored in variables or data structures (such as arrays). An object can also be passed as an argument to a function, or returned as a result of a function.
An object can have members, which are typically accessed using dot notation, as in someObject.memberName. The two most common kinds of members are fields (also known as attributes) and methods (sometimes called behaviors). Fields are variables inside the object and are accessed as someObject.fieldName. Methods are functions inside the object and are called as someObject.methodName(args).

#### [^Return to Index](#top)  
----
## <a name="class"></a>Class  

A class is a type that describes a family of objects that have the same members, especially fields and methods. An object of that class is called an instance of the class. A new object is created by instantiating the class, either directly or through a factory method.
In most OO languages, (direct) instances of the same class will have the same set of members, with possibly different values in the fields but with exactly the same implementations of the methods.
See also subclass.

#### [^Return to Index](#top)  
----
## <a name="subclass"></a>Subclass
A subclass is a class that is defined by extending an existing class (called the parent class or superclass). The subclass automatically inherits all the members of the parent class, but may add more members, and may override some existing members.
The subclass/superclass relationship is transitive, so if A is a subclass of B, and B is a subclass of C, then A is also a subclass of C.
See also [subtype](#subtype).

#### [^Return to Index](#top)  
----
## <a name="inheritance"></a>Inheritance  

Inheritance is code stealing. A subclass inherits (steals the code for) all the members of the parent class, almost as if that code had been cut-and-pasted from the parent class into the subclass. If there are some members of the parent class that the subclass wants to modify, then the subclass can override those particular definitions.
Many OO languages allow a subclass to inherit from at most one parent class. This is called single inheritance. However, some OO languages allow a subclass to inherit fom more than one parent class. This is called multiple inherintance. Scala supports an unusual form of multiple inheritance, where a subclass can inherit from at most one parentclass, but can inherit from multiple traits.

#### [^Return to Index](#top)  
----
## <a name="Subtype"></a>Subtype  

A type A is a subtype of type B if a value of type A can be used wherever a value of type B is expected. (This is called the Liskov Substitution Principle, named after 2008 Turing Award winner Barbara Liskov.) For example, if we have a variable of type B, then we can assign a value of type A into the variable.
We also describe the subtype relationship as an IS-A relationship, as in “A hedgehog is a mammal” or “A shoofly pie is a dessert.”
In most object-oriented languages (including Scala), a subclass is also a subtype of its superclass. For example, if we have a class Mammal and another class Hedgehog that extends Mammal, than an instance of class Hedgehog can be used where an instance of class Mammal is expected. Put another way, a (direct or indirect) instance of class Hedgehog is also an (indirect) instance of class Mammal.

#### [^Return to Index](#top)  
----
## <a name="dynamicpolymorphism"></a>Dynamic Polymorphism  

Dynamic polymorphism (also known as dynamic dispatch) is the idea that when we call a method of an object, there may be several different implementations of that method, and which method is executed at run-time depends on the class of the object whose method is being called.
Example: Consider a class Animal with a method makeNoise, and three subclasses of Animal that each override the makeNoise method. A Dog says “woof”, a Cat says “meow”, and a Goldfish says “glub”.
Now, if we have a function:
```scala
def talk(animal: Animal): Unit = animal.makeNoise()
```
Then the call animal.makeNoise might say “woof” or “meow” or “glub”, depending on whether animal was a Dog or a Cat or a Goldfish.
See also parametric polymorphism and overloading.

#### [^Return to Index](#top)  
----
## <a name="generics"></a>Parametric Polymorphism / Generics  

Parametric polymorphism (also known as generics) is more of a functional-programming concept that an object-oriented concept, but it does appear in many OO languages, including Scala. The key feature of parametric polymorphism is type parameters. For example, in Scala, we don't just have the type List, but rather the type List[A], where A is a type parameter. Similarly, many functions/methods take type parameters.
Because of these parameters, we can write functions/methods that operate on all kinds of lists. For example, the reverse method works on all kinds of lists, rather than needing to write a different function/method for each type of list.
What really distinguishes parametric polymorphism from dynamic polymorphism that the point of parametric polymorphism is to be able to do essentially the same thing regardless of type, whereas the point of dynamic polymorphism is to be able to do different things for different types.

For example, List(1,2,3).reverse and List("a","b","c").reverse do essentially the same thing, even though one works on a list of integers and the other works on a list of strings.

#### [^Return to Index](#top)  
----
## <a name="overloading"></a>Overloading  

Overloading is when a single class has multiple methods with the same name. When looking at a particular method call, the intended version of the method is determined by comparing the number and types of arguments in the method call to the number and types of arguments in the various method definitions to see which one matches. For example, this class has three methods with the same name:
 ```scala
 class Foo {
    def bar(n: Int) = { ... }
    def bar(s: String) = { ... }
    def bar(n: Int, s: String) = { ... }
  }
```
If we call someFoo.bar(3), the first version is run; if we call someFoo.bar("hello"), the second version is run; and if we call someFoo.bar(4,"a"), the third version is run. (If the number and types of arguments do not match any versions, or if they match more than one version, it is a compile-time error.)
The determination of which version to run is made at compile-time rather than run-time, so overloading is sometimes called static polymorphism. (Note that, in programming languages, the term static refers to compile-time and the term dynamic refers to run-time.)
Contrast this with dynamic polymorphism.

#### [^Return to Index](#top)  
----

## <a name="stub"></a>Stub / Abstract Method

A stub (also known as an abstract method) is method signature (name, parameters, and return type) without an implementation/body. (In contrast, a concrete methodincludes an implementation/body.)
In Scala, a class cannot have any abstract methods; a class with one or more abstract methods must be declared as an abstract class or trait instead.

#### [^Return to Index](#top)  
----
## <a name="abstractclass"></a>Abstract Class 

An abstract class is a class that is intended to serve as a base for subclasses but cannot be directly instantiated. For example, Animal might be an abstract class, with subclasses like Dog or Shark or Lobster. In such a scenario, you could instantiate those subclasses, but could never directly instantiate an Animal.
Importantly, an abstract class can include stubs/abstract methods that are intended to be given implementations in the subclasses.
Compare to trait.

#### [^Return to Index](#top)  
----
## <a name="trait"></a>Trait

A trait is a more powerful version of an abstract class. Like an abstract class, a trait cannot be directly instantiated, but can include stubs/abstract methods.
The biggest different between traits and abstract classes is that traits support multiple inheritance, but abstract classes only support single inheritance. That is, if T1 and T2are traits, and A1 and A2 are abstract classes, then you can define
```scala
   class C1 extends A1 with T1
   class C2 extends A2 with T1 with T2
   class C3 extends T1 with T2
   class C4 extends C1 with T2
```
but you cannot define
```scala
   class C5 extends A1 with A2
   class C6 extends A1 with A2 with T1
   class C7 extends C1 with A2
```
More specifically, a class or abstract class can inherit from at most one class or abstract class, but can inherit from as many traits as desired.

#### [^Return to Index](#top)  
----
## <a name="objectidentity"></a>Object Identity

The phrase object identity refers to the idea that every instantiation of a class produces a distinct object. Even if two instances of the same class have all the same values in their fields, they are still distinct objects (ie, have their own identity).
In Scala, the eq method compares object identity. The equals/== method is looser and may consider distinct objects to be “equal” if they are similar according to some other criteria. For example,
```scala
  val list1 = List(1,2,3)
  val list2 = List(1,2,3)
  list1 eq list2 // returns false, list1 and list2 are NOT the same object
  list1 == list2 // returns true, list1 and list2 have the same contents
  list1 equals list2 // same as ==
```

#### [^Return to Index](#top)  
----

## <a name="foldRight"></a>foldRight

```scala
list.foldRight(0)(_ + _) // sum all elements
```
Folds collapse a collection into one value.  The 0 is the start value.  For the second pair of parentheses, you can also do ((x,y) -> x+y) if it helps you keep track of everything…

#### [^Return to Index](#top)  
----

## <a name="map"></a>Map

```scala
list.map(_ < x) // turn each element into a bool
    .map(if (_) 1 else 0) // turn each bool into 1 or 0
```
Map applies a function against each element in a collection and returns the resulting new collection.

#### [^Return to Index](#top)  
