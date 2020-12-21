---
layout: post
title: Learn Frontend in 2021
tags:
  - react
  - typescript
---

Frontend engineer changes every year. Different technologies, libraries and techniques.
This series is everything you need to know to get up to scratch with Frontend Engineering in 2021.

In this part, we will go over

- [JavaScript](#modern-arrays-strings-objects-and-functions)
- [CSS](#css)


## Modern Arrays, Strings, Objects and Functions

Quickly to recap some common advanced techniques using JavaScript and Typescript types.


### Variables

Don't use `var` use `let` or `const`.

```tsx
harry = 27

console.log(harry)

var harry = 31

console.log(harry)
```

What is the output?

```
> 27
> 31
```

Why? Because when you use var, the variable declaration is hoisted. The above is the same as this:

```tsx
var harry = 27

console.log(harry)

harry = 31

console.log(harry)
```

Use let and const to avoid this.

```tsx
harry = 27 // ERROR harry is used before it's declared

console.log(harry)

let harry = 31

console.log(harry)
```


### Arrays

```tsx
// Arrays can have anything inside
const things = [1,2,3,4,'harry',1.2,() => 1, null, undefined, {}]
```

But to let TypeScript help you out, you should make sure to type the array.

![Array types]({{site.baseurl}}/img/fe-2021-1.png)

```tsx
const things: (number | string)[] = [1,2,3,'harry']
```

With arrays you can easily access elements using Array Destructure Assignment.

```tsx
const [first, ...rest] = [1,2,3,4,5]
console.log(first) // 1
console.log(rest) // [2,3,4,5]
```

You can also do

```tsx
const [first, second, third] = [1,2,3,4,5]
console.log(first) // 1
console.log(second) // 2
console.log(third) // 3
```


### Strings

Strings are quite straightforward and have loads of classic functions on the type.

```tsx
"1".padStart(2, '0') // "01"
```

Simply write a string and press dot to see a list of functions.

![Array types]({{site.baseurl}}/img/fe-2021-2.png)

```tsx
const currency = "£123"
const sign = currency.substring(0, 1) // "£"
```

But always be on the lookout for translation issues, e.g. if the currency value came from a translated value, then
you can't always be sure that the currency symbol will be on the left. So you have no way of knowing some details
about translated strings.

```tsx
const currency = "123£"
const sign = currency.substring(0, 1) // "1" // not what you initially expect
```

Finally you should be careful with string interpolation.

All of these are equivalent, but you will have a prettier / auto formatter to choose one
of these, so don't worry about this too much.

```tsx
'harry'
"harry"
`harry`
```

But for interpolating things you should always opt for:

```tsx
const age = 27
const id = '1000'

`${age}{id}` // 271000
```

Because using + sign coerces the string to a number (if it can).

```tsx
const age = 27
const id = '1000'
age + id // 1027
```

### Objects

Similar to arrays you can destructure objects too!

```tsx
const props = { isStarred: true, disabled: false }

const { isStarred } = props

console.log(isStarred) // true
```



On another note, mutating state is generally considered a bad idea, but for JavaScript it is seen as a bad practice, and will
likely be flagged in code reviews as bad code.

```tsx
const data = { age: 27 }

// ...

data.age = 35

// ...

console.log(data.age) // we have to find all occurrences of data to know what this value is
```

It is very typical to see the spread operator when modifying objects.

e.g.

```tsx
const data = { age: 27, name: 'harry'}

const newData = { ...data, age: 35 }

console.log(newData.age) // 35
```

This seems almost pointless in this example, but it leads us onto a point about functions...

### Functions

My first programming language was VB.NET. When you defined a function with arguments you had to state
if you wanted to copy the input value ByVal or use a reference to it ByRef.
In JavaScript everything (except primitives, e.g. 'harry' or 123) is passed ByRef.

```tsx
const transform = (d) => {
  d.age = 30
}


const data = { age: 27, name: 'harry' }
transform(data);

console.log(data.age); // ???
```

The answer is 30, as we mutated the data OBJECT when we passed it to transform.
To avoid this, I always recommend copying the input object and returning a new copy.
e.g.

```tsx
const transform = (d) => {
  const newData = { ...d } // shallow copies
  newData.age = 30
  return newData
}


const data = { age: 27, name: 'harry' }
const newData = transform(data);

console.log(newData.age); // easy to follow, 30
```

Or even better, use the spread operator with the averring of keys

```tsx
const transform = (d) => {
  return { ...d, age: 30 }
}
```

Which can be condensed to

```tsx
// Note: js gets confused here because we don't know we are returning an object or starting a function
const transform = (d) => { ...d, age: 30 }

// So wrap in brackets like this, to return an object
const transform = (d) => ({ ...d, age: 30 })
```

You will also see weird function expressions like this

```tsx
(() => {
  console.log('I am an IIFE, immediately invoked function expression')
})()
```
Try to avoid these as you can just write them simply like

```tsx
const func = () => {
  console.log('I am no longer an IIFE, immediately invoked function expression')
}

(func)()
```

or

```tsx
const func = () => {
  console.log('I am no longer an IIFE, immediately invoked function expression')
}

func()
```


## CSS

Everyone has seen the [family guy css gif](https://giphy.com/gifs/frustrated-annoyed-programming-yYSSBtDgbbRzq).


### SASS

Use [sass](https://sass-lang.com/). It's great and is better than CSS.
The main benefit is that you can have nested selectors, e.g.

```scss
.container {
  padding: var(--spacing-multiplier);
  
  h3 { 
    color: red;
  }
}
```

This transpiles down to 

```scss
.container {
  padding: var(--spacing-multiplier);
}

.container h3 { 
  color: red;
}
```

### CSS variables

Projects often define CSS variables, such as a spacing multiple.
You can access these using the var key word.

```scss
.container {
  padding: calc(2 * var(--spacing-multiplier));
}
```

### CSS Modules

This is a great method to write CSS. As they prevent leaky CSS.

e.g.

```
Panel.tsx
Panel.module.scss
```

```scss
.container {
  padding: calc(2 * var(--spacing-multiplier));
}

// This will effect all h3's on the page that the Panel is included in
h3 {
  color: red;  
}
```

When you nest and have CSS modules you limit the scope, e.g.

```scss
.container {
  padding: calc(2 * var(--spacing-multiplier));


  // This will effect all h3's on the page that are under the CSS module
  // .container
  h3 {
    color: red;  
  }
}
```


```tsx
// Panel.tsx
import React from 'react';
import styles from './Panel.module.scss';

export const Panel = ({ title }: { title: string }) => {
  return (
    <div className={styles.container}>
      <h3>{title}</h3>
    </div>
  )
}
```

If we didn't use CSS modules here, we could also have another component with a class called 'container' and a h3
inside. That CSS we wrote in Panel.module.scss would effect that too! And 'leak' into our other components.
CSS modules turns all class names into unique strings to prevent this. That way when you use styles.container,
it will always be unique.

(in dev mode, localhost you will see a helpful name like the path to your component, but in production it will be random).


### Interacting with libraries

To interact with libraries that haven't been 'css moduled', you need to use the global keyword to target those selectors.
e.g.

```tsx
// Panel.tsx
import React from 'react';
import { H3 } from 'a-framework-library';
import styles from './Panel.module.scss';

export const Panel = ({ title }: { title: string }) => {
  return (
    <div className={styles.container}>
      <H3>{title}</H3>
    </div>
  )
}
```

```scss
.container {
  padding: calc(2 * var(--spacing-multiplier));

  // the H3 component applies it's own non-css module'd class names
  // here we are selecting it, and making it more targeted and more specific
  h3:global(.a-framework-h3) {
    color: black;
  }
  
  h3 {
    color: red;
  }
}
```

### Specificty 

The more targeted a selector the more specific it is and the higher specificity it has.
The highest specificity results in the selector that gets chosen.

```scss
.container {
  padding: calc(2 * var(--spacing-multiplier));
  
  // specificity 1
  h3 {
    color: black;
  }

  // specificity 1
  h3 {
    color: red;
  }
}

```

h3 is red, because if the specificity is tied, the last one is applied.

```scss
.container {
  padding: calc(2 * var(--spacing-multiplier));
  
  // specificity 2
  h3:global(.a-framework-h3) {
    color: black;
  }

  // specificity 1
  h3 {
    color: red;
  }
}

```

h3 is black, because of the higher specificity.


## Summary

We have covered SASS/CSS and modern JavaScript Arrays, Strings, Objects and Functions.

Frontend is a broad topic to cover. This is part one of a series in modern frontend development.
Stay tuned for part 2.


### More reading

- [Learn SASS](https://sass-lang.com/guide)
- [JavaScript modern guide](https://javascript.info/variables)
