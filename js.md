# JavaScript

## A quick disclaimer

I may have errors in my code. If so, please just correct them, but keep the spirit of the example. If something needs to be added or changed just be sure to get feedback from the other devs.

## var, let, const

Use **let** for times when the object or literal referred to will change. Otherwise use **const**. Just don't use _var_. The scoping is different and even if _you_ understand it, it may cause confusion among our other developers who expect block scoping from other languages.

## Initialize Variables or Test For Nulls

There is a lot of room for null values in the code below. Browsers are very permissive when it comes to failing code, but avoidable null reference errors can clutter up your console and hide actual problems. The code below will not prevent other lines from running, but it is sloppy. It would be better to test the used elements or set defaults.

```javascript
const message = document.querySelector("#message-input");

document.querySelector("#my-button).addEventListener("click" ()=>{
    document.querySelector("#message-window").innerHTML = message;
});
```

The code below supplies a default for message in the case that it's not found, and tests the other elements before operating on them.

```javascript
const message = document.querySelector("#message-input") || "Nothing to see here...";
const window = document.querySelector("#message-window");
const button = document.querySelector("#my-button);

if( button && window){
    button.addEventListener("click" ()=>{
        window.innerHTML = message;
    });
}
```

## Line Endings, For Loops, and Turneries

Optional semicolons should always be used. All for loops should have braces and be on multiple lines. Turneries are fine, but should not be nested.

## Use Classes Instead of .style

The best way of adding a style to an element is by putting the style in a css rule and adding/removing it with javascript. There are a lot of different properties and they are not always the same as the css rules. Additionally, you may want to reuse styles across multiple elements.

```javascript
const window = document.querySelector("#message-window");
window.style.color = "red";

```

better is the following:

```javascript
const window = document.querySelector("#message-window");
window.style.classList.add("warning");
```

Now, you can use the warning class wherever it's needed and if you want to do something like add a border, it's easy to add it in the css rule.

## Avoid Globals

wrap code in an IIFE or similar structure to avoid global variables. The code below creates 3 very generic sounding global variables which could conflict or cause bugs.

```javascript
const message = document.querySelector("#message-input") || "hello world";
const window = document.querySelector("#message-window");
const button = document.querySelector("#my-button);

if( button && window){
    button.addEventListener("click" ()=>{
        window.innerHTML = message;
    });
}
```

You could put the code in a function and call it immediately like so:

```javascript
function init(){
    const message = document.querySelector("#message-input") || "hello world";
    const window = document.querySelector("#message-window");
    const button = document.querySelector("#my-button);
    if( button && window){
        button.addEventListener("click" ()=>{
            window.innerHTML = message;
        });
    }
};

init();
```

however, if you are only ever running the function once, you can use an IIFE. An immediately invoked function expression is just a function that executes right away. You declare it as shown below. The variables exist inside the variable you declared in the global scope.

```javascript
const myNameSpace = function(){
    const message = document.querySelector("#message-input") || "hello world";
    const window = document.querySelector("#message-window");
    const button = document.querySelector("#my-button);
    if( button && window){
        button.addEventListener("click" ()=>{
            window.innerHTML = message;
        });
    }
    return{
        //return needed variables here.
    }
}();
```

Then, you can call the variables with **nameSpace.variableName**. If you don't need anything, you can simplify this a bit by eliminating the declaration and return statement, and wrap the function in parenthesis.

```javascript
(function(){
    const message = document.querySelector("#message-input") || "hello world";
    const window = document.querySelector("#message-window");
    const button = document.querySelector("#my-button);
    if( button && window){
        button.addEventListener("click" ()=>{
            window.innerHTML = message;
        });
    }
})();
```

## Naming Conventions

### Variables

Use camel case for variable names.

```javascript
// bad
const d = 'Scooby-Doo';

// bad
const name = 'Scooby-Doo';

// good
const dogName = 'Scooby-Doo';
```

### Booleans

When it comes to Boolean variables, we should use is or has as prefixes. For example, if you need a Boolean variable to check if a dog has an owner, you should use hasOwner as the variable name.

```javascript
// bad
const barking = false;

// good
const isBarking = false;

/******/

// bad
const ideal = true;

// good
const areIdeal = true;

/******/

// bad
const owner = true;

// good
const hasOwner = true;
```

### Functions and class methods

Use camel case for function and method names and descriptive nouns or verbs as prefixes. For example, if we declare a function to retrieve a name, the function name should be getName.

```javascript
// bad
function name(dogName, ownerName) { 
  return '${dogName} ${ownerName}';
}

// good
function getName(dogName, ownerName) { 
  return '${dogName} ${ownerName}';
}
```

### Classes

Use pascal case for class names.

```javascript
class DogCartoon { 
  constructor(dogName, ownerName) { 
    this.dogName = dogName; 
    this.ownerName = ownerName; 
  }
}

var cartoon = new DogCartoon('Scooby-Doo', 'Shaggy');
```

## Prefer === Over ==

Unless you are intentionally using loose equality for type coercion, use strict equality.
