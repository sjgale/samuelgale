---
layout: post
title:  "Common JS Array Methods"
date:   2017-06-02 8:15:13 -0600
categories: jekyll update
---

### Validating:
{% highlight javascript %}
Array.isArray(maybeArray); // returns boolean
{% endhighlight %}

### Creating from string:
{% highlight javascript %}
let newArray = stringVariable.split(delimeter)
{% endhighlight %}

### Adding and removing elements:
{% highlight javascript %}
theArray.push(newValue); // add newValue to the end of theArray
theArray.unshift(newValue); // add newValue to the beginning of theArray
theArray.pop(); // removes the final element from theArray
let lastElem = theArray.pop(); // removes the theArray's last element and stores it as lastElem
theArray.shift(); // removes the first element of theArray
let firstElem = theArray.shift(); // removes theArray's first elements and stores it as firstElem
{% endhighlight %}

### Creating from an Array from another array:
Assigning array as value actually just assigns a referernce. To create a new array with identical values, you must iterate through each element of the array assigning it to the new array.
Like:
{% highlight javascript %}
let newArray = oldArray.map(function (currentElement) {
	return currentElement;
}
{% endhighlight %}

Slice():
{% highlight javascript %}
let newArray = oldArray.slice(1,5)
{% endhighlight %}
Grab elements from oldArray, starting at the first element, until we reach the fifth element. The fifth element is not included. If either parameter is negative, it will count backwards from the end, to determine the position. The second, ending parameter is optional. The original array is untouched.

Filter:
{% highlight javascript %}
let newArray = oldArray.filter(function (currentVariable) {
	if (typeof currentVariable !== "number")
		return false;
	return currentVariable % 2 === 0;
})
{% endhighlight %}
Iterate over each element from oldArray. If the value returned by the callback function is true, store the currentVariable into newArray. In this case, an array of the even numbers in oldArray will be set to the value of newArray.


### Ordering methods:
{% highlight javascript %}
myArray.reverse() // reverse the contents of the array
myArray.sort() // Alphabetically sort the elements in the array
{% endhighlight %}

Custom Sort:
{% highlight javascript %}
myArray.sort(function(a, b){
	return a - b;
});
{% endhighlight %}
If the callback function returns 0, parameter is equal to b. If the result is greater than 0, a is assumed greater than b. If less than 0, b is assumed greater than a.

### Iterating Methods:
ForEach:
{% highlight javascript %}
myArray.forEach(function (element, index, array) {
	console.log(`${index}: ${element}\n`);
});
{% endhighlight %}

Every:
{% highlight javascript %}
myArray.every(function (currentItem) {
	return typeof currentItem === "number" && currentItem > 50;
});
{% endhighlight %}
`.every()` returns a boolean value. True only if every element returns true from the callback function. In this case, every() will return true only if myArray has only number elements greater than 50.

Some:
{% highlight javascript %}
myArray.some(function (currentItem) {
	return typeof currentItem === "number" && currentItem > 50;
});
{% endhighlight %}
Like `.every()`, `.some()` also returns a boolean value. True if any of the elements return true from the callback function. In this case, every() will return if any element in myArray is a number greater than 50.


### Reducing:
{% highlight javascript %}
/* reduce an array to the total of its elements */
let sum = [10, 20, 10, 30].reduce(
	(runningTotal, current) => runningTotal + current,
	0
); // Sum is 70

/* reduce an array to the max value */
let max = [10, 20, 10, 30].reduce(
	(runningMax, current) => {
		return runningMax > current ? runningMax : current
	},
	0
); // max is 30
{% endhighlight %}
Applies a callback, which accepts an accumulator, and against each element in an array