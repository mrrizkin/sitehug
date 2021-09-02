---
title: 'Memoization: What, Why, and How'
date: 2021-09-02T18:39:19+07:00
description: Memoization is a technique that enhances a function by creating and using a cache to store and retrieve results of that function. Memoization uses the arguments of a function to create a key for the cache.
tags: [technique, programming, improvement]
featured_image: http://www.wikihow.com/images/d/d0/Memorize-Scripts,-Poems,-Verses-Step-17.jpg
categories: Programming
comment: false
---

Recently, I spent an hour with one of my protégés demonstrating some common advanced techniques we use at Webflow. One of the techniques I showed them was memoization. Let's learn what memoization is, why you might use it, and how do we write it from scratch.

# What is Memoization?

Memoization is a technique that enhances a function by creating and using a `cache` to store and retrieve results of that function. Memoization uses the arguments of a function to create a `key` for the `cache`. The first time a memoized function is called with a set of arguments, those arguments are turned into a `key` and the result of the function is stored as the value for that `key` in the `cache`. Then, on subsequent calls of the function with the same arguments, we can retrieve that previously calculated value from the `cache` and return it before we ever do the work of calculating the result. This improves the performance of our function, since hitting the `cache` is a constant time operation (`O(1)` in big O notation).

# How to implement Memoization?

We can use memoization on any pure function and it's not too difficult to implement either. Let's create a higher order function that will allow us to create a memoized version of a pure function.

Typically, we want to use memoization on functions with expensive calculations and we'll talk about why later, but for the sake of writing our memoize function, I'm going to use a very simple pure function.

```javascript
function add(x, y) {
	return x + y
}
```

Can't get much simpler than an `add` function! Since it's a pure function, we can guarantee that the same inputs always lead to the same output. So if we're able to create a cache that will use the function arguments as a key and store the results of the function as a value, we can retrieve that value from the cache knowing it's the same as the result of running the function.

```javascript
function memoize(fn) {
	// We create a cache inside the closure of the `memoize` function
	// This creates a new cache for each function we pass
	// to `memoize`. We'll discuss other cache strategies later
	const cache = {}

	// The goal is to return a function with an identical
	// signature as the one passed in
	return (...args) => {
		// We need to create a key for our cache. A simple way to do this is
		// to join the args with a delimiter that clearly separates arguments
		// This way the arguments (12, 3) don't create the same key as (1, 23)
		const key = args.map(JSON.stringify).join('---')

		if (cache[key] !== undefined) {
			// Just for our example, let's make it clear we returned a value
			// from the cache
			console.log('from cache')
			return cache[key]
		}

		const result = fn(...args)
		cache[key] = result

		return result
	}
}
```

Let's break that down. `memoize` receives a function as an argument. It then creates a cache in closure. This will store the results of our function in memory to be retrieved later.

Next, we return a function that can receive whatever `args` the original function receives. Inside of the function we are returning, we create a `key` for our cache. In this case, I chose to stringify and join the arguments with a delimiter. This delimiter prevents similar arguments from accidentally being the same `key`. Without a delimiter, calling `add(2, 34)` and `add(23, 4)` would result in the `key` `234`. We would end up with a mistaken cache hit for the second call, and even worse, our result would be incorrect.

Next, if there is a defined value at the `cache[key]`, we return it and skip calculating the result. Otherwise, we calculate the `result`, store it in the `cache`, and then return it.

Now, let's create a memoized `add` function and use it.

```javascript
const memoizedAdd = memoize(add)
```

Seriously. Adding memoization to a pure function is that simple.

# Why Use Memoization?

Memoization is a tradeoff exchanging space (memory) for time. The purpose of this tradeoff is to gain a performance benefit by skipping the calculation of the function's result, i.e. save time. Thus, it only makes sense to use memoization where memory is not a concern and the original calculation is both expensive and often called with the same arguments. Our `add` function was a bad example. It's not an expensive calculation at all. Let's create a slightly better example.

I've used this example before in my writing, but a `factorial` function might be a good candidate for memoization. It's recursive, which means that `factorial` will be called with the same argument frequently. In fact, if it's ever been called with a number greater than the current argument, it will simply return the value from the cache, since it's already been calculated before. Let's write the factorial function.

```javascript
const factorial = memoize((n) => {
	if (n === 0) {
		return 1
	}

	return n * factorial(n - 1)
})
```

# Conclusion

Memoization is a trade off of space for time. It's used to cache the result of a function so that the next time it's called with the same arguments, we can just return the answer. We don't need to calculate it again. This technique is useful when we have an expensive calculation that will be called frequently with the same arguments. It's used more often than you might realize and is a useful tool to have in your tool belt.
