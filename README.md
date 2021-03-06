ngraph.random
=============

Operation with seeded random numbers for ngraph.*.

[![build status](https://secure.travis-ci.org/anvaka/ngraph.random.png)](http://travis-ci.org/anvaka/ngraph.random)

Usage
=====
API provides random number generation, and array shuffling. 

Let's start with random number generation:

``` js
// create generator, seeded with 42
var randomGenerator = require('ngraph.random')(42);

 // prints double number from [0..1)
console.log(randomGenerator.nextDouble());

// Get next non-negative random number, less than 100.
console.log(randomGenerator.next(100)); // prints 20, we are seeded
// Note: next() always expect maxValue. If you don't pass it it will return NaN.
// This is done for performance reasons, we don't want to check input arguments
// on each call.
```

Second part of the API is array shuffling:

``` js
var randomAPI = require('ngraph.random');

// create "shuffling" iterator:
var originalArray = [0, 1, 2, 3, 4, 5];
var randomIterator = randomAPI.randomIterator(originalArray);

// iterate over array in random order:
randomIterator.forEach(function(x) {
  console.log(x); // prints originalArray's items in random order
});
// Note: using random iterator does modify original array.
// This is done to save memory.

// If you want to re-shuffle array in-place, you can use:
randomIterator.shuffle();

// Finally if you want to have seeded shuffling you can pass optional seeded 
// random number generator:
var seededGenerator = randomAPI.random(42);
randomAPI.randomIterator(originalArray, seededGenerator); 
```


## distributions

The library supports random number generation that follow Gaussian distribution:

``` js
var generator = require('ngraph.random')(42);

// returns a random number from a gaussian distribution with mean 0 and
// standard deviation 1
generator.gaussian();
```

Install
=======

With [npm](http://npmjs.org) do:

```
npm install ngraph.graph
```

License
=======
BSD 3-clause
