## Class Theory
Here will explore 'Class Theory' before moving on to OOJS.

## Objects
Object Oriented Programming is a design pattern created to give our code reason, organization and extensibility (code re-use). To accomplish this architecture, we compare our 'inanimate' code, to 'animate' (real-world) objects. For example, let's compare a program that might have dogs in it, with a real dog. We can use our parts of speech to describe this dog.

* A _dog_ is a *noun*
* A dog might have a _breed_ of _golden retriever_. This is an *adjective*.
* A dog might be able to _bark_. This is a *verb*.

Now, if we think about this in terms of humble JavaScript, we might say the following:

* A *noun* in JS, is an *object* `{}`
* An *adjective* in JS is that *object's* properties `{ breed: 'golden_retriever' }`
* A *verb* in JS is that *object's* methods `{ bark: function () { } }`

## Factories and Classes
Now, if we wanted to create many Golden Retrievers, we might build a Golden Retriever factory (if that was possible - with programming it is). For this we would need a master Golden Retriever blueprint to know how to build all other Golden Retrievers.

```JavaScript
class GoldenRetriever (name) {
  breed: 'Golden Retriever',
  fur_color: 'gold',
  bark: function () {
    alert('woof!')
  }
  name: name
}
```

Above is a little bit of pusedo-code (meaning, it won't work), but it get's the point across. The things that will be consistently true for a 'Golden Retriever' have been hard-coded, but the things that will be unique to each new Golden Retriever, will be dynamic (their name). So now, if we wanted a new Golden Retriever we might write something like this:

```JavaScript
var ralph = new GoldenRetriever('Ralph');
```

And we would now expect that `ralph` is a Golden Retriever with all the attritubes that a Golden Retriever should have, but with the `name` attribute set to `Ralph`.

To put some more OO vocabulary to this, we would say that `GoldenRetriever` is our *class* (the abstract concept of a real-world Golden Retriever) and that `ralph` is an *instance* of the `GoldenRetriever` class.

## Inheritance
That's all good an well, but Object Oriented Programming suggests not only that new objects can be created from a blue-print (class) but that we can also have *sub-classes* (or child classes) that *inherit* from *super-classes* (or parent classes). In our dog example, what if we wanted to also build many Black Labs? We might then want to create a more generic `Dog` super-class, and then have our `GoldenRetriever` and `BlackLap` sub-classes inherit from them.

```JavaScript
class Dog (name) {
  bark: function () {
    alert('woof!')
  },

  name: name
}
```

Notice that we've removed the `breed` and `fur-color` attributes. These will be given by our sub-classes. They may look as follows:

```JavaScript
class GoldenRetriever extends Dog {
  breed: 'Golden Retriever',
  fur_color: 'gold',
}
```

```JavaScript
class BlackLab extends Dog {
  breed: 'Black Lab',
  fur_color: 'black',
}
```

Neither the `BlackLab` or `GoldenRetriever` sub-classes needed the `bark` method, because they both inherited it from ther `Dog` super-class.

## Object Oriented JavaScript
Is JavaScript Object Oriented? Yes of course, and no not really (we'll explain in a moment). In JavaScript, many things revolve around the humble object. In fact, functions, arrays and objects (of course), are objects! Functions are just objects that have this special ability to be 'invoked'. Check this out:

```JavaScript
var func = function () {};

func.a = 10;

console.log(func.a) // an object for sure!
```

Functions can also be used to create new objects:

```JavaScript
var func2 = new func();

console.log(func2) // func {}
```

When we use the `new` keyword, any old regular function will now be invoked and a new object will be created based on that function. A more conventional way that you'll see is this:

```JavaScript
var Dog = function (name) {
  this.name = name;
};

var ralph = new Dog('Ralph');
```

By convention in JavaScript, developers use a capital letter when defining "constructor functions" (functions that will later be called with the `new` keyword). Other than that, there is literally no difference between these functions and normal ones. For example, `Dog` is obviously not just for creating dogs, but is a normal function:

```JavaScript
var Dog = function (name) {
  alert('Woof!');
  this.name = name;
};

var ralph = new Dog('Ralph');
```

So again, does JavaScript have classes? No, it certainly does not - just functions and objects. Other than that, JS only has a hacked convention that developer have used to try and mimic classes.

Let's take a quick glance at it now. Here, we'll create our super and sub-classes with real JavaScript:

```JavaScript
var Dog = function (name) {
  this.bark = function () {
    alert(this.name)
  };

  this.name = name
};

var GoldenRetriever = function (name) {
  Dog.call(this, name);

  this.breed = 'Golden Retriever';
  this.fur_color = 'gold';
}

var BlackLab = function (name) {
  Dog.call(this, name);

  this.breed = 'Black Lab';
  this.fur_color = 'black';
};

var ralph = new BlackLab('Ralph');
var jake = new GoldenRetriever('Jake');
```

Great! We have classes and sub-classes, but as you can see, it 'inherit' from one class to another, we had use this hack `Dog.call(this, name)`. More on that in the lesson.

However, we still have a problem
