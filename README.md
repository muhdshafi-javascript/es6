# ES6(ES2015)
## var, let and const
- ***var*** is function scoped.
- ***const*** and ***let*** are block scoped.
- ***const*** is write protected as well, can't be mutated.
- ***var*** and ***let*** together, 
```javascript
    //var as outer and nested scope
    var age = 31;
    {
        var age = 32;
        console.log(age);   //32
    }
    console.log(age);       //32
```
```javascript
    //let as outer and nested scope
    let age = 31;
    {
        let age = 32;
        console.log(age);   //32
    }
    console.log(age);       //31
```
```javascript
    //var in outer scope and let as nested scope
    var name = 'Shafi';
    {
        let name = 'Sudheesh';
        console.log(name);  //Sudheesh
    }
    console.log(name);      //Shafi
```
```javascript
    //let as outer scope and var as nested scope
    let age = 31;
    {
        var age = 32;       //SyntaxError: Identifier 'age' has already been declared
        console.log(age);
    }
    console.log(age);
```

## Blocks and IIFEs
- ES6 Blocks do the same purpose as IIFE in ES5
```javascript
    //ES5 IIFE
    (function(){
        var x = 10;
        var y = 15;
        console.log(x + y);
    })();
    console.log(x + y);
```
```javascript
    //ES6 Block
    {
        let a = 10;
        let b = 15;
        console.log(a + b);
    }
    console.log(a + b);
```
## Strings
- ***Template Literal***: 
```javascript
    //Template literal
    let name = 'Shafi';
    let job = 'Software Developer'
    //ES5
    console.log(name + ' is a ' + job);
    //ES6
    console.log(`${name} is a ${job}`);
```
-***StartWith,endWith, includes, repeat:*** 
```javascript
    //StartsWith(), endsWith(), includes(), repeat()
    //ES5
    console.log(job.substring(0, 'Soft'.length) === 'Soft');
    console.log(job.substring(9, 9 +'Dev'.length) === 'Dev');
    console.log(job.substring(job.length-'per'.length, job.length) === 'per');
    console.log(job.indexOf('Dev') !== -1);
    //ES6
    console.log(job.startsWith('Soft'));
    console.log(job.startsWith('Dev', 9));//0 based position 
    console.log(job.endsWith('per'));
    console.log(job.includes('Dev'));
    console.log(name.repeat(3));
    console.log(`${name} `.repeat(3));
```
## Arrow functions
## Destructuring
## Arrays
## The Spread Operator
## Rest and Default Parameters
## Maps
## Classes and subclasses
## Promises
## Native Modules
