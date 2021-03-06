
# JS Cheatsheet

### Array
```javascript
Properties
    Array.prototype
    Array.prototype[@@unscopables]
    array.length
Methods
    Array.from()
    Array.isArray()
    Array.observe()
    Array.of()
    Array.prototype.concat()
    Array.prototype.copyWithin()
    Array.prototype.entries()
    Array.prototype.every()
    Array.prototype.fill()
    Array.prototype.filter()
    Array.prototype.find()
    Array.prototype.findIndex()
    Array.prototype.forEach()
    Array.prototype.includes()
    Array.prototype.indexOf()
    Array.prototype.join()
    Array.prototype.keys()
    Array.prototype.lastIndexOf()
    Array.prototype.map()
    Array.prototype.pop()
    Array.prototype.push()
    Array.prototype.reduce()
    Array.prototype.reduceRight()
    Array.prototype.reverse()
    Array.prototype.shift()
    Array.prototype.slice()
    Array.prototype.some()
    Array.prototype.sort()
    Array.prototype.splice()
    Array.prototype.toLocaleString()
    Array.prototype.toSource()
    Array.prototype.toString()
    Array.prototype.unshift()
    Array.prototype.values()
    Array.prototype[@@iterator]()
```

### from(arrayLike[, mapFn[, thisArg])
```javascript
// Array-like object (arguments) to Array
function f() {
  return Array.from(arguments);
}
f(1, 2, 3); // [1, 2, 3]
// Any iterable object...
// Set
var s = new Set(["foo", window]);
Array.from(s);     // ["foo", window]
// Map
var m = new Map([[1, 2], [2, 4], [4, 8]]);
Array.from(m);     // [[1, 2], [2, 4], [4, 8]]  
// String
Array.from("foo"); // ["f", "o", "o"]
// Using an arrow function as the map function
// to manipulate the elements
Array.from([1, 2, 3], x => x + x);// [2, 4, 6]
```

### of(element0[, element1[, ...[, elementN]]])
```javascript
Array(42)            // [undefined × 42]   
Array.of(1);         // [1]
Array.of(1, 2, 3);   // [1, 2, 3]
Array.of(undefined); // [undefined]
```

### concat(value1[, value2[, ...[, valueN]]])
```javascript
let alpha = ['a', 'b', 'c'],
    numeric = [1, 2, 3];
let alphaNumeric = alpha.concat(numeric);
console.log(alphaNumeric);
// Result: ['a', 'b', 'c', 1, 2, 3]
entries()
var arr = ['a', 'b', 'c'];
var eArr = arr.entries();
console.log(eArr.next().value);  //[0, 'a']
console.log(eArr.next().value);  //[1, 'b']
console.log(eArr.next().value);  //[2, 'c']
//Same as above, using a for…of loop:
var arr = ['a', 'b', 'c'];
var eArr = arr.entries();
for (let e of eArr) {
    console.log(e);
}
```

### entries()
```javascript
var arr = ['a', 'b', 'c'];
var eArr = arr.entries();
console.log(eArr.next().value); // [0, 'a']
console.log(eArr.next().value); // [1, 'b']
console.log(eArr.next().value); // [2, 'c']
//Same as above, using a for…of loop:
var arr = ['a', 'b', 'c'];
var eArr = arr.entries();
for (let e of eArr) {
  console.log(e);
}
```

### every(callback[, thisArg])
```javascript
function isBigEnough(element, index, array){
    return element >= 10;
}
[12, 5, 8, 130, 44].every(isBigEnough); //false
[12, 54, 18, 130, 44].every(isBigEnough);//true
```

### fill(value[, start=0[, end=this.length]])
```javascript
[1, 2, 3].fill(4);              // [4, 4, 4]
[1, 2, 3].fill(4, 1);           // [1, 4, 4]
[1, 2, 3].fill(4, 1, 2);        // [1, 4, 3]
[1, 2, 3].fill(4, 1, 1);        // [1, 2, 3]
[1, 2, 3].fill(4, -3, -2);      // [4, 2, 3]
[1, 2, 3].fill(4, NaN, NaN);    // [1, 2, 3]
Array(3).fill(4);               // [4, 4, 4]
[].fill.call({ length: 3 }, 4); //{0: 4, 
                                   1: 4,
                                   2: 4,
                                   length: 3}
```

### filter()
```javascript
function isBigEnough(value) {
  return value >= 10;
}
var filtered = 
[12, 5, 8, 130, 44].filter(isBigEnough);
// filtered is [12, 130, 44]
```

### find(callback[, thisArg])
```javascript
//callback (element, index, array)
var inventory = [
    {name: 'apples', quantity: 2},
    {name: 'bananas', quantity: 0},
    {name: 'cherries', quantity: 5}
];
function findCherries(fruit) { 
    return fruit.name === 'cherries';
}
console.log(inventory.find(findCherries)); 
// { name: 'cherries', quantity: 5 }

function isPrime(element, index, array) {
  var start = 2;
  while (start <= Math.sqrt(element)) {
    if (element % start++ < 1) {
      return false;
    }
  }
  return element > 1;
}
console.log([4, 6, 8, 12].find(isPrime)); 
// undefined, not found
console.log([4, 5, 8, 12].find(isPrime)); 
// 5
```

### findIndex(callback[, thisArg])
```javascript
//callback (element, index, array)

console.log([4, 6, 8, 12].findIndex(isPrime)); 
// -1, not found
console.log([4, 6, 7, 12].findIndex(isPrime));
// 2 
```

### forEach(callback[, thisArg])
```javascript
//callback (element, index, array)
//does not modify array
function Counter() {
  this.sum = 0;
  this.count = 0;
}
Counter.prototype.add = function(array) {
  array.forEach(function(entry) {
    this.sum += entry;
    ++this.count;
  }, this);
  // --^-- Note
};
var obj = new Counter();
obj.add([2, 5, 9]);
obj.count       // 3 
obj.sum         // 16
```

### includes(searchElement[, fromIndex])
```javascript
[1, 2, 3].includes(2);     // true
[1, 2, 3].includes(4);     // false
[1, 2, 3].includes(3, 3);  // false
[1, 2, 3].includes(3, -1); // true
[1, 2, NaN].includes(NaN); // true
```

### indexOf(searchElement[, fromIndex = 0])
```javascript
var array = [2, 9, 9];
array.indexOf(2);     // 0
array.indexOf(7);     // -1
array.indexOf(9, 2);  // 2
array.indexOf(2, -1); // -1
array.indexOf(2, -3); // 0
```

### join([separator = ','])
```javascript
var a = ['Wind', 'Rain', 'Fire'];
var myVar1 = a.join();      
// assigns 'Wind,Rain,Fire' to myVar1
var myVar2 = a.join(', ');  
// assigns 'Wind, Rain, Fire' to myVar2
var myVar3 = a.join(' + '); 
// assigns 'Wind + Rain + Fire' to myVar3
var myVar4 = a.join('');    
// assigns 'WindRainFire' to myVar4
```

### keys(); values();
```javascript
var arr = ["a", "b", "c"];
var iterator = arr.keys();
console.log(iterator.next()); 
// { value: 0, done: false }
console.log(iterator.next()); 
// { value: 1, done: false }
console.log(iterator.next()); 
// { value: 2, done: false }
console.log(iterator.next());
// { value: undefined, done: true }

var eArr = arr.values();
for (let letter of eArr) {
  console.log(letter);  // a b c
}
```

### lastIndexOf(searchElement[, fromIndex=arr.length - 1])
```javascript
var array = [2, 5, 9, 2];
array.lastIndexOf(2);     // 3
array.lastIndexOf(7);     // -1
array.lastIndexOf(2, 3);  // 3
array.lastIndexOf(2, 2);  // 0
array.lastIndexOf(2, -2); // 0
array.lastIndexOf(2, -1); // 3
```

### map(callback[, thisArg])
```javascript
//callback(currentValue, index, array)
var kvArray = [{key:1, value:10}, 
               {key:2, value:20},
               {key:3, value: 30}];
var refArray = kvArray.map(function(obj){ 
   var rObj = {};
   rObj[obj.key] = obj.value;
   return rObj;
});
// refArray is now [{1:10}, {2:20}, {3:30}], 
// kvArray is still [{key:1, value:10}, 
                     {key:2, value:20},
                     {key:3, value: 30}]

var numbers = [1, 4, 9];
var doubles = numbers.map(function(num) {
  return num * 2;
});
// doubles is now [2, 8, 18]
// numbers is still [1, 4, 9]

var str = '12345';
Array.prototype.map.call(str, function(x) {
  return x;
}).reverse().join(''); 
// Output: '54321'
// Bonus: use '===' to test if original
// string was a palindrome
```

### pop(); push(element)
```javascript
let a = [1, 2, 3, 4]
let poped = a.pop()
//poped = 4, a = [1, 2, 3]

var veget = ['parsnip', 'potato'];
var moreVegs = ['celery', 'beetroot'];
// Merge the second array into the first one
// Equivalent veget.push('celery', 'beetroot')
Array.prototype.push.apply(veget, moreVegs);
console.log(veget); 
// ['parsnip', 'potato', 'celery', 'beetroot']
```

### reduce(cb[, initialValue]); reduceRight(cb[, initialValue])
```javascript 
//cb(prevVal, currentVal, currentIndex, arr)
var maxCB = (pre, cur)=>Math.max(pre.x, cur.x)
var maxCB2 = (max, cur)=>Math.max(max, cur)

// reduce() without initialValue
[ { x: 22 }, { x: 42 } ].reduce(maxCB);
// 42
[ { x: 22 }            ].reduce(maxCB);
// { x: 22 }
[                      ].reduce(maxCB);
// TypeError

// map/reduce; better solution, 
// also works for empty arrays
[ { x: 22 }, { x: 42 } ]
    .map( el => el.x )
    .reduce( maxCB2 , 0 );
```

### reverse()
```javascript
var myArray = ['one', 'two', 'three'];
myArray.reverse(); 
console.log(myArray) //['three', 'two', 'one']
```

### shift(); unshift(element)
```javascript
var letters = ['a', 'b', 'c', 'd'];
var shifted = letters.shift(); 
console.log('letters after: ' + letters); 
// letters after: 'b', 'c', 'd'
console.log('Removed this elem: ' + shifted); 
// Removed this element: a"
letters.unshift('žnj');
// letters after unshift: 'žnj', 'b', 'c', 'd'
```

### slice([begin[, end]]); splice(start, deleteCount[, item1[, item2[, ...]]])
```javascript
//splice mutate array, slice don't. 
//String equivalent is substring()
//if begin negative, counted from the end
'abc'.slice(1,2)           // "b"
[14, 3, 77].slice(1, 2)    //  [3]
var x = [14, 3, 77];
var y = x.slice(1, 2);
console.log(x);          // [14, 3, 77]
console.log(y);          // [3]
[14, 3, 77].slice(1, 2)     //  [3]
[14, 3, 77].splice(1, 2)    //  [3, 77]
```
                                                 
### some(callback[, thisArg])
```javascript
//callback(currentValue, index, array)
function isBiggerThan10(element, index, array){
    return element > 10;
}
[2, 5, 8, 1, 4].some(isBiggerThan10);  // false
[12, 5, 8, 1, 4].some(isBiggerThan10); // true
```

### sort([compareFunction])
```javascript
var scores = [1, 10, 2, 21]; 
scores.sort(); // [1, 10, 2, 21]

var numbers = [4, 2, 5, 1, 3];
numbers.sort(function(a, b) {
  return a - b;
});
console.log(numbers); // [1, 2, 3, 4, 5]
```

### toLocaleString()
```javascript
// returns string representing toLocaleString
// on each element, separated by local divider
```
                                                

### [@@iterator]()
```javascript
// initial value of the @@iterator is the same 
// func obj as initial value of arr.values()
var arr = ['w', 'y', 'k', 'o', 'p'];
for (let letter of arr) {
  console.log(letter);
}
var eArr = arr[Symbol.iterator]();
console.log(eArr.next().value); // w
console.log(eArr.next().value); // y
console.log(eArr.next().value); // k ...
```

