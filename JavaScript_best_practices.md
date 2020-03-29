## Must-know Things

### Fat Arrow
Fat arrows are used as function shortcuts. Instead of writing `function()` , you can omit the function keyword and write  `() =>`. 
* You can omit the return statement and the curly brackets if you return only line, `() => "some string"` .  
* You can assign the function to a constant: `const MyExport = () => { code goes here }`.

### Template Literals
Three ways to specify strings in JavaScript.
* Double quote  \"string\" 
* Single quote  \'string\' 
* Back-tick  \`string\`

The back-tick string comes with special power. You can render variables into the string:
```javascript
const name = "James Bond";
const description = "a secret agent"
console.log(`${name} is ${description}.` );
```

Another back-tick feature is that the string can span multiple lines.
```javascript
console.log(`The
sky
is
blue`);
```

### Import and Export
You can import code from one file into another: `import { MyExport } from "./MyExport.js";`

### Destructuring  
You can destructure objects or arrays with this syntax: `const {userId, title} = json` 
```javascript
const fetch = require('node-fetch');
console.log("get a single JSON entry for testing");
fetch('https://jsonplaceholder.typicode.com/todos/1')
  .then(response => response.json())
  .then(json => {
    console.log(json);
    /*
    { userId: 1,
      id: 1,
      title: 'delectus aut autem',
      completed: false }
    */
    const {userId, title} = json;
    console.log(`the userId is ${userId}`);
    console.log(`the title is ${title}`);
    })
```

### Map
* Use the array map method constantly!. 
* Master it. 
* This works like a forEach loop.

```javascript
myArray = [1,2,3,4];
// square each element of array
console.log(myArray.map(element => element * element));

console.log(myArray.map(element => "My number is " + element)); 

console.log(myArray.map((element, index) => `At index ${index} the number is ${element} `));
```

### Filter
Filter the output for conditions. Filter returns an array.
```javascript
myArray = [1,2,3,4];
console.log (myArray.filter(element => element > 3)); 
```

### Find
* Find is similar to filter but does not return an array. 
* It will only return the first element that meets the condition and then exits.
```javascript
myArray = [1,2,3,4];
console.log(myArray.find(element => element === 3)); 
```

### Reduce
* It works like a loop that has an outside global variable that keeps the contents of a mathematical operation applied to each element of the array.
* The classic example is to add all the elements of an array together and return a single number.
* You can start the total or accumulator at any value
```javascript
myArray = [1,2,3,4];
console.log("use reduce to sum array and produce single result");
console.log(myArray.reduce((total, current) => total + current));
console.log(myArray.reduce((total, current) => total + current, 100)); 
```

### Ternary Operator
* It functions like an if-then-else statement.
* The concept of the ternary operator is easy to understand if you think of it as a shortcut for an if-then-else statement.
```javascript
const activeUser = true
console.log(activeUser ? "Welcome" : "Please sign in"); 
```

### Async and Await
The syntax of async and await easier to understand compared to promises.
```javascript
//Promise
const fetch = require('node-fetch');
console.log("get a single JSON entry for testing");
fetch('https://jsonplaceholder.typicode.com/todos/1')
  .then(response => response.json())
  .then(json => {
    console.log(json)
    })

//Async and Await
const fetch = require('node-fetch');
async function getUsers() {
    const response = await fetch('https://jsonplaceholder.typicode.com/users');
    const data = await response.json();
    return data;
}
getUsers()
    .then(data => {
        console.log(data.find(entry => entry.website === 'conrad.com')) });
```