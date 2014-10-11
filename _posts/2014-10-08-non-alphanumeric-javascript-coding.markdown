---
layout: post
title:  "Non Alphanumeric Javascript Coding - Quick Reference"
date:   2014-10-08 00:27:33
categories: coding
permalink: post/non-alphanumeric-javascript-coding/
---

This is a quick reference to generate a fully non-alphanumeric javascript code! 

## ~1 Base knowledge

### Generating numbers

  Number        | Non-Alphanumeric      | Return string by */+[]                   | Other way through increment
  ------------- | --------------------- | ---------------------------------------- | ---------------------------------
  0             | `+[]`                 |  `[]*[]`                                 |
  1             | `+!+[]`               | `++[[]][+[]]`                            |
  2             | `!+[]+!+[]`           | `++[++[[]][+[]]][+[]]`                   | `++[!![]][+[]]`
  3             | `!+[]+!+[]+!+[]`      | `++[++[++[[]][+[]]][+[]]][+[]]`          | `++[++[!![]][+[]]][+[]]`
  4             | `!+[]+!+[]+!+[]+!+[]` | `++[++[++[++[[]][+[]]][+[]]][+[]]][+[]]` | `++[++[++[!![]][+[]]][+[]]][+[]]`

### Generate statements

  Statement          | Non-Alphanumeric  | Return string through +[]  | Other way through +''
  ------------------ | ----------------- | -------------------------- | ---------------------------------
  [object, Object]   | `{}`              | `{}+[]`                    | `{}+''`
  false              | `[![]]`           | `[![]]+[]`                 | `[![]]+''`
  true               | `[!![]]`          | `[!![]]+[]`                | `[!![]]+''`
  NaN                | `[![]]`           | `[![]]+[]`                 | `[![]]+''`
  undefined          | `[]['']`          | `[]['']+[]`                | `[]['']+''`

## ~2 Generate a simple non-alphanumeric string

### How to generate a simple "alert" string

  Char index         | Return char   | Non-Alphanumeric                    | Description
  ------------------ | ------------- | ----------------------------------- | ---------------------------------
  "false"[1]         | 'a'           | `([![]]+[])  [+!+[]]`               | JS statement char of "false" array index 1
  "false"[2]         | 'l'           | `([![]]+[])  [!+[]+!+[]]`           | JS statement char of "false" array index 2
  "false"[4]         | 'e'           | `([![]]+[])  [!+[]+!+[]+!+[]+!+[]]` | JS statement char of "false" array index 4
  "true"[1]          | 'r'           | `([![]]+[])  [!+[]+!+[]+!+[]+!+[]]` | JS statement char of "true" array index 1
  "true"[0]          | 't'           | `([!![]]+[]) [[]*[]]`               | JS statement char of "true" array index 0

**Concatenate and store non-alphanumeric "alert" to variable _**

{% highlight js %}
_ = ([![]]+[]) [+!+[]] + ([![]]+[]) [!+[]+!+[]] + ([![]]+[]) [!+[]+!+[]+!+[]+!+[]] + ([!![]]+[]) [++[[]][+[]]] + ([!![]]+[]) [[]*[]];
{% endhighlight %}

<!--r34dm0r3-->

## ~3 Types of execution methods

### How to execute "alert(1)" through root Object, Pointer or other possible methods

Remember we have previously generate "alert" string and store It to _ variable.

  Function call                                   | Function prototype                     | Description
  ----------------------------------------------- | -------------------------------------- | --------------------------
  `window[_](++[[]][+[]]);`                       | `window['function_name'](arguments)`   | Call through the [object Window] (Represents an open window in a browser)
  `this[_](++[[]][+[]]);`                         | `this['function_name'](arguments)`     | Call through the global environment refers to the [object Window]
  `eval(_)(++[[]][+[]]);`                         | `eval['function_name'](arguments)`     | Interprets arbitrary javascript statements (Dangerous function)
  `var x = new Function(_+'('+(+!+[])+')'); x();` | `Function('function_name(arguments)')` | Another possible way to execute "alert(1)" (not a full non-alphanumeric)

###  How to execute with "[].constructor.constructor"

  Constructor property / Constructor function call      | Description
  ----------------------------------------------------- | -------------------------------------- | --------------------------
  `[].constructor`                                      | Array's constructor property returns an array's constructor function for an object - function Array() { [native code] } - ([].constructor === Array) = true
  `[].constructor.constructor`                          | Array's constructor property returns constructor Function - function Function() { [native code] } - ([].constructor.constructor === Function) = true
  `[].constructor.constructor("function_name")()`       | Constructor function that create a function object
  `[].constructor.constructor("funct(x)")()`            | Return funct(x) { } by Function object
  `[].constructor.constructor("alert(0)")()`            | Return alert(0) - we have already generated the string "alert" so we need to generate the remaining part "(0)"

### Generate non-alphanumeric "[].constructor.constructor by JS statements"

  Char index           | Return char   | Non-Alphanumeric
  -------------------- | ------------- | -----------------------------------
  "[object Object]"[5] | 'c'           | `({}+[])     [!+[]+!+[]+!+[]+!+[]+!+[]]`
  "[object Object]"[1] | 'o'           | `({}+[])     [+!+[]]`
  "undefined"[1]       | 'n'           | `([]['']+[]) [+!+[]]`
  "false"[3]           | 's'           | `([![]]+[])  [!+[]+!+[]+!+[]]`
  "true"[0]	           | 't'           | `([!![]]+[]) [+[]]`
  "true"[1]	           | 'r'           | `([!![]]+[]) [+!+[]]`
  "undefined"[0]	   | 'u'           | `([!![]]+[]) [!+[]+!+[]]`
  "[object Object]"[5] | 'c'           | `({}+[])     [!+[]+!+[]+!+[]+!+[]+!+[]]`
  "true"[0]	           | 't'           | `([!![]]+[]) [+[]]`
  "[object Object]"[1] | 'o'           | `({}+[])     [+!+[]]`
  "true"[1]	           | 'r'           | `([!![]]+[]) [+!+[]]`

### Generate parenthesis with argument "0" using sort(), then concat It to previous generated string "alert" stored in variable _

  Constructor property                     | Return string                       | Non-Alphanumeric
  ---------------------------------------- | ----------------------------------- | --------------------------
  [].sort                                  | function sort() { [native code] }   | `([] [([![]]+[])[++[++[!![]][+[]]][+[]]] + ({}+[])[+!+[]] + ([!![]]+[]) [+!+[]] + ([!![]]+[])[+[]]])`
  [].sort                                  | "function sort() { [native code] }" | `([] [([![]]+[])[++[++[!![]][+[]]][+[]]] + ({}+[])[+!+[]] + ([!![]]+[]) [+!+[]] + ([!![]]+[])[+[]]]+[])`

  String char index                               | Return char                         | Non-Alphanumeric
  ----------------------------------------------- | ----------------------------------- | --------------------------
  "function sort() { [native code] }"[12]         | ')'                                 | `([] [([![]]+[])[++[++[!![]][+[]]][+[]]] + ({}+[])[+!+[]] + ([!![]]+[]) [+!+[]] + ([!![]]+[])[+[]]]+[]) [!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]]`
  "function sort() { [native code] }"[13]          | '('                                 | `([] [([![]]+[])[++[++[!![]][+[]]][+[]]] + ({}+[])[+!+[]] + ([!![]]+[]) [+!+[]] + ([!![]]+[])[+[]]]+[]) [!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]]`

**Now concat the string "alert" stored at variable _ with "(0)"**

{% highlight js %}
_p = ([] [([![]]+[])[++[++[!![]][+[]]][+[]]] + ({}+[])[+!+[]] + ([!![]]+[]) [+!+[]] + ([!![]]+[])[+[]]]+[]) [!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]] + // '('
[]*[]                                                                                                                                                                          + // '0'
([] [([![]]+[])[++[++[!![]][+[]]][+[]]] + ({}+[])[+!+[]] + ([!![]]+[]) [+!+[]] + ([!![]]+[])[+[]]]+[]) [!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]+!+[]];  // ')'
_ += _p;                                                                                                                                                                         // "alert" += "(0)"
{% endhighlight %}

**Final concatenated code - full javascript non-alphanumeric code without using the [object Window]**

Generating `"[].constructor.constructor("alert(0)")();"`<br>
`"alert(0)"` was stored at variable `_`

{% highlight js %}
(function() {
  /**
   * Constructor property &                          Value
   * Constructor function call
   */
  ([] [(                                             // [].
    ({}+[]) [!+[]+!+[]+!+[]+!+[]+!+[]] +             // c
    ({}+[]) [+!+[]] +                                // o
    ([]['']+[]) [+!+[]] +                            // n
    ([![]]+[]) [!+[]+!+[]+!+[]] +                    // s
    ([!![]]+[]) [+[]] +                              // t
    ([!![]]+[]) [+!+[]] +                            // r
    ([!![]]+[]) [!+[]+!+[]] +                        // u
    ({}+[]) [!+[]+!+[]+!+[]+!+[]+!+[]] +             // c
    ([!![]]+[]) [+[]] +                              // t
     ({}+[]) [+!+[]] +                               // o
     ([!![]]+[]) [+!+[]]                             // r
  )]
  [                                                  // .
    ({}+[]) [!+[]+!+[]+!+[]+!+[]+!+[]] +             // c
    ({}+[]) [+!+[]] +                                // o
    ([]['']+[]) [+!+[]] +                            // n
    ([![]]+[]) [!+[]+!+[]+!+[]] +                    // s
    ([!![]]+[]) [+[]] +                              // t
    ([!![]]+[]) [+!+[]] +                            // r
    ([!![]]+[]) [!+[]+!+[]] +                        // u
    ({}+[]) [!+[]+!+[]+!+[]+!+[]+!+[]] +             // c
    ([!![]]+[]) [+[]] +                              // t
    ({}+[]) [+!+[]] +                                // o
    ([!![]]+[]) [+!+[]]                              // r
  ]) (_)();                                          // (“alert(0)”)();
}());
{% endhighlight %}

## ~4 Encoded possible characters list

If you find a method to retrieve the unknowns, please mail me to update the document.

  Char index           | Return char   | Non-Alphanumeric
  -------------------- | ------------- | -----------------------------------
  "false"[1]           | 'a'           | `([![]]+[])  [+!+[]]`
  "[object Object]"[2] | 'b'           | `({}+[])     [!+[]+!+[]]`
  "[object Object]"[5] | 'c'           | `({}+[])     [!+[]+!+[]+!+[]+!+[]+!+[]]`
  "undefined"[2]       | 'd'           | `([]['']+[]) [!+[]+!+[]]`
  "false"[4]           | 'e'           | `([![]]+[])  [!+[]+!+[]+!+[]+!+[]]`
  "false"[0]           | 'f'           | `([![]]+[])  [+[]]`
  unknown              | 'g'           | `unknown`
  unknown              | 'h'           | `unknown`
  "undefined"[5]       | 'i'           | `([]['']+[]) [!+[]+!+[]+!+[]+!+[]+!+[]]`
  "[object Object]"[3] | 'j'           | `([]['']+[]) [!+[]+!+[]+!+[]]`
  unknown	           | 'k'           | `unknown`
  "false"[2]           | 'l'           | `([![]]+[])  [!+[]+!+[]]`
  unknown              | 'm'           | `unknown`
  "undefined"[1]       | 'n'           | `([]['']+[]) [+!+[]]`
  "[object Object]"[1] | 'o'           | `({}+[])     [+!+[]]`
  unknown              | 'p'           | `unknown`
  unknown              | 'q'           | `unknown`
  "true"[1]            | 'r'           | `([![]]+[])  [!+[]+!+[]+!+[]+!+[]]`
  "false"[3]           | 's'           | `([![]]+[])  [!+[]+!+[]+!+[]]`
  "true"[0]            | 't'           | `([!![]]+[]) [[]*[]]`
  "undefined"[0]       | 'u'           | `([]['']+[]) [[]*[]]`
  unknown              | 'v'           | `unknown`
  unknown              | 'w'           | `unknown`
  unknown              | 'x'           | `unknown`
  unknown              | 'y'           | `unknown`
  unknown              | 'z'           | `unknown`

## ~5 References

* [http://www.w3schools.com/jsref/][w3c]
* [https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference][mozilla]
* [https://www.owasp.org/images/6/66/OWASP_Manchester_Nonalpha.pdf][oswap]

[w3c]:		  http://www.w3schools.com/jsref/ 									                "W3C - JavaScript and HTML DOM Reference."
[mozilla]:	https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference	"MDN - Mozilla Developer Network - JavaScript reference"
[oswap]:	 https://www.owasp.org/images/6/66/OWASP_Manchester_Nonalpha.pdf		"Non-alphanumeric code - With JavaScript & PHP by Gareth Heyes"

