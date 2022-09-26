# NaN

- NaN represent as `Not-A-Number`.
 
- NaN is a number that is not a legal number.
 
- NaN is a Number Data type.
 
- NaN is the only value that compares unequal to itself.
 
- If NaN is involved in any mathematical operation, the result is also NaN.
  
- When NaN is one of the operands of any relational comparison (>, <, >=, <=), the result is always false.
 
- NaN compares **unequal** (via ==, !=, ===, and !==) to any other value — including to another NaN value.
  
- NaN is also one of the falsy values.

- To tell if a value is NaN, use `Number.isNaN()` or `isNaN()` to most clearly determine whether a value is NaN — or,


*example :*
```js
console.log("abc" / 2); // returns NaN
```
This above line gives NaN because / is a numerical operator which expects 2 numbers at both side, but since 'abc' is not a number even though js tries coercion.

### coerction
- Coercion means convert one data type to another dta type `( type casiting )`;


## isNaN vs Number.isNaN
- `isNaN` converts the argument to a Number and returns true if the resulting value is NaN.

- `Number.isNaN()` returns true if and only if the argument is of type Number and the value equals to NaN

- The `Number.isNaN()` method determines whether the passed value is NaN and its type is Number. 


```js
isNaN("vignesh"); // returns true because even though coercion takes place it's not a number

isNaN("51"); // returns false, because coercion happens and "51" will be converted as 51 which is a number
```

```js
isNaN(NaN);       // true
isNaN(undefined); // true
isNaN({});        // true

isNaN(true);      // false
isNaN(null);      // false
isNaN(37);        // false

// strings
isNaN('37');      // false: "37" is converted to the number 37 which is not NaN
isNaN('37.37');   // false: "37.37" is converted to the number 37.37 which is not NaN
isNaN("37,5");    // true
isNaN('123ABC');  // true:  parseInt("123ABC") is 123 but Number("123ABC") is NaN
isNaN('');        // false: the empty string is converted to 0 which is not NaN
isNaN(' ');       // false: a string with spaces is converted to 0 which is not NaN

// dates
isNaN(new Date());                // false
isNaN(new Date().toString());     // true

// This is a false positive and the reason why isNaN is not entirely reliable
isNaN('blabla');   // true: "blabla" is converted to a number.
                   // Parsing this as a number fails and returns NaN
                  
```


```js

Number.isNaN(NaN); // true
Number.isNaN(Number.NaN); // true
Number.isNaN(0 / 0); // true
Number.isNaN(37); // false

isNaN("NaN"); // true
isNaN(undefined); // true
isNaN({}); // true
isNaN("blabla"); // true
isNaN(true); // false, this is coerced to 1
isNaN(null); // false, this is coerced to 0
isNaN("37"); // false, this is coerced to 37
isNaN("37.37"); // false, this is coerced to 37.37
isNaN(""); // false, this is coerced to 0
isNaN(" "); // false, this is coerced to 0

```



# ParseInt()
- The `parseInt()` function parses a **string** argument and returns an integer of the specified

- The parseInt function converts its `first argument` to a string, parses that string, then returns an `integer or NaN.`

*syntax*
>- parseInt(string)
>- parseInt(string, radix)

- A radix parameter specifies the number system to use.

- 2 = binary, 8 = octal, 10 = decimal, 16 = hexadecimal.

- If radix is omitted, JavaScript assumes radix 10. If the value begins with "0x", JavaScript assumes radix 16.

-radix is optional parameter.


```js
parseInt('0xF', 16)
parseInt('F', 16)
parseInt('17', 8)
parseInt(021, 8)
parseInt('015', 10)    // but `parseInt('015', 8)` will return 13
parseInt(15.99, 10)
parseInt('15,123', 10)
parseInt('FXX123', 16)
parseInt('1111', 2)
parseInt('15 * 3', 10)
parseInt('15e2', 10)
parseInt('15px', 10)
parseInt('12', 13)

parseInt('Hello', 8)  // Not a number at all
parseInt('546', 2)    // Digits other than 0 or 1 are invalid for binary radix

parseInt('-F', 16)
parseInt('-0F', 16)
parseInt('-0XF', 16)
parseInt(-15.1, 10)
parseInt('-17', 8)
parseInt('-15', 10)
parseInt('-1111', 2)
parseInt('-15e1', 10)
parseInt('-12', 13)

parseInt(4.7, 10)
parseInt(4.7 * 1e22, 10)        // Very large number becomes 4
parseInt(0.00000000000434, 10)  // Very small number becomes 4

parseInt(0.0000001,10);
parseInt(0.000000123,10);
parseInt(1e-7,10);
parseInt(1000000000000000000000,10);
parseInt(123000000000000000000000,10);
parseInt(1e+21,10);

parseInt('0e0', 16)

parseInt('900719925474099267n')// 900719925474099300

parseInt('123_456') //123
```



# How to Clone an array in javascript

## 1. Spread Operator (Shallow copy)
 - The `spread operator` is a new addition to the features available in the JavaScript `ES6 `version.
 - The spread operator ... is used to `expand` or `spread` an `iterable` or an `array`.

*example*
```js
numbers = [1, 2, 3];
numbersCopy = [...numbers];
```

>- **Note :** This doesn’t safely copy multi-dimensional arrays. Array/object values are copied by reference instead of by value.

```js
numbersCopy.push(4);
console.log(numbers, numbersCopy);
// [1, 2, 3] and [1, 2, 3, 4]
// numbers is left alone
```
```js
nestedNumbers = [[1], [2]];
numbersCopy = [...nestedNumbers];

numbersCopy[0].push(300);
console.log(nestedNumbers, numbersCopy);
// [[1, 300], [2]]
// [[1, 300], [2]]
// They've both been changed because they share references
```

## 2. for loop 

```js
numbers = [1, 2, 3];
numbersCopy = [];

for (i = 0; i < numbers.length; i++) {
  numbersCopy[i] = numbers[i];
}

numbersCopy.push(4);
console.log(numbers, numbersCopy);
// [1, 2, 3] and [1, 2, 3, 4]
// numbers is left alone

```

## 3.map

- The map() method in JavaScript creates an array by calling a specific function on each element present in the parent array. It is a non-mutating method. 
- Generally map() method is used to iterate over an array and calling function on every element of array.
  
*syntax*
```js
array.map(function(currentValue, index, arr), thisValue)
```

```js
numbers = [1, 2, 3];
double = (x) => x * 2;

numbers.map(double);


numbers = [1, 2, 3];
numbersCopy = numbers.map((x) => x);


identity = (x) => x;
numbers.map(identity);
// [1, 2, 3]
```

## 4.Array.filter (Shallow copy)
- This function returns an array, just like map, but it’s not guaranteed to be the same length.
```js
// What if you’re filtering for even numbers?
[1, 2, 3].filter((x) => x % 2 === 0);
// [2]
```
- The input array length was 3, but the resulting length is 1.

- If your filter's predicate always returns true, however, you get a duplicate!
```js
numbers = [1, 2, 3];
numbersCopy = numbers.filter(() => true);
```
- Every element passes the test, so it gets returned.

>- Note: This also assigns objects/arrays by reference instead of by value.

## 5. Array.reduce (Shallow copy)
- I almost feel bad using reduce to clone an array, because it’s so much more powerful than that. But here we go…

```js
numbers = [1, 2, 3];

numbersCopy = numbers.reduce((newArray, element) => {
  newArray.push(element);

  return newArray;
}, []);
```


## 6. Array.slice (Shallow copy)
- slice returns a shallow copy of an array based on the provided start/end index you provide.

```js
//If we want the first 3 elements:

[1, 2, 3, 4, 5].slice(0, 3);
// [1, 2, 3]
// Starts at index 0, stops at index 3
If we want all the elements, don’t give any parameters

numbers = [1, 2, 3, 4, 5];
numbersCopy = numbers.slice();
// [1, 2, 3, 4, 5]
```

>- Note: This is a shallow copy, so it also assigns objects/arrays by reference instead of by value.

## 7. JSON.parse and JSON.stringify (Deep copy)
- JSON.stringify turns an object into a string.

- JSON.parse turns a string into an object.

- Combining them can turn an object into a string, and then reverse the process to create a brand new data structure.

>- Note: This one safely copies deeply nested objects/arrays!
```js
nestedNumbers = [[1], [2]];
numbersCopy = JSON.parse(JSON.stringify(nestedNumbers));

numbersCopy[0].push(300);
console.log(nestedNumbers, numbersCopy);

// [[1], [2]]
// [[1, 300], [2]]
// These two arrays are completely separate!
```

## 8. Array.concat (Shallow copy)
- concat combines arrays with values or other arrays.
```js
[1, 2, 3].concat(4); // [1, 2, 3, 4]
[1, 2, 3].concat([4, 5]); // [1, 2, 3, 4, 5]
```
- If you give nothing or an empty array, a shallow copy’s returned.

```js
[1, 2, 3].concat(); // [1, 2, 3]
[1, 2, 3].concat([]); // [1, 2, 3]
```

>- Note: This also assigns objects/arrays by reference instead of by value.

## 9. Array.from (Shallow copy)
>- This can turn any iterable object into an array. Giving an array returns a shallow copy.
```js
numbers = [1, 2, 3];
numbersCopy = Array.from(numbers);
// [1, 2, 3]
```
>- Note: This also assigns objects/arrays by reference instead of by value.