---
layout:     post
title:      "Short-Circuiting Evaluation"
date:       2017-04-19 19:00:00
author:     "Tobey"
header-img: "img/post-short-circuiting-bg.jpg"
---
<p>I've been resolving issues from sonarqube analysis for objective-c. Whenever code existed like this, a critical issue, collapsible if statements, is then reported.</p>
```objective-c
if(someEvaluation){
    if(otherEvaluation){
        //blablabla
    }
}
```
It suggests the issue to be fixed like this

```objective-c
if(someEvaluation && otherEvaluation){
    //blablabla
}
```
But what if I have the first evaluation checking for object to be not nil and then get the value in the object? Will the program crash if it's done in the same line of code?

```objective-c
if(dictionary != nil && [dictionary objectForKey:@"key"]){
    //blablabla
}
```
The answer is no. Due to the application of short-circuiting evaluation in C language, the second argument is executed or evaluated only if the first argument does not suffice to determine the value of the expression, which means the first condition will ensure that the dictionary is not nil before executing the second arugument.

Reference Link: [stack overflow link](http://stackoverflow.com/questions/14341008/if-statement-with-operator-checks-for-2nd-value), [Wikipedia: Short-Circuiting Evaluation](https://en.wikipedia.org/wiki/Short-circuit_evaluation)
