---
title: "JavaScript String Interpolation and Computed Property Names: ES6 to the Rescue!"
date: "2019-05-30"
---

I've recently been diving deep into JavaScript after stumbling upon the ["You Don't Know JS" series by Kyle Simpson](https://github.com/getify/You-Dont-Know-JS)... It's such a great resource and I loved it so much that I bought the whole series! I'd highly recommend it to anyone interested in unraveling the mysteries of JavaScript.

I had no idea that I didn't _truly_ understand JavaScript! I've been writing a lot of it since 2011, but the thing is... JavaScript has changed so much over the last 10-15 years and if you aren't keeping up then you're falling behind! I thought jQuery was all I needed, and boy was I wrong! :oops: 😂

Now that JSON and RESTful APIs are such a driving force in web development, I've grown to appreciate JavaScript/MongoDB significantly more than PHP/mySQL. Sure, JavaScript has some odd quirks (automatic type coercion, unusual inheritance, ["Run-to-completion"](https://developer.mozilla.org/en-US/docs/Web/JavaScript/EventLoop#Run-to-completion)) but JavaScript has changed a lot since we were using it to add snowflakes and trailing mouse cursors to our websites in the early 2000's.

I'm still getting acquainted with all the changes from ES6 and beyond, but "new" JavaScript has some really intuitive features that make writing JavaScript a lot less painful than before.

In this post, I want to talk about Template literals and using computed property names in object literals. Both are features introduced in [ECMAScript 2015](https://en.wikipedia.org/wiki/ECMAScript#6th_Edition_-_ECMAScript_2015), also referred to as "ES6".

## Template literals

ES6 provides a new way to declare string literals called Template literals. Template literals are enclosed by backticks instead of double or single quotes and can contain placeholders that are indicated by using the dollar sign and curly braces `${expression}`

Placeholders can contain variable identifiers and expressions! WOW! 🙌 This allows us to perform string and expression interpolation in a way that's much easier to read and write.

Template literals can also be multi-line strings, but keep in mind they are not supported in Internet Explorer, but it works in Microsoft's Edge browser. For more information on compatibility, check [caniuse.com](https://caniuse.com/#search=template%20literals)

If you need to include a backtick in your template literal, you must add a backslash (`\`) before the backtick to escape it... Otherwise, an error will be thrown in the console.

For more information, see [Template literals](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals)...

## Computed Property Names

Since ES5, we've been able to use string and expression interpolation to create computed property names, however, previously this could not be done inside an object literal.

Before ES6, you would have had to declare the object first, then create a computed property using bracket notation along with an assignment operator...

`let obj = {}`  
`obj['a'+'b'] = 42`

Now, thanks to ES6's enhanced object literals, we can use Template literals as property names when defining an object literal! No assignment operator is needed! Now the assignment operator is not needed, allowing us to use computed property names while writing less code!

Underscores are typically used to denote "hidden" properties, but since JavaScript doesn't actually have a `public` or `private` keyword doing so is virtually pointless. All JavaScript objects are mutable, even Object prototypes like, `toString()` but that's a topic that I'll have to cover in another post.

We can also create computed property names with Strings. For example, take a look at the following code:

`obj['prefix'+'_'+'suffix']  // obj.prefix_suffix`

However, template literals are usually much easier to read than concatenated strings and variables. It is very important to write code that is easy to read, this will make it easier to maintain in the future for yourself and others!

In order to truly appreciate this syntactic sugar, let's take a look at what this code looks like when it's transpiled by [Babel](https://babeljs.io/repl) to work in older browsers that do not yet support the latest ECMAScript.

**ES5 and Beyond**

![](../../images/blog/image-2.png)

  

**"old" JavaScript**

![](blog/images/image-3.png)

The transpiled code does the exact same thing, but as you can see it takes a lot more code. Isn't that awesome?!

## Property Accessors

Also, don't forget! We can access object properties using _dot notation_ or _bracket notation_.

However, if a property name is not alphanumeric, then dot notation will not work. In that case, bracket notation must be used. For example, take a look at the following code...

`obj['not-alphanumeric'] // works `

`obj.not-alphanumeric // Uncaught ReferenceError: alphanumeric is not defined`

For more details, see [Property Accessors](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Property_Accessors).

That's it for now, but I'll be back soon. Happy coding! ❤
