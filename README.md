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
## Strings
## Arrow functions
## Destructuring
## Arrays
## The Spread Operator
## Rest and Default Parameters
## Maps
## Classes and subclasses
## Promises
## Native Modules
