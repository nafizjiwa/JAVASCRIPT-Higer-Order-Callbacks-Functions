# JAVASCRIPT-Higer-Order-Callbacks-Functions

## Callback Functions & `forEach` in JavaScript**
What is a **Callback function**:
• 	A function passed as an argument to another function
• 	Makes code modular, flexible, and reusable

**`forEach`** array method uses a callback 

### **How**
• 	`forEach` loops through each element and pushes it into callback    
• 	It receives index + array optionally
•   NO new array   

### **Example**
```js
const numbers = [1, 2, 3, 4, 5];
numbers.forEach(number => console.log(number * 2));
***push inot a new array
numbers.forEach(num => {newArrayDoubled.push(num * 2); });

```

### **`forEach` Callback Parameters**
1. **element** – the current item  
2. **index** – the position of the item  
3. **array** – the full array being iterated  

Example:
```js
numbers.forEach((num, index, arr) => {
  console.log(`Element ${num} at index ${index} in ${arr}`);
});
```
Here’s a **clean, point‑form summary** of higher‑order functions — tight, clear, and classroom‑ready:

---

## **Higher‑order functions (HOF)** :
  - **Takes one or more functions as arguments**, or  
  - **Returns a function**, or  **Does both**
**Are First‑Class Ctizens** (can be stored, passed, and returned as a value)

### **Why They Matter**
- Make code **flexible**, **reusable**, and **modular**
- Enable **declarative programming** (describe *what* you want, not *how* to do it)

### **Example: Passing a Function In**
```js
function operateOnArray(arr, operation) {
  let result = [];
  for (let i = 0; i < arr.length; i++) {
    result.push(operation(arr[i]));
}
  return result;
}

function double(x) {
    return x * 2;
}

let numbers = [1, 2, 3, 4, 5];
let doubledNumbers = operateOnArray(numbers, double);
console.log(doubledNumbers); // [2, 4, 6, 8, 10]
```
- `operateOnArray` is a HOF because it **accepts a function** (`double`)  
- Lets you reuse the same loop with different operations

### **Example: Returning a Function**
```js
function multiplyBy(factor) {
  return function(number) {
    return number * factor;
  }
}
let double = multiplyBy(2);
let triple = multiplyBy(3);
console.log(double(5)); // 10
console.log(triple(5)); // 15
```
- `multiplyBy` is a HOF because it **returns a new function**

### **Array methods are HOFs and take in callback functions:
  - **`map()`**
  - **`filter()`**
  - **`reduce()`**
  - **`forEach()`**
---
Here’s a **tight, condensed summary** of the `map` method — clean and perfect for quick reference:

---

## **The `map` Method**

- **`map` creates a new array** a callback function is applied to each element of an array.  
- **Does not change** the original array.  
- Returns a transformed value.  
- `map callback` accepts **3 arguments**:
  1. **element** – current item  
  2. **index** – position of the item  
  3. **array** – the full array being mapped  
- USED for transforming data (e.g., doubling numbers, extracting properties, formatting values).

### **Example**
```js
const numbers = [1, 2, 3];
const doubled = numbers.map(n => n * 2);
// numbers → [1, 2, 3]
// doubled → [2, 4, 6]
```

## **The `filter` Method**

- **`Creates a new array`** of elements that pass a test in the callback.  
- Original array is **not modified**.  
- Callback return **true** (keep the element) or **false** (exclude it).  
- If all elements Fail the test, `filter` returns an **empty array**.  
- Callback receives up to **three arguments**:
  1. **element** – current item  
  2. **index** – position of the item  
  3. **array** – the full array being filtered  
- Used for selecting items based on conditions (e.g., even numbers, valid values, matching properties).

### **Example**
```js
const numbers = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10];
const evenNumbers = numbers.filter((num) => num % 2 === 0);

console.log(evenNumbers); // [2, 4, 6, 8, 10]
```

### **Object Filtering Example**
```js
const developers = [
  { name: "Alice", age: 25 },
  { name: "Bob", age: 30 },
  { name: "Charlie", age: 35 },
  { name: "David", age: 25 }
];
const youngPeople = developers.filter(person => person.age < 30);
console.log(youngPeople);
```

Here’s a **clean, condensed summary** of the `reduce` method — tight, clear, and perfect for quick reference:

---

## **The `reduce` Method**

- **Processes an ARRAY --> into a SINGLE VALUE** (number, string, object, array, etc.).
- It runs a **reducer function** on each element, passing along a **running result** called the *accumulator*.
- The reducer function receives:
  1. **accumulator** – the ongoing total/running result  
  2. **currentValue** – the current array element
  3. Accepts an **initial value** for the accumulator; otherwise, 1st array element is used.

### **Example**
```js
const numbers = [1, 2, 3, 4, 5];
const sum = numbers.reduce(
  (accumulator, currentValue) => accumulator + currentValue,
  0
);

console.log(sum); // 15
```

- Each iteration updates the accumulator, and the final accumulator value is returned.
---
Here’s a **tight, condensed summary** of method chaining — clean, clear, and perfect for quick reference:

---

## **Method Chaining**

- Multiple methods called back‑to‑back on the same value.  
- Works on **strings, arrays, objects**, and more.  
- Each method returns a **new value** this.object, new value is the input for the next method.

### **Array Example (filter → map → reduce)**
```js
const transactions = [
  { amount: 100, type: "credit" },
  { amount: 20, type: "cash" },
  { amount: 150, type: "credit" },
  { amount: 50, type: "cash" },
  { amount: 75, type: "credit" }
];

const totalCreditWithBonus = transactions
  .filter((transaction) => transaction.type === "credit")
  .map((transaction) => transaction.amount * 1.1)
  .reduce((sum, amount) => sum + amount, 0);

console.log(totalCreditWithBonus); // 357.5
```
### **Filter items → transform them → combine into one result.**
---

Here’s a **clean, condensed summary** of how the `sort` method works — tight, clear, and perfect for quick reference:

---

## **The `sort` Method**

- **Arranges array elements in place** and returns the **same mutated array**.
- By default, JavaScript **converts elements to strings** and sorts them by **UTF‑16 code order**.
- Great for **strings**, but produces incorrect results for **numbers**.

### **Why Numbers Sort Incorrectly by Default**
```js
const numbers = [414, 200, 5, 10, 3];
numbers.sort();

console.log(numbers); // [10, 200, 3, 414, 5]
```

### **Fix: Use a Compare Function**
```js
const numbers = [414, 200, 5, 10, 3];

numbers.sort((a, b) => a - b);
console.log(numbers); // [3, 5, 10, 200, 414]
```

- The compare function must return:
  - **negative** → `a` comes before `b`
  - **positive** → `a` comes after `b`
  - **zero** → equal order
---
Here’s a **tight, condensed summary** of `every()` and `some()` — clean, clear, and perfect for quick reference:

---

## **`every()` and `some()` Methods**

### **`every()`**
- Checks **ALL elements** in ARRAY pass test/satisfies condition --> Returns **true**. 
- Stops when finds a **false** result.

**Example**
```js
const numbers = [2, 4, 6, 8, 10];
const hasAllEvenNumbers = numbers.every((num) => num % 2 === 0);

console.log(hasAllEvenNumbers); // true
```
---

### **`some()`**
- Checks **IF ONE element** pass test/satisfies conditionn --> Returns **true**. 
- Stops when finds a **true** result.

**Example**
```js
const numbers = [1, 3, 5, 7, 8, 9];
const hasSomeEvenNumbers = numbers.some((num) => num % 2 === 0);

console.log(hasSomeEvenNumbers); // true
```
---

### **`every()` and `some()` Key Points**
- Both methods use a callback with up to three arguments:  
  **element**, **index**, **array**  

---

Here’s a **condensed, clean, classroom‑ready version** of your Higher‑Order Functions review.  
Everything essential is preserved, but the wording is tighter and easier to scan.

---

# **JavaScript Higher‑Order Functions Review**

## **Callback Functions & `forEach`**
- A **callback** a function passed into another function.
- `forEach()` loops through an array and runs a callback on each element.  
  Callback receives: **element**, **index**, **array**.

```js
[1, 2, 3, 4, 5].forEach(n => console.log(n * 2));
```

---

## **Higher‑Order Functions**
- take a function as an argument or returns one.

## **`map()`**
- Creates a **new array** by applying a function to each element.
- Callback receives: **element**, **index**, **array**.

```js
const doubled = [1, 2, 3, 4, 5].map(n => n * 2);
```

## **`filter()`**
- Returns a **new array** of elements that pass a test.

```js
const even = [1,2,3,4,5,6,7,8,9,10].filter(n => n % 2 === 0);
```
## **`reduce()`**
- Reduces an array to a **single value**.
- Reducer receives: **accumulator**, **current value**.

```js
const sum = [1,2,3,4,5].reduce((acc, val) => acc + val, 0);
```
## **Method Chaining**
- Calling multiple methods in sequence on the same value.

```js
const result = "  Hello, World!  "
  .trim()
  .toLowerCase()
  .replace("world", "JavaScript");
```
## **`sort()`**
- Sorts an array **in place**.
- Strings sort by UTF‑16 code units by default.
- Numbers require a compare function.

```js
const fruits = ["Banana", "Orange", "Apple", "Mango"];
fruits.sort();

[414, 200, 5, 10, 3].sort((a, b) => a - b);
```

## **`every()` & `some()`**
- `every()` → returns **true** if *all* elements pass a test.
- `some()` → returns **true** if *at least one* element passes.

```js
[2,4,6].every(n => n % 2 === 0); // true
[1,3,5,8].some(n => n % 2 === 0); // true
```



