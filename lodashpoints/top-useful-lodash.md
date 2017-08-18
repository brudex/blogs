Lodash Functions to cheat coding time

Transforming object literals and arrays is a repeatitive task that the javascript developer will continue to battle. You can only beat development time buy having utility functions that ease and save you lines of code. Lodash functions to the rescue. Practically everything lodash does is faster than native, it has a consistent api and browser compatibility (For old IE support use version 3.0 and before). 

This artile will present some powerfull lodash functions that can cut down on your javascript development time.
I really like the short-hand notations in _.filter().
I much prefer to write:
_.filter(persons, { name: 'Joe' });
over:
persons.filter(function(person) { return person.name === 'Joe'; });
or even the ES6 version:
persons.filter(person => person.name === 'Joe');


http://illarionvk.github.io/warsawjs-lodash/?full#4

 **Transforming  an array
 Its a common task to use Array.map function to return a newly transform array. Lodash has an easy syntax and performant version 


_.map()
 
```js 
 let result = _.map([1, 2, 3], function(value) {
   return value * 3;
 });
 // → [3, 6, 9]

 /*ES6*/
 _.map('Print Every Character', (x) =>  {return x });
 // → [ 72, 101, 108, 108, 111, 32, 87, 111, 114, 108, 100 ]
```

_.reduce()

```js
 _.reduce(
   [1, 2, 3],
   function(accumulator, value) {
     return accumulator + value;
   },
   0
 );
 // → 6

 _.reduce(
   [1, 2, 3],
   function(accumulator, value) {
     accumulator[value] = true;
     return accumulator;
   },
   {}
 );
 // → {1: true, 2: true, 3: true}
```

_.filter() 
```js
 _.filter([1, 2, 3, 4, 5, 6], function(value) {
   return value > 3;
 });
 ```


 _.reject()
 ```js
 // → [4, 5, 6]
 _.reject([1, 2, 3, 4, 5, 6], function(value) {
   return value > 3;
 });
 // → [1, 2, 3]
var users = [
  { 'user': 'barney', 'age': 36, 'active': false },
  { 'user': 'fred',   'age': 40, 'active': true }
];
 
_.reject(users, function(o) { return !o.active; });
// => objects for ['fred']
 
// The `_.matches` iteratee shorthand.
_.reject(users, { 'age': 40, 'active': true });
// => objects for ['barney']
 
// The `_.matchesProperty` iteratee shorthand.
_.reject(users, ['active', false]);
// => objects for ['fred']
 
// The `_.property` iteratee shorthand.
_.reject(users, 'active');

```

_.chain()

```js
 _.chain([1, 2, 3, 4, 5, 6])
   .filter(function(value) { return value > 3; }) // → [4, 5, 6]
   .map(function(value) { return value * 5; }) // → [20, 25, 30]
   .reduce(function(accumulator, value) {
     return accumulator + value;
   }, 0)
   .value();
 // → 75
```

```js
 _.chain([1, 2, 3, 4, 5, 6, 7, 3, 4, 4])
    .groupBy(function(item) {
      return item;
    })
    .pairs()
    .filter(function(pair) {
      return _.last(pair).length > 1;
    })
    .map(function(pair) {
      return _.first(pair);
    })
    .value();
     // → ["3","4"]
```

```js
  _.chain([1, 2, 3, 4, 5, 6, 7, 3, 4, 4])
    .groupBy(function(item) {})
    // → {"1":[1],"2":[2],"3":[3,3],"4":[4,4,4],"5":[5],"6":[6],"7":[7]}
    .pairs()
    // → [ ["1",[1]],["2",[2]],["3",[3,3]],
    //     ["4",[4,4,4]],["5",[5]],["6",[6]],["7",[7]] ]
    .filter(function(pair) {})
    // → [["3",[3,3]],["4",[4,4,4]]]
    .map(function(pair) {})
   .value();
    // → ["3","4"]
```

 Object Transformation
```js
 var item = {"a":{"b":{"c":3}}};
 
 _.get(item, 'a.b.c', 3);
 // → 3
 
 _.set(item, 'a.b.c', 5);
 // → {"a":{"b":{"c":5}}}
 
 _.has(item, 'a.b.c.d');
 // → false
```

String Manipulation

```js
 _.startCase('+Hello++world+');
 // → Hello World
 _.camelCase('+Hello++world+');
 // → helloWorld
 _.snakeCase('+Hello++world+');
 // → hello_world
```
_.debounce 

```js
function myFunc(a) {
   console.log(a);
}
let callingFunc  = _.debounce(myFunc, 1500, {leading: true});
 
callingFunc('first call'); 
callingFunc('second call'); 
callingFunc('last call');

// → last call
```


_.groupBy

```js
_.groupBy([6.1, 4.2, 6.3], Math.floor);
// => { '4': [4.2], '6': [6.1, 6.3] }
 
// The `_.property` iteratee shorthand.
_.groupBy(['one', 'two', 'three'], 'length');
// => { '3': ['one', 'two'], '5': ['three'] }
```

_.sortBy
 
```js
var users = [
  { 'user': 'fred',   'age': 48 },
  { 'user': 'barney', 'age': 36 },
  { 'user': 'fred',   'age': 40 },
  { 'user': 'barney', 'age': 34 }
];
_.sortBy(users, [function(o) { return o.user; }]);
// => objects for [['barney', 36], ['barney', 34], ['fred', 48], ['fred', 40]]
_.sortBy(users, ['user', 'age']);
// => objects for [['barney', 34], ['barney', 36], ['fred', 40], ['fred', 48]]
```


_.some

```js
_.some([null, 0, 'yes', false], Boolean);
// => true
 
var users = [
  { 'user': 'barney', 'active': true },
  { 'user': 'fred',   'active': false }
];
 
// The `_.matches` iteratee shorthand.
_.some(users, { 'user': 'barney', 'active': false });
// => false
 
// The `_.matchesProperty` iteratee shorthand.
_.some(users, ['active', false]);
// => true
 
// The `_.property` iteratee shorthand.
_.some(users, 'active');
// => true
```

```js
var users = [
  { 'user': 'barney',  'age': 36, 'active': true },
  { 'user': 'fred',    'age': 40, 'active': false },
  { 'user': 'pebbles', 'age': 1,  'active': true }
];
 
_.find(users, function(o) { return o.age < 40; });
// => object for 'barney'
 
// The `_.matches` iteratee shorthand.
_.find(users, { 'age': 1, 'active': true });
// => object for 'pebbles'
 
// The `_.matchesProperty` iteratee shorthand.
_.find(users, ['active', false]);
// => object for 'fred'
 
// The `_.property` iteratee shorthand.
_.find(users, 'active');
// => object for 'barney'
```


```js

var initialize = _.once(createApplication);
initialize();
initialize();
// => `createApplication` is invoked once

```


```js
var users = [
  { 'user': 'barney', 'age': 36 },
  { 'user': 'fred',   'age': 40 }
];
 
_.pluck(users, 'user');
// => ['barney', 'fred']
 
var userIndex = _.indexBy(users, 'user');
_.pluck(userIndex, 'age');
// => [36, 40] (iteration order is not guaranteed)

//pluck has been removed from version 4 in favour of map
var objects = [{ 'a': 1 }, { 'a': 2 }];

// in 3.10.1
_.pluck(objects, 'a'); // → [1, 2]
_.map(objects, 'a'); // → [1, 2]

// in 4.0.0
_.map(objects, 'a'); // → [1, 2]

```


***************************************************


**********************************************************
 find, once,, pluck, memoize, all.
Chaining is very important to keep from nesting a ton of fn calls. Similar to thread first operator in clojure.
Of course you can do these things with map, filter, reduce, but using lodash makes your code shorter and the intent is much clearer.

lodashs implementations of each,map,reduce are more performant than the native functions as they utilize the Just In Time compilation optimizations


***********************************************
For example, it’s a very common task to iterate an array and process all elements in this array in sequence. In some old browsers, the JavaScript Array object doesn’t have the method forEach(). To iterate an array, for loop is required as in Listing 1.1. process is the function to process elements in the array.


************************sOME************************\




