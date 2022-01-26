---
title: Generating Random Number Distributions
layout: post
keywords: random, C++
katex: true
---

This document describes Random, a C++ class for generating pseudorandom number distributions.
This class gives the programmer the ability to generate pseudorandom number distributions as if they were native types in the C++ language. The class is self-contained in a single header file
(Random.h) so that a C++ programmer only has to include the header file in order to make use of the code.
Examples and a reference sheet are provided to serve as guidance in using the code.

## Summary

This document describes Random, a C++ class for generating random number distributions,
suitable for performing Monte Carlo simulations. This class gives the
programmer the ability to generate random number distributions as if they were
native types in the C++ language.
There are two broad aspects to this class:

- **Random Number Generator**<br />
The class provides a number of generators to choose from. These are the
engines for generating the pseudorandom numbers. Each engine will deliver
32-bit and 64-bit integers as well as floating point numbers between 0 and 1.
Many of the generators also have jump capabilities.
 
- **Random Number Distribution**<br />
Independently of whichever generator is selected, the class provides many different
distributions to choose from. The class currently contains 27 continuous
distributions, 9 discrete distributions, distributions based on empirical data,
and bivariate distributions, as well as distributions based on number theory.
Moreover, it allows the user–programmer to specify an arbitrary function
or procedure to use for generating distributions that are not already in the
collection. It is also shown that it is easy to extend the collection to include
new distributions.

To generate 1000 normally-distributed random numbers (with default mean 0 and
standard deviation 1) using the jkiss generator, we would write the following code:

{% highlight cpp %}
#include "Random.h"
#include <iostream>
#include <cstdlib>

int main( void ) {

   // create a new generator using jkiss as the engine
   Generator<uint32_t> *rng = new JKISS::jkiss;
   
   // create a distribution object and initialize it to use this generator
   dist::Distribution<uint32_t> rnd( rng );
   
   // output 1000 normally-distributed pseudorandom numbers
   for ( int i = 0; i < 1000; i++ )
      std::cout << rnd.normal() << std::endl; 

   return 0;
}
{% endhighlight %}

No libraries are required and there is nothing to build; one merely needs to include
the header file in order to make use of the class.

**Links**

- [Random document]({% link /assets/random.pdf %})
- [Random repository](https://github.com/rsaucier/Random)
