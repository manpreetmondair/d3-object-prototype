### *Difference Between Class and Prototypal Inheritance*
JavaScript's object system is based on Prototype Inheritance, not on classes. But we need to understand the concept of Prototype and classes.
###### Class
A Class is a description of object to be created
##### Class Inheritance
Classes inherit from classes and create subclass relationships: hierarchical class taxonomies.In JavaScript, class inheritance is implemented on top of prototypal inheritance, but that does not mean that it does the same thing.JavaScript’s class inheritance uses the prototype chain to wire the child `Constructor.prototype` to the parent `Constructor.prototype` for delegation. Usually, the `super()` constructor is also called. Those steps form single-ancestor parent/child hierarchies and create the tightest coupling available in OO design.
This is the example of Class inheritance
``` JavaScript
class GuitarAmp {
  constructor ({ cabinet = 'spruce', distortion = '1', volume = '0' } = {}) {
    Object.assign(this, {
      cabinet, distortion, volume
    });
  }
}

class BassAmp extends GuitarAmp {
  constructor (options = {}) {
    super(options);
    this.lowCut = options.lowCut;
  }
}

class ChannelStrip extends BassAmp {
  constructor (options = {}) {
    super(options);
    this.inputLevel = options.inputLevel;
  }
}

const myAmp = new BassAmp();
const myStrip = new ChannelStrip();
```
###### Side-effect of Class Inheritance
* The tight coupling problem (class inheritance is the tightest coupling available in oo design), which leads to the next one…
* agile base class problem
* Inflexible hierarchy problem (eventually, all evolving hierarchies are wrong for new uses)
* The duplication by necessity problem (due to inflexible hierarchies, new use cases are often shoe-horned in by duplicating, rather than adapting existing code)
* The Gorilla/banana problem (What you wanted was a banana, but what you got was a gorilla holding the banana, and the entire jungle)

####  Prototypal Inheritance: 
A prototype is a working object instance. Objects inherit directly from other objects.
 there are three different kinds of prototypal OO. 

###### Concatenative inheritance: 
The process of inheriting features directly from one object to another by copying the source objects properties

###### Prototype delegation: 
In JavaScript, an object may have a link to a prototype for delegation. If a property is not found on the object, the lookup is delegated to the delegate prototype, which may have a link to its own delegate prototype, and so on up the chain until you arrive at `Object.prototype`, which is the root delegate.

###### Functional inheritance: 
In JavaScript, any function can create an object. When that function is not a constructor (or `class`), it’s called a factory function. Functional inheritance works by producing an object from a factory, and extending the produced object by assigning properties to it directly (using concatenative inheritance).

Here is the example of Prototypical Inheritance
``` JavaScript
const distortion = { distortion: 1 };
const volume = { volume: 1 };
const cabinet = { cabinet: 'maple' };
const lowCut = { lowCut: 1 };
const inputLevel = { inputLevel: 1 };

const GuitarAmp = (options) => {
  return Object.assign({}, distortion, volume, cabinet, options);
};

const BassAmp = (options) => {
  return Object.assign({}, lowCut, volume, cabinet, options);
};

const ChannelStrip = (options) => {
  return Object.assign({}, inputLevel, lowCut, volume, options);
};

const myAmp = BassAmp({
  lowCut: 2,
  volume: 2,
  cabinet: 'vintage'
});

const myStrip = ChannelStrip({
  inputLevel: 2,
  lowCut: 2,
  volume: 2
}); ```



Here is the codepen link:
http://codepen.io/manpreetmondair/pen/evOKWZ?editors=001