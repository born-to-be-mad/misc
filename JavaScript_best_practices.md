## Must-know Things

#Tips for console.log() usage
* Naming Output Variables
```javascript
function sum(a, b) {
  console.log({ b });
  return a + b;
}

sum(3, 5);
sum(4, 6);
```
* Advanced formatting
`console.log()` can format string similar to ` sprintf()`with the different specificators like  `%s`, `%i`  and similar.
```javascript
const user = 'james_bond';
const attempts = 3;

console.log('%s failed to login %i times', user, attempts);
// logs "james_bond failed to login 3 times"
```

| Specifier    | Value  |
| --------- | ---------- |
| `%s`      | Transform into string    |
| `%d` or `%i | Transform into number    |
| `%f`      | Transform into float number   |
| `%o`      | View with optimal formatting    |
| `%O`      | View with Javascript common formatting    |
| `%c`      | Used with CSS    |

* Log output using CSS styles
```javascript
console.log('%c Big message', 'font-size: 36px; font-weight: bold');
```

* Interactive Logs
Browsers such as Chrome and Firefox offer interactive logs of objects and arrays, and the Node console displays logs as text.
```javascript
const heroes = ['Neo', 'Morpheus', 'John Smith'];
console.log(heroes);

console.log(document.getElementById('root'));
```

* Large Objects in the Console
To see the full structure of the object, use `JSON.stringify()`
```javascript
const myObject = {
  propA: {
    propB: {
      propC: {
        propD: 'test'
      }
    }
  }
};

console.log(JSON.stringify(myObject, null, 4));
```

### Fat Arrow
Fat arrows are used as function shortcuts. Instead of writing `function()` , you can omit the function keyword and write  `() =>`. 
* You can omit the return statement and the curly brackets if you return only line, `() => "some string"` .  
* You can assign the function to a constant: `const MyExport = () => { code goes here }`.
* we can write less
```javascript
[1, 2, 3].map(i => i + 1).reduce((s, i) => s + i);
[1, 2, 3].filter(i => i % 2 == 0).sort();
[1, 2, 3].some(i => i % 2 == 0);
[1, 2, 3].every(i => i % 2 == 0);
```

### Template Literals
Three ways to specify strings in JavaScript.
* Double quote  \"string\" 
* Single quote  \'string\' 
* Back-tick  \`string\`

The back-tick string(sometimes called _template string_) comes with special power. 
The template string is just a better way of constructing strings cause you can render variables into the string.
It removes the challenges inherent in formatting strings. It can also evaluate the logic inside.
```javascript
const name = "James Bond";
const description = "a secret agent"
console.log(`${name} is ${description}.` );

let name = 'James', agentId = 7;
console.log(`Hello ${name}`);
let url = `http://secretagents.com/${agentId}`;
console.log(url);
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
This is truly magical. You can destruct objects and arrays. You can just get the property you are looking for easily.
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
    });

const [a, ...b] = [1, 2, 3]; // a becomes 1 and b becomes [2, 3]
const {id, person} = { id: 3, person: {name: 'James'}}; // id becomes 3 and person becomes {name: 'James'}
const newArray = [1, ...[2, 3]]; // newArray becomes [1,2,3]
//You can also destruct in a for loop
const people = [{ id: 7, person: {name: 'James'}}, { id: 10, person: {name: 'Alfred'}}];
for (var {id: id, person: {name: name}} of people) {
  console.log(`The person with id=${id} is ${name}.`);
}
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
