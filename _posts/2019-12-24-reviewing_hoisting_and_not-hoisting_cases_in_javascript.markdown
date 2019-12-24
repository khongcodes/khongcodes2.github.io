---
layout: post
title:      "Reviewing hoisting and not-hoisting cases in Javascript"
date:       2019-12-24 21:32:21 +0000
permalink:  reviewing_hoisting_and_not-hoisting_cases_in_javascript
---

Hoisting - when you call a function or variable in a line above the line where it is defined.

#### Var declaration hoists, but not assignment
```
function sayVar() {
  console.log('My name is', theName)
  var theName = 'Jane Doe'
}
```
This returns, when called, "My name is undefined".

The declaration of theName is saved to memory when the Javascript engine does its first pass on the code; but does not yet assign it value. When the Javascript engine does its second run and reaches the line where we call console.log('My name is', theName); theName is declared but not assigned; so it simply evaluates to 'undefined'. This does not throw an error, and so, can go undetected.

#### Let and Const do not hoist
```
function sayConst() {
  console.log('My name is', theName)
  const theName = 'Jane Doe'
}

function sayLet() {
  console.log('My name is', theName)
  let theName = 'Jane Doe'
}
```
Both of the following functions, when called, return ReferenceError: theName is not defined.

As they throw an error, the not-yet-defined nature of theName is more obvious than if we declared the varible using var.


#### Function declarations DO hoist
```
function sayFunction() {
  console.log('My name is', theName())
  function theName() {
    const name = 'Jane Doe'
    return name
	}
}
```
This returns, when called, "My name is Jane Doe." - showing that when we declare to memory using the *function* keyword, the Javascript engine saves a reference to memory even on its first, "compiling" run on the code.

A common design pattern I have seen in code is to define a main program function at the top of a file, or call the functions that comprise a main program at the top, and then define those component functions below; AFTER they have been called. The reason why this can work is because they are declared with the function keyword.

###### An example of this design pattern

```
const mainProgram = function() {
  function1();
	function2();
}

function function1() {
  console.log(1)
}

function function2() {
  console.log(2)
}

// 1
// 2
```


#### Anonymous functions assigned to variables with Let or Const do NOT hoist
```
function sayConstAnonFunction() {
  console.log('My name is', theName)
  const theName = function() {
    theName = 'Jane Doe'
  }
}
```
This returns, when called, ReferenceError: theName is not defined.

Functions declared with the function keyword versus those declared with the const keyword behave the same - except for those declared with the const keyword are not hoisted. I thought this was very interesting - the same design pattern above does not work if its functions are declared with the keyword const.

The design pattern works under specific circumstances, actually - the reason I was interested in testing these different cases is because of a conversation I had with Nancy during my project review.

The design pattern will work if the main program that calls the component functions is only called dependent on an Event Listener firing - an easy one to image is 'click'. By the time you interact with an element in the DOM, certainly Javascript has declared and assigned values to those const variables, right? *This also works if the event you are listening for is DOMContentLoaded.* In the split seconds it takes for the DOM to load, Javascript has prepared into its memory those functions you declared with const.

```
document.addEventListener('DOMContentLoaded', () => {
  function1();
  function2();
});

const function1 = function() {
  console.log(1);
};

const function2 = function() {
  console.log(2);
};

```

What's the takeaway here? I personally lean towards function assignment with the const keyword now - I think it can be just slightly trickier to make sure the load order is correct, but it's worth it. Not to mention, because const is block scoped, entities don't use functions that aren't meant to relate to their own concerns.
