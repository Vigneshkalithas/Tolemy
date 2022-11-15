## 1.what is the Difference Between Promise.all() vs Promise.allSettled().?

 ### Promise.all()
   
- promise.all() methods takes input as array of promises and returns a single promise.
- all the values in the array was resolved they return  array of resolved values.
- if any one promise in the array was rejected,
- promise.all() rejected all.
- 
```js
var promise1 = Promise.resolve(5) 
var promise2 = Promise.resolve(2)
var promise3 =Promise.reject(3);
Promise.all([promise1,promise2, promise3])
.then(x=>console.log(x))
.catch(error=>console.log(error)) 

```

<!-- 3 will be printed  --> because promise3 was rejected and it goes to catch()


### Promise.allSettled()

- promise.allSettled() methods takes input as array of promises and returns a single promise.

- will waits for all the promise to be excuted, even if it is a rejected promise and returns a array ob objects with each object. having the result of setteled promise.

```js
var promise1 = Promise.resolve(4)
var promise2 = Promise.reject(5)
var promise3 = Promise.resolve(6)
var promise4 = Promise.reject(7)
Promise.allSettled([promise1,promise2,promise3,promise4])
  .then(x=>console.log(x) , j=>console.log(j))



<!-- output -->
[
{
    "status" : "fulfilled"
    "value"  : 4
},
{
    "status" : "rejected"
    "value"  : 5
},
{
    "status" : "fulfilled"
    "value"  : 6
},
{
    "status" : "rejected"
    "value"  : 7
},
]

```



## 2.what is the Difference between Promise.any() vs Promise.race()


### Promise.any()

- promise.any()methods takes input as array of promises, and returns single promises.
- it focus only resolved state anfd skip the reject state.
- it returns a 1st resolved promise.

```js
var promise1 = Promise.resolve(4)
var promise2 = Promise.reject(5)
var promise3 = Promise.resolve(6)
var promise4 = Promise.reject(7)
Promise.any([promise1,promise2,promise3,promise4])
  .then(x=>console.log(x) , j=>console.log(j))
.catch(z=>console.lof(z))

// output : 4

```

### Promise.race()

- Promise.race() takes input as a array of promise and returns a single promise.
- it returns 1st promise which get settled. if its a resolve or rejected state.

```js 
var promise1 = Promise.reject(10)
var promise2 = Promise.resolve(5)
var promise3 = Promise.resolve(6)
var promise4 = Promise.reject(7)
Promise.race([promise1,promise2,promise3,promise4])
  .then(x=>console.log(x) , j=>console.log(j))

// output : 10
```


## 3.List all lifecycle methods and their equivalent hook.?


### mounting 
- componentWillmount
  
 ```js
 useEffect(()=>{

 },[])
  ```
> note :in react v18 it will load 2 times initially, older version loads only one time. 

 - componentDidmount - doesn't have equivalent hook.

### updating

- componentWillUpdate - doesn't have equivalent hook.

- componentDidUpdate

```js
useEffect(() => {})
//   (or)
useEffect(() => {}, [dependencyArray]);
```
> In dependency array we give props or state value 
> whenever array values in the dependency in array is changed the useEffect was called.
>you didn't give the value in the dependency array
>also act as same.


### unMounting

- componentUnMount 
- 
  ```js
  useEffect( ()=>{
    return ()=>{}
  },[])
  ```
> whenever unmount happens the return function was  excuted


## 4. What is higher order function? Explain with an example.?

a function can take another function as a arguement or that return a new function or both is called as higher order function.

```js
var array = [1,2,3,4];
var rsult = array.map((key)=>{
    return key*2
}) 
```
> here map function return a new function.


## 5.What is the difference between event stoppropagation vs stopimmediatepropagation. Explain with an example.?

stopPropagation and stopImmidiatePropagation are two methods are affect the nestedelements.eventflows.

```html
<div id="div">  div tag
    <p id="para"> para tag
        <a id="anchor">anchor tag</a>
    </p>
</div>
```

```js
var anchorEle = document.getElementById("anchor")
anchorEle.addEventListener("click" , Anchor(event));

var paraEle = document.getElementById("para")
paraEle.addEventListener("click" , Para());


var divEle = document.getElementById("div")
divEle.addEventListener("click" , Div());

function Anchor(event){
  console.log("this is a")
  event.stopPropagation();
 
}

function Para(){
  console.log("this is para")
}

function Div(){
  console.log("this is div")
}
```


>here order of excution of event flow is 1st anchor event trigger then para then div if you use stopProgation in Anchor function the flow in not spread to parent stoped. only that one event was triggered. parent event was not triggered.



### stopImmidiatePropagation
 
 ```html
 <div>
    <p>
        <a></a>
    </p>
 </div>
 ```
>let assume if  we have the <p></p> element. the element have 2 events.
>and we give the stopImmidiatePropagation() to the first event.
>1st event was triggered, which means only one event was performed other >will be stopped.


## 6.What is "key" prop and what is the benefit of using it in arrays of elements?

- React has virtual DOM instead of Real DOM, for permance reason.
- Keys are used in React to identify which items in the list are changed, updated, or deleted.
- keys are used to identify the elments in virtual dom.
- let asume arrays of elements are there we map the array.
  key is used ti identify the particular element.



## 7).What is Lifting State Up in React? Explain with example.?
- let assume one parent component A. and it has two child Components B and C,  B and C are cousins. they two component wants same data.
- if the data was inside the B is not access by C also the data inside the C is not access by B, so we maintain the state in Parent A component. 
- so we lift the the state in child component to parent component os called Lifting state up.  

```js
 function  ParentA(){
  const [like,setLike] = useState(0);
  return(
    <>
<ChildB like={like} setLike={setLike}/>
<ChildC like={like} setLike={setLike}/>
       )
 }
```
```js
 function ChildB({like,setLike}){

   return(<>
   <div>
   <button onclick={()=>setLike(like+1)}>{like}</button>
   </div>
   )
 }
 ```

```js
  function ChildC({like,setLike}){

   return(<>
   <div>
   <button onclick={()=>setLike(like+1)}>{like}</button>
   </div>
   )
 }

``` 

## 8.Explain the difference between Object.freeze() vs const
### object.freeze()
- The Object.freeze() method freezes an object.
- makes the properties non-writable and non-configurable.
- new properties cannot be added, existing properties cannot be removed.
- value cannot be changed.

```js
const obj = {
  prop: 42
};

Object.freeze(obj);

obj.prop = 33;
// Throws an error in strict mode

console.log(obj.prop);
// expected output: 42

```

### const

- const is used for declaring the value 
- where re-declaration and re-assignment is not possible.

```js

const c = 5;

c= 6 // trow error can't be redecler.

const c = 8 // throw error cant be ressign.

```

## What strict mode in javascript?

- `use strict` is  es6 feature.
- it was not a statement, its a expression, it indicates the codes are in strict mode.
- this method preventing your code from undeclered variables.

```js

// before stict mode 
x = 3.14;       // This will not cause an error.

//after strict mode 

 "use strict";

 x=3.14        // This will cause an error

```


## 10 .What is difference between proto vs prototype in Object? Explain with an example.?

proto is a object which refers to the properties from where it has inherited them and prototype is an constructor which is available on all non-primitive datatypes

```js

var karthi = { bike: "Xtreme" };
var gopi = { car: "Thar" };
var zeni = { accessories: ["earphones", "charger"] };

Object.setPrototypeOf(karthi, gopi);
Object.setPrototypeOf(gopi, zeni);

console.log(karthi.__proto__); // Now karthi has access to gopi's property which is __proto__

```

## 11.What will be the output of the following JavaScript code? Why?
```js
var grades = "S";
var answer;
switch (grades) {
  case "S":
    answer += "10";
  case "A":
    answer += " 8";
  case "B":
    answer += " 6";
  default:
    answer += " 0";
}
document.write(result); // returns 'undefined10 8 6 0'

```


## 12.What is the output of this code snippet? and Why.?
```js
for (var i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}

for (let i = 0; i < 3; i++) {
  setTimeout(() => console.log(i), 1);
}
```
0,1,2 and 0,1,2 because each time the setTimeout is kept in callBackQueue where the first setTimeout is executed first followed by the same order


## 13.What's the output? Why.?
```js
const person = {
  name: "Lydia",
  age: 21,
};

const changeAge = (x = { ...person }) => (x.age += 1);
const changeAgeAndName = (x = { ...person }) => {
  x.age += 1;
  x.name = "Sarah";
};

changeAge(person); // prints 22
changeAgeAndName();

console.log(person);
```

- 22 will be the output for changeAge(person) , because the argument passed is person object.

> For changeAgeAndName it'll be {
>    age: 22, name: 'Sarah'
> } Here, the argument is not passed so the parameter is checked which > as a default value

