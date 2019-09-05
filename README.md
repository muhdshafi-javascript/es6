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
```javascript
    var container = document.createElement('div');
    container.innerHTML = `<ol>
                                <li>Coffee</li>
                                <li>Tea</li>
                                <li>Milk</li>
                            </ol>`;
    document.body.appendChild(container);
    var nodeList = document.getElementsByTagName('li');
    console.log('is nodeList an Array: ', nodeList instanceof Array);
    //*** Iterate over Array like list ***
    //ES-5, we need to use hack here
    var nodeArray = Array.prototype.slice.call(nodeList);
    console.log('is nodeArray an Array: ', nodeArray instanceof Array);
    nodeArray.forEach(function (element) {
        console.log(element.textContent);
    });

    //ES-6, convert Array like data structure to an Array
    const nodes = Array.from(nodeList);
    console.log('is nodes an Array: ', nodes instanceof Array);


    //Continue or Break
    //ES-5, we have to use traditional for loop as the ForEach support Continue or Break 
    for (var i = 0; i < nodeArray.length; i++) {
        if (nodeArray[i].textContent === 'Coffee')
            continue;
        if (nodeArray[i].textContent === 'Milk')
            break;
        console.log(nodeArray[i].textContent);
    }

    //ES-6, new loop, For-of
    for (let current of nodeArray) {
        if (current.textContent === 'Coffee')
            continue;
        if (current.textContent === 'Milk')
            break;
        console.log(current.textContent);
    }

    // find indices or find a values which match a criteria, from an array
    //ES-5
    var ages = [12, 17, 8, 21, 5, 22];

    //ES-6 , find() and findIndex()
    var fullAges = ages.map(function (element) {
        return element >= 18;
    });
    console.log(fullAges.indexOf(true));
    console.log(ages[fullAges.indexOf(true)]);

    //ES-6
    console.log(ages.findIndex(current => current >= 18));
    console.log(ages.find(current => current >= 18));
```    
## The Spread Operator
Spread allows an iterable such as an array expression or string to be expanded in places where zero or more arguments (for function calls) or elements (for array literals) are expected, or an object expression to be expanded in places where zero or more key-value pairs (for object literals) are expected.  
- it can be used as a better replacement of apply() to pass an array or string to a funtion that expect a number of args.
- apply() can not be used with the *new()*, spread can be used, ypu can do shallow clone and concatination.
- it can be used with object literals as well *(ES7)*  
```javascript
   //with Array
    function sumOfFour(a, b, c, d) {
        return a + b + c + d;
    }
    //expected input
    console.log('regular: ', sumOfFour(1, 2, 3, 4));
    //with Array as input
    var inputArr = [1, 2, 3, 4];
    //ES-5
    console.log('using ES-5 apply: ', sumOfFour.apply(null, inputArr));
    //ES-6
    console.log('using ES6 spread:', sumOfFour(...inputArr));
    const arr1 = [1, 2, 3];
    const arr2 = [4, 5, 6];
    console.log('array concatination: ', [...arr1, ...arr2]);
    //use with new(), apply can not be used here.
    var dateFields = [1988, 9, 17];  // 17 Oct 1988
    var d = new Date(...dateFields);
    console.log('date: ', d);

    //with String
    function combineString(s1, s2, s3, s4) {
        return s1 + 'A' + s2 + 'B' + s3 + 'C' + s4 + 'D';
    }
    console.log(combineString(...'abcde'));

    //with Object
    const person = {
        name: 'Shafi',
        age: 31
    }
    const employee = {
        designation: 'R&D Development Manager',
        skills: ['javaScript', 'Java']
    }

    const clone = { ...person };
    console.log('clone: ', clone);
    console.log('combine: ', { ...person, ...employee });
```    
## Rest and Default Parameters  
 - The rest parameter allows us to represent an indefinite number of arguments as an array. 
 - The syntax is same as speard operator, but the rest paramether is used in funtion declration where as spread operator is used when invoking a function.
 - we can also mix regular parameters and rest parameter, but only the last one can be a rest parameter.
```javascript
    //ES-5
    function getAges(){
        var currentYear = new Date().getFullYear();
        console.log('is arguments an array: ', arguments instanceof Array);
        var argArray = Array.prototype.slice.call(arguments);
        argArray.forEach(function(yob){
            console.log(currentYear - yob);
        });
    }
    getAges(1988, 1990, 1965, 2008);
    console.log('-----------------');
    //ES-6
    function getAgesNew(...yobs){
        var currentYear = new Date().getFullYear();
        yobs.forEach(yob => console.log(currentYear - yob));
    }
    getAgesNew(1988, 1990, 1965, 2008);
    console.log('-----------------');

    //pass addiotional parameter
    //we have to split the argument to acheive it in ES-5.
    function getAgesIn(year, ...yobs){
        yobs.forEach(yob => console.log(year - yob));
    }
    getAgesIn(2030, 1988, 1990, 1965, 2008);
```    
ES6 provides an easier way to set the default values for the parameters of a function as shown below:  
```javascript  
  //ES5
    function Person(firstName, lastName, age, nationality){

        if(nationality === undefined ){
            nationality = 'Indian';
        }

        this.firstName = firstName;
        this.lastName = lastName;
        this.age = age;
        this.nationality = nationality;
    }

    var shafi = new Person('Muhammed', 'Shafi');
    console.log('shafi:', shafi);
    var abin = new Person('Abin', 'Stephan', 30, 'Canadian');
    console.log('abin:', abin);

    //ES6
    function Student(firstName, lastName, age =32, department='CSE'){
        this.firstName = firstName;
        this.lastName = lastName;
        this.age = age;
        this.department = department;
    }

    console.log('Vinessh:', new Student('Vineesh', 'Chola', 31));
    console.log('Sudheesh:', new Student('Sudheesh', 'Athra', undefined, 'EEE'));
```    
## Maps
## Classes and subclasses  
- Class and Objects  
    - Classes provide a easier syntax for prototype inheritance.
    - Only the Syntax is new, the semantics are same.  
    - Class allows only funtions to be defined inside, properties should defined through the constructor.(it is to avoid inherit the propertites)
```javascript 
    //ES5
    var Person5 = function (name, yob, job) {
        this.name = name;
        this.yob = yob;
        this.job = job;
    }
    Person5.prototype.getAge = function () {
        var now = new Date();
        console.log(this.name + ' is ' + (now.getFullYear() - this.yob) + ' years old');
    }
    //static method
    Person5.sayHello = function(){
        console.log('Hello...');
    }

    var shafi = new Person5('Shafi', 1988, 'SDE');
    console.log('shafi:',shafi);
    shafi.getAge();
    Person5.sayHello();

    //ES6
    class Person6 {
        constructor(name, yob, job) {
            this.name = name;
            this.yob = yob;
            this.job = job;
        }

        getAge() {
            var now = new Date();
            console.log(this.name + ' is ' + (now.getFullYear() - this.yob) + ' years old');
        }

        //Static method
        static sayHello(){
            console.log('Hello...');
        }
    }

    const vineesh = new Person6('Vineesh', 1988, 'SDE');
    console.log('vineesh:',vineesh);
    vineesh.getAge();
    console.log(Person6);
    Person6.sayHello();    

```    
- Class inheritance  
```javascript 
    //ES5
    //Super class
    var Person5 = function (name, yob) {
        this.name = name;
        this.yob = yob;
    };
    //Methods on super class
    Person5.prototype.getAge = function () {
        var now = new Date();
        console.log(this.name + ' is ' + (now.getFullYear() - this.yob) + ' years old');

    };
    //Sub class
    var Student5 = function (name, yob, department) {
        Person5.call(this, name, yob);
        this.department = department;
    };
    //connect prototype chain(order is important here, 
    //othewise the funtions will be defined on the default prototype object 
    //and those will not accessible after connecting the chain)
    Student5.prototype = Object.create(Person5.prototype);
    //Methods on sub class
    Student5.prototype.getDep = function () {
        console.log(this.name + ' is a student of ' + this.department + ' department');
    };


    var shafi = new Student5('Shafi', 1988, 'CSE');
    shafi.getAge();
    shafi.getDep();

    var shameer = new Person5('Shameer', 1990);
    shameer.getAge();
    //shameer.getDep();  //shameer.getDep is not a function


    //ES6
    class Person6 {
        constructor(name, yob) {
            this.name = name;
            this.yob = yob;
        }
        getAge() {
            var now = new Date();
            console.log(this.name + ' is ' + (now.getFullYear() - this.yob) + ' years old');
        }
    }
    class Student6 extends Person6{
        constructor(name, yob, department){
            super(name, yob);
            this.department = department;
        }
        getDep(){
            console.log(this.name + ' is a student of ' + this.department + ' department');
        }
    }

    const midhun = new Student6('Midhun', 1988, 'CSE');
    midhun.getAge();
    midhun.getDep();
```  

## Promises  
### Asynchronous funtions
- Web APIs are the set of API provided by the browser and that we can communicate with using JavaScript in order to solve our front-end problems  
eg: setTimeout(), DOM events, XMLHttpRequest()    
These lives out side the javaScript engine, there are also in the Javascript runtime. 
- **Javascript Engine vs Runtime environment**  
  - A ***JavaScript engine*** is a program responsible for translating source code into machine code and executing the translation result on a computer’s central processing unit 
    - Chrome V8 – As you probably guessed the engine shipped in Google Chrome. It’s an open source project written in C++. V8 is also used in Opera, NodeJS, and Couchbase.  
    - SpiderMonkey – The open source engine implemented in C++. It’s maintained by Mozilla Foundation. You can find it in Firefox.  
    - Nitro – The engine developed by Apple. It’s used in Safari.  
    - Chakra – Developed by Microsoft as the JavaScript engine for Edge browser.  
  - ***JavaScript Runtime environment:*** In the web development, you don’t usually use the engine directly. The JavaScript engine works inside an environment, which provides additional features to your scripts that you can use at runtime.   
- **Event loop** 
    - It is a part of the JavaScript runtime environment, is a mechanism responsible for handling callbacks.  
    - When you create a callback, you always associate it with a particular event. If that event occurs, the environment puts your callback into a so-called Event handlers queue. The Event loop constantly monitors the queue and executes its elements in the order they arrive.  
    - Callbacks are a l w a y s executed completely. The Event loop runs one callback at a time. No context switching. All callbacks in the queue have to wait until the current one is finished.  

If a script runs too long, it blocks others. That’s why callbacks should be relatively short and simple.

## Native Modules
