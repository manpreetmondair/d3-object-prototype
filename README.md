# *Difference between class ans Prototypal inheritance*
JavaScript's object system is based on Prototype Inheritance, not on classes. But we need to understand the concept of Prototype and classes.
##### Class
A Class is a description of object to be created
### Class Inheritance
Classes inherit from classes and create subclass relationships: hierarchical class taxonomies.In JavaScript, class inheritance is implemented on top of prototypal inheritance, but that does not mean that it does the same thing.JavaScript’s class inheritance uses the prototype chain to wire the child `Constructor.prototype` to the parent `Constructor.prototype` for delegation. Usually, the `super()` constructor is also called. Those steps form single-ancestor parent/child hierarchies and create the tightest coupling available in OO design.
### Side-effect of Class Inheritance
*The tight coupling problem (class inheritance is the tightest coupling available in oo design), which leads to the next one…1
*agile base class problem2
*Inflexible hierarchy problem (eventually, all evolving hierarchies are wrong for new uses)3
*The duplication by necessity problem (due to inflexible hierarchies, new use cases are often shoe-horned in by duplicating, rather than adapting existing code)4
*The Gorilla/banana problem (What you wanted was a banana, but what you got was a gorilla holding the banana, and the entire jungle)5
### Prototypal Inheritance: A prototype is a working object instance. Objects inherit directly from other objects.
there are three different kinds of prototypal OO.
Concatenative inheritance: The process of inheriting features directly from one object to another by copying the source objects properties
Prototype delegation: In JavaScript, an object may have a link to a prototype for delegation. If a property is not found on the object, the lookup is delegated to the delegate prototype, which may have a link to its own delegate prototype, and so on up the chain until you arrive at `Object.prototype`, which is the root delegate.
Functional inheritance: In JavaScript, any function can create an object. When that function is not a constructor (or `class`), it’s called a factory function. Functional inheritance works by producing an object from a factory, and extending the produced object by assigning properties to it directly (using concatenative inheritance).