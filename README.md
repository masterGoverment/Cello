Cello
=====

__Cello__ is a _library_ that brings higher level programming to C.

By acting as a _modern_, _powerful_ runtime system Cello makes many things easy 
that were previously impractical or awkward in C such as:

* __Generic Data Structures__
* __Polymorphic Functions__
* __Interfaces / Type Classes__
* __Constructors / Destructors__
* __Optional Garbage Collection__
* __Exceptions__
* __Reflection__

And because Cello works seamlessly alongside standard C you get all the other 
benefits such as great performance, powerful tooling, and extensive 
libraries.

Examples
--------

```c
#include "Cello.h"

int main(int argc, char** argv) {

  /* Stack objects are created using "u" */
  var i0 = u(Int, 5);
  var i1 = u(Int, 3);
  var i2 = u(Int, 4);

  /* Heap objects are created using "new" */
  var items = new(Array, Int, i0, i1, i2);
  
  /* Collections can be looped over */
  foreach (item in items) {
    print("Object %u is of type %u\n",
      item, type_of(item));
  }
  
  /* Heap objects destructed via Garbage Collection */
  return 0;
}
```

```c
#include "Cello.h"

int main(int argc, char** argv) {
  
  /* Shorthand $ can be used for basic types */
  var prices = new(Table, String, Int);
  set(prices, uS("Apple"),  uI(12)); 
  set(prices, uS("Banana"), uI( 6)); 
  set(prices, uS("Pear"),   uI(55)); 

  /* Tables also support iteration */
  foreach (key in prices) {
    var val = get(prices, key);
    print("Price of %u is %u\n", key, val);
  }
  
  return 0;
}
```

Articles
--------

Learning Resources:

* [Installation](http://libcello.org/learn/installation)
* [Cello World](http://libcello.org/learn/cello-world)
* [Quickstart](http://libcello.org/learn/quickstart)
* [Common Queries / Pitfalls](http://libcello.org/learn/queries-and-pitfalls)

Articles about its creation and internal workings:

* [Best Improvements of Cello 2.0](http://libcello.org/learn/best-improvements-of-cello-2.0)
* [A Fat Pointer Library](http://libcello.org/learn/a-fat-pointer-library)
* [Cello vs C++ vs ObjC](http://libcello.org/learn/cello-vs-cpp-vs-objc)
* [Benchmarks](http://libcello.org/learn/benchmarks)
* [Garbage Collection](http://libcello.org/learn/garbage-collection)


More Examples
-------------

```c
#include "Cello.h"

int main(int argc, char** argv) {

  var items = new(Array, Int, 
    uI( 8), uI( 5), uI(20), 
    uI(15), uI(16), uI(98));

  /* Iterate over indices using "range" */
  foreach (i in range(uI(len(items)))) {
    print("Item Range %i is %i\n", i, get(items, i));
  }

  /* Iterate over every other item with "slice" */ 
  foreach (item in slice(items, _, _, uI(2))) {
    print("Item Slice %i\n", item);
  }
  
  return 0;
}
```
    
```c
#include "Cello.h"

/* Define a normal C structure */
struct Point {
  float x, y;
};

/* Make it compatible with Cello */
var Point = Cello(Point);

int main(int argc, char** argv) {
  
  /* Create on Stack or Heap */
  var p0 = u(Point, 0.0, 1.0);
  var p1 = new(Point, u(Point, 0.0, 2.0));
  
  /* It can be shown, compared, hashed, etc...
  **
  ** p0: <'Point' At 0x000000000022FC58>
  ** p1: <'Point' At 0x00000000004C7CC8>
  ** cmp: 1
  ** hash: 2849275892l
  */ 
  print("p0: %u\np1: %u\ncmp: %i\nhash: %ul\n",
    p0, p1, uI(cmp(p0, p1)), uI(hash(p0)));
  
  /* And collected by the GC when out of scope */
  return 0;
}
```

F.A.Q
-----

* __Why does this exist?__

I made Cello as a fun experiment to see what C looks like hacked to its limits. 
As well as being a powerful library and toolkit, it should be interesting to 
those who want to explore what is possible in C.

* __How does it work?__

I recommend reading 
[A Fat Pointer Library](http://libcello.org/learn/a-fat-pointer-library) to get an 
overview of how Cello works. You can also peek at the source code, which I'm 
told is fairly readable, or ask me any questions you like via e-mail.

* __Can it be used in Production?__

It might be better to try Cello out on a hobby project first. Cello does aim to 
be _production ready_, but because it is a hack it has its fair share of 
oddities and pitfalls, and if you are working in a team, or to a deadline, 
there is much better tooling, support and community for languages such as C++.

* __Is anyone using Cello?__

People have experimented with it, but there is no high profile project I know 
of that uses it. Cello is too big and scary a dependency for new C projects if 
they want to be portable and easy to maintain.

* __Can I get involved?__

Yes! That would be great. If you do anything with Cello I'd love to know, you 
can e-mail me at `contact@theorangeduck.com`, or help with the development at 
the [Cello github repo](https://github.com/orangeduck/libCello). Contributions 
are very welcome.

* __Who are you?__

Hello! I'm Daniel Holden. You many know me from a 
[book I wrote](http://www.buildyourownlisp.com/) or my 
[personal website](http://theorangeduck.com/). I also have a rarely updated 
[twitter account](https://twitter.com/anorangeduck).
