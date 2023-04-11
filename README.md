<!---
marp: true
theme: uncover
class: invert
headingDivider: 2
paginate: true
header: ![&e Tech](img/and-e-tech-logo-300.svg)
footer: 'Created with [Marp](https://marp.app) and [Github Pages](https://pages.github.com)'
backgroundImage: url('img/javascript-logo.svg')
backgroundPosition: 110% 120%
backgroundSize: 40%
style: |
  section,
  section code {
    font-size: 30px;
    text-align: left;
  }

  section ul,
  section ol,
  section img {
    margin-left: 0;
  }

  section.long p,
  section.long ul,
  section.long ol,
  section.long code, {
    font-size: 24px;
  }

  section .columns img {
    width: 100%;
  }

  section .columns {
    display: grid;
    grid-template-columns: repeat(2, minmax(0, 1fr));
    gap: 1rem;
  }

  section header img {
    height: 100px;
    width: 100px;
    float: right;
  }
--->

# Javascript Workshop

To ES6 and beyond!

# Let's clear up som "ES" confusion!

- ES stands for ECMAScript
- ECMAScript is the real name for JavaScript
- Sometimes you may see ES20XX - this is the old way of defining JS versions eg `ES2015`
- Nowadays we use a version number a la `ES6`
- Often `ES5` is used synonymously with "anything before ES6"

# String interpolation

```js
var username = 'Bill';

// Old style
var helloString = 'Hello ' + username + '!';

// new style
var helloString = `Hello ${username}!`;

// result
helloString === 'Hello Bill!'
```

# Optional chaining

```js
// old style (shudder!)
var email = null;
if (user && user.contact) email = user.contact.email;
// or
var email = user ? (user.contact ? user.contact.email : null) : null

// new style
var email = user?.contact?.email
```

# Object properties shorthand

```js
var id = 1;
var username = 'Bill';

// old style
var user = { id: id, username: username };

// new style
var user = { id, username };

// result
user === { id: 1, username: 'Bill'};
```

# Spread operator

# In arrays

```js
var otherNumbers = [3, 4];

// old style
var numbers = [1, 2].concat(otherNumbers);

// new style
var numbers = [1, 2, ...otherNumbers];

// result
numbers === [1, 2, 3, 4];
```

# In objects

```js
var userAttributes = { id: 1, username: 'andy' };
var updatedUserAttributes = { username: 'Bill', firstName: 'Stephen' };
```

<div class="columns">

```js
// old style
var user = {};
Object.keys(userAttributes).forEach(function (key) {
    user[key] = userAttributes[key];
});
Object.keys(updatedUserAttributes).forEach(function (key) {
    user[key] = updatedUserAttributes[key];
});
```

```js
// new style
var user = { ...userAttributes, ...updatedUserAttributes };
// or
var user = Object.assign(
  {},
  userAttributes,
  updatedUserAttributes
);
```

</div>

```js
// result
user === { id: 1, username: 'Bill', fistName: 'Stephen' };
```

# In functions

```js
function mergeUsers(userA, userB) {
  return { ...userA, ...userB };
}

var usersToMerge = [
  { firstName: 'Bill', lastName: 'Jobs' },
  { firstName: 'William' }
];
```

<div class="columns">

```js
// old style
mergeUsers(usersToMerge[0], usersToMerge[1]);
// or
mergeUsers.apply(this, usersToMerge);
```

```js
// new style
mergeUsers(...usersToMerge);
```

</div>

# Rest parameter

```js
var userToMergeTo = { id: 1, username: 'Bill' };
var otherUser1 = { id: 2, firstName: 'William' };
var otherUser2 = { id: 4, lastName: 'Jobs' };

mergeUsers(userToMergeTo, otherUser1, otherUser2);
```

<div class="columns">

```js
// Old style
function mergeUsers(userToMergeTo) {
  var otherUsers = Array.prototype.slice.call(arguments, 1);
  otherUsers.forEach(function (user) {
    // Object.keys FINISH ME
  })
  return [andy].concat(otherUsers);
}
```

```js
// new style (similar to python's *kwargs or ruby's splat (*))
function createUserCollection(andy, ...otherUsers) {
  return [andy].concat(otherUsers)
}
```

</div>

# Destructuring Assignments

# Array matching

```js
var numbers = [1, 2];

// Old style
var one = numbers[0];
var two = numbers[1];

// New style array matching
var [one, two] = numbers;
```

# Array matching - default values

```js
var numbers = [1];

// Old style
var one = numbers[0];
var two = numbers[1] === undefined ? 2 : numbers[1];;

// New style array matching
var [one, two = 2] = numbers;
```


# Object matching

```js
var user = { id: 1, username: 'andy' };

// Old style
var id = user.id;
var username = user.username;

// New style
var { id, username } = user;
```

# Deep object matching

```js
var user = { id: 1, username: 'andy', contact: { email: 'andy@example.com' } };

// Old style
var email = user.contact.email;

// New style
var { contact: { email } } = user;
```

# Object matching - default values

```js
var user = { id: 1, username: 'andy' };

// Old style
var id = user.id;
var username = user.username === undefined ? "anonymous" : user.username;

// New style
var { id, username = "anonymous" } = user;
```

# Parameter destructuring

# With array parameters

```js
var usersToMerge = [
  { firstName: 'Bill', lastName: 'Jobs' },
  { firstName: 'William' }
];
mergeUsers(usersToMerge);
```

<div class="columns">

```js
// Old style
function mergeUsers(usersArray) {
  var userA = usersArray[0];
  var userB = usersArray[1];
  return {
    ...userA,
    ...userB
  };
}
```

```js
// New style
function mergeUsers([userA, userB]) {
  return {
    ...userA,
    ...userB
  };
}
```

# With object parameters


```js
// Old style
function sayHello(user) {
  var username = user.username;
  return `Hello ${username}`;
}

// New style
function sayHello({ username }) {
  return `Hello ${username}`;
}
```

# Import and export destructuring

```js
// my-module.js
const myFunction = function () {};
const myConstant = Math.PI;
const MyModule = { myFunction, myConstant };

// exporting
export default MyModule;
// or
export myFunction;
export myConstant;

// importing
import 'my-module';
import MyModule from 'my-module';
import MyModule as TheirModule from 'my-module';
import { myFunction, MyConstant as TheirConstant } from 'my-module';
```

# Arrow functions

```js
// Old style function
function doSomething (someValue) {
  return someValue + 1;
}
// or
var doSomething = function (someValue) {
  return someValue + 1;
}

// new arrow style function
var doSomething = someValue => {
  return someValue + 1;
}
// or with an implicit return
var doSomething = someValue => someValue + 1;
```

# Usage as inline callback

```js
// Old style function
var usernames = users.map(function (user) {
  return user.username;
});

// new arrow style function
var usernames = users.map(user => user.username);
```

# Lexical this - What is this?

<div class="columns">

- Well... it depends!
- by default it is likely `window` or `global`
- using strict mode there is no default binding, it is `undefined`
- in an object it is the object itself
- in DOM event listeners it will be the `event.target` node
- usually though, `this` is related to whatever called the function asking for `this`

```js
this.numbers = [...Array(50).keys()];
this.multiplesOfFive = [];

this.numbers.forEach(function (number) {
  if (isMultiplesOfFive(number)) {
    // "this" here could be undefined or
    // it could be something else depending
    // on how this function is called
    this.multiplesOfFive.push(number);
  }
});
```
</div>

# Lexical this - the old options

```js
// option 1
var that = this;
this.numbers.forEach(function (number) {
  if (isMultipleOfFive(number)) that.multiplesOfFive.push(number);
})

// option 2
this.numbers.forEach(function (number) {
  if (isMultipleOfFive(number)) this.fives.push(number);
}, this)

// option 3
this.numbers.forEach(function (number) {
  if (isMultipleOfFive(number)) this.fives.push(number);
}.bind(this))
```

# Lexical this - arrow style

- In arrow functions `this` is always the object which defined the function
- you cannot use them for constructors (functions which use the `new` keyword)

```js
this.numbers.forEach(number => {
  if (isMultipleOfFive(number)) this.multiplesOfFive.push(number);
})
```

# Arrow functions - but when and why?

- We can use arrow functions __almost__ interchangeably for normal functions
- We cannot use them in constructors
- Knowing when and why is often a case of style unless you explicitly need special lexical this scoping or not

# Promises

<div class="columns">

```js
// Old style function
function doSomething (someId, onSuccess, onFailure, onFinally) {
  try {
    var data = getSomeData(someId);
    onSuccess(data);
  } catch (error) {
    onFailure(error);
  } finally {
    onFinally();
  }
}

doSomething(1, console.log, console.error, function () {
  // this always happens!
});
```

```js
// new Promise style
function doSomething (someId) {
  return new Promise((resolve, reject) => {
    try {
      var data = getSomeData(someId);
      resolve(data);
    } catch (error) {
      reject(error);
    }
  })
}

doSomething(1)
  .then(data => {
    var modifiedData = doSomethingWithData(data);
    return data;
  })
  .then(console.log)
  .catch(console.error)
  .finally(() => {
    // This always happens!
  })
```

<div>

# Throwing errors

```js
function doSomething () {
  return new Promise((resolve, reject) => {
    throw new Error("Ro roh!");
  })
}

doSomething().catch(error => {
  console.log(error);
  sendErrorToSomeErrorTrackingService(error);
})
```

# Promise.all()

<div class="columns">

```js
function runAll(functions, onSuccess, onError) {
  var results = [];
  var overallError;

  functions.forEach(function (func, index) {
    function handleFuncSuccess(data) {
      results[index] = data;
    }

    function handleFuncError(error) {
      overallError = error;
      break;
    }

    func(handleFuncSuccess, handleFuncError);
  });

  if (overallError) {
    onError(overallError);
  } else {
    onSuccess(results);
  }
}

function func1(onSuccess) { onSuccess('great success!') }
function func2(onSuccess) { onSuccess('yes, very nice') }
runAll([func1, func2], function (data) {
  data === [
    'great success!',
    'yes, very nice'
  ]
});

function func1(onSuccess) { onSuccess('great success!') }
function func2(onSuccess, onFailure) { onFailure('fail') }
runAll([func1, func2], null, function (error) {
  error === 'fail';
});
```

```js
Promise.all([
  Promise.resolve('great success!'),
  Promise.resolve('yes, very nice')
]).then(data => {
  // data === [
  //   'great success!',
  //   'yes, very nice'
  // ]
})

Promise.all([
  Promise.resolve('great success!'),
  Promise.reject('fail')
]).catch(error => {
  // error === 'fail'
})
```

</div>

# Promise.allResolved()

```js
Promise.allResolved([
  Promise.resolve('great success'),
  Promise.reject('failure')
]).then(data => {
  // data === [
  //   { status: 'fulfilled', value: 'great success' },
  //   { status: 'rejected', reason: 'failure' }
  // ]
})
// No catch needed here as the failed result is included in the result data
```

# async / await

<div class="columns">

```js
function fetchDataFromApi () {
  return new Promise((resolve, reject) => {
    try {
      var data = getData();
      resolve(data);
    } catch (error) {
      reject(error);
    }
  });
}

// Trigger the data request then carry on doing other stuff
fetchDataFromApi().then(data => {
  // do something with the data
  // when it eventually completes
})

// continue working on other stuff
```

```js
async function fetchDataFromApi () {
  var promise = new Promise((resolve, reject) => {
    try {
      var data = getData();
      resolve(data)
    } catch (error) {
      reject(error)
    }
  });

  return await promise;
}

// function will wait for promis to be resolved
// and assign the result before continuing
let data = fetchDataFromApi();

// continue working on other stuff
```
</div>

# Classes

<div class="columns">

```js
// old style
function Shape (x, y) {
    this.x = x;
    this.y = y;
}

Shape.prototype.move = function (x, y) {
    this.x = x;
    this.y = y;
};

var shape = new Shape(x, y);
shape.move(newX, newY);
```

```js
// new style
class Shape {
  constructor(x, y) {
    this.x = x;
    this.y = y;
  }

  move(x, y) {
    this.x = x;
    this.y = y;
  }
}

var shape = new Shape(x, y);
shape.move(newX, newY);
```

</div>

# Inheritance

<div class="columns">

```js
// old style
function Shape (sides) {
  this.sides = sides;
}

function Triangle () {
  Shape.call(this, 3);
}

Triangle.prototype = Object.create(
  Shape.prototype
);
```

```js
// new style
class Shape {
  constructor(sides) {
    this.sides = sides;
  }
}

class Triangle extends Shape {
  constructor() {
    super(3);
  }
}
```

</div>

# Modifying inhereted functionality

<div class="columns">

```js
// old style
function Shape (sides) {
  this.sides = sides
}

Shape.prototype.toString = function () {
  return "I have " + this.sides + " sides";
};

function Triangle () {
  Shape.call(this, 3);
}
Triangle.prototype = Object.create(Shape.prototype);

Triangle.prototype.toString = function () {
  return "As a Triangle " + Shape.prototype.toString.call(this);
}

var shape = new Shape(4);
shape.toString() === "I have 4 sides"

var triangle = new Triangle();
triangle.toString() === "As a Triangle I have 3 sides"
```

```js
// new style
class Shape {
  constructor (sides) {
    this.sides = sides;
  }

  toString () {
    return "I have " + this.sides + " sides";
  }
}

class Triangle extends Shape {
  constructor () {
    super(3)
  }

  toString () {
    return "As a Triangle " + super.toString();
  }
}

var shape = new Shape(4);
shape.toString() === "I have 4 sides"

var triangle = new Triangle();
triangle.toString() === "As a Triangle I have 3 sides"
```

</div>

# Static members

<div class="columns">

```js
// old style
function Shape (sides) {
  this.sides = sides;
}

Shape.defaultShape = function () {
  return new Shape(3);
}

var shape = Shape.defaultShape();
shape.sides === 3;
typeof shape === "object";
shape.__proto__.constructor.name === "Shape";
```

```js
// new style
class Shape {
  constructor (sides) {
    this.sides = sides;
  }

  static defaultShape () {
    return new Shape(0);
  }
}

var shape = Shape.defaultShape();
shape.sides === 3;
typeof shape === "object";
shape.__proto__.constructor.name === "Shape";
```

</div>

# Getters and setters

<div class="columns">

```js
// old style
function Shape (sides) {
  this._sides = sides;
}

Shape.prototype = {
    set sides (sides) {
      this._sides = sides;
    },

    get sides () {
      return this._sides;
    }
};

var shape = new Shape(0);
shape.sides = 2
shape.sides === 2
```

```js
// new style
class Shape {
  constructor(sides) {
    this._sides = sides;
  }

  set sides (sides) {
    this._sides = sides;
  }

  get sides () {
    return this._sides;
  }
}

var shape = new Shape(0);
shape.sides = 2
shape.sides === 2
```
</div>
