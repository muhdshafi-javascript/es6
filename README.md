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
- ***StartWith,endWith, includes, repeat:*** 
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
- regular anonymous functions use dynmic soping.
- Arrow functions use lexical scoping.  
```javascript
    var shafi = {
        name: 'Shafi',
        yob: 1988,
        doSomething: function (callBack) {
            callBack('doSomething');
        },
        getAge: function (callBack) {
            callBack(this.name, this.yob);
        }
    }
    //ES5
    shafi.doSomething(function (obj) {
        console.log('Callback is invoked from ' + obj);
    });
    //ES6
    shafi.doSomething(obj => console.log(`Callback is invoked from ${obj}`));

    //ES5
    shafi.getAge(function (name, yob) {
        var today = new Date();
        console.log(name + ' is ' + (today.getFullYear() - yob) + ' years old');
    });
    //ES6
    shafi.getAge((name, yob) => {
        const today = new Date();
        console.log(`${name} is ${today.getFullYear() - yob} years old`);
    });

    //this keyword
    //ES5 - anonymous funtions use dynamic scope 
    var vineesh = {
        name: 'Vineesh',
        yob: 1988,
        drawMe: function () {
            var vineeshDom = document.createElement('div');
            vineeshDom.innerHTML = '<h2>' + this.name + ' was born in ' + this.yob + ', click me </h2>';
            document.body.insertAdjacentElement('beforeend',vineeshDom);
            vineeshDom.addEventListener('click', function(){
                var today = new Date();
                console.log(this.name + ' is ' + (today.getFullYear() - this.yob) + ' years old');
                console.log('this:',this); //this points to vineeshDom
            });
        }
    };
    vineesh.drawMe();
    //Fix the this issue 
    //Using bind()
    var sudheesh = {
        name: 'Sudheesh',
        yob: 1987,
        drawMe: function () {
            var sudheeshDom = document.createElement('div');
            sudheeshDom.innerHTML = '<h2>' + this.name + ' was born in ' + this.yob + ', click me </h2>';
            document.body.insertAdjacentElement('beforeend',sudheeshDom);
            sudheeshDom.addEventListener('click', function(){
                var today = new Date();
                console.log(this.name + ' is ' + (today.getFullYear() - this.yob) + ' years old');
                console.log('this:',this); //this points to sudheesh object
            }.bind(this));
        }
    };
    sudheesh.drawMe();
    //Using extra local variable
    var shameer = {
        name: 'Shameer',
        yob: 1990,
        drawMe: function () {
            var that = this;
            var shameerDom = document.createElement('div');
            shameerDom.innerHTML = '<h2>' + this.name + ' was born in ' + this.yob + ', click me </h2>';
            document.body.insertAdjacentElement('beforeend',shameerDom);
            shameerDom.addEventListener('click', function(){
                var today = new Date();
                console.log(that.name + ' is ' + (today.getFullYear() - that.yob) + ' years old');
                console.log('this:',that); //that points to shameer object
            });
        }
    };
    shameer.drawMe();


    //ES6
    //Arrrow functions use lexical scope
    var paul = {
        name: 'Paul',
        yob: 1990,
        drawMe: function () {
            var paulDom = document.createElement('div');
            paulDom.innerHTML = '<h2>' + this.name + ' was born in ' + this.yob + ', click me </h2>';
            document.body.insertAdjacentElement('beforeend',paulDom);
            paulDom.addEventListener('click', event =>{
                var today = new Date();
                console.log(this.name + ' is ' + (today.getFullYear() - this.yob) + ' years old');
                console.log('this:',this); //this points to paul object
            });
        }
    };
    paul.drawMe();
```    
## Destructuring
- used to de-structuring the data structures
- automatically create varibales for us.
- can be used with both array and object.
- with object, the variable names should match with keys, otherwise we need to specify it.
- useful when a funtion return multple values.
```javascript
 //destructure Array
    var shafi = ['Shafi', 31];
    //ES-5
    var name = shafi[0];
    var age = shafi[1];
    console.log(name + ' is '+ age +' years old.');

    //ES-6
    const [name2, age2] = shafi;
    console.log(name2 + ' is '+ age2 +' years old.');

    //destructure Object
    const midhun = {
        firstName:'Midhun',
        lastName:'Sebastian',
        skills: ['Java', 'javaSript']
    };

    //ES-5
    var fstName = midhun.firstName;
    var lstName = midhun.lastName;
    var skillSet = midhun.skills;
    console.log('first name:', fstName, '\nlast name:', lstName,'\nskills', skillSet);

    //ES-6
    const{fName, lName} = midhun;
    console.log('first name:',fName,'\nlast name:', lName);
    //the keys and varible names should match.
    const{firstName, lastName, skills} = midhun;
    console.log('first name:', firstName, '\nlast name:', lastName,'\nskills', skills);

    //use a diifferent name other than the key
    const{firstName: fn, lastName: ln, skills: s} = midhun;
    console.log('fn:', fn, '\nln:', ln,'\s', s);
```    
## Arrays  
- ***Array.from():***  convert an array like data structure to an array, eg: Node list
- ***For-of:***  new loop which work like forEach and support continue and break as well.
- ***find() & findIndex():***  to find the index or elelemt which match the criteria given in callback argument
## The Spread Operator
Spread allows an iterable such as an array expression or string to be expanded in places where zero or more arguments (for function calls) or elements (for array literals) are expected, or an object expression to be expanded in places where zero or more key-value pairs (for object literals) are expected.  
- it can be used as a better replacement of apply() to pass an array or string to a funtion that expect a number of args.
- apply() can not be used with the *new()*, spread can be used, ypu can do shallow clone and concatination.
- it can e used with object literals as well *(ES7)*

## Rest and Default Parameters
## Maps
## Classes and subclasses
## Promises
## Native Modules
