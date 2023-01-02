# Higher-order Functions

## Flattening

Use the `reduce` method in combination with the `concat` method to “flatten” an array of arrays into a single array that has all the elements of the original arrays.

### Solution

```js
console.log(arrays.reduce((flat, arr) => flat.concat(arr)));
```

## Your own loop

Write a higher-order function `loop` that provides something like a `for` loop statement. It takes a value, a test function, an update function, and a body function. Each iteration, it first runs the test function on the current loop value and stops if that returns `false`. Then it calls the body function, giving it the current value. Finally, it calls the update function to create a new value and starts from the beginning.

When defining the function, you can use a regular loop to do the actual looping.

### Solution

```js
function loop (value, test, update, body) {
  for (let i = value; test(i); i = update(i)) {
    body(i);
  }
};

```

## Everything

Analogous to the `some` method, arrays also have an `every` method. This one returns `true` when the given function returns `true` for every element in the array. In a way, `some` is a version of the `||` operator that acts on arrays, and `every` is like the `&&` operator.

Implement `every` as a function that takes an array and a predicate function as parameters. Write two versions, one using a loop and one using the `some` method.

### Solution

```js
function every(array, test) {
  for (const item of array) {
    if (!test(item)) return false;
  }
  return true;
}

function every(array, test) {
  if (array.some(item => !test(item))) return false;
  return true;
}
```

## Dominant writing direction

Write a function that computes the dominant writing direction in a string of text. Remember that each script object has a `direction` property that can be `"ltr"` (left to right), `"rtl"` (right to left), or `"ttb"` (top to bottom).

The dominant direction is the direction of a majority of the characters that have a script associated with them. The `characterScript` and `countBy` functions defined earlier in the chapter are probably useful here.

### Solution

```js
function dominantDirection(text) {
  return countBy(text, char => {
    let script = characterScript(char.codePointAt(0));
    return script ? script.direction : 'none';
  })
  .filter(({name}) => name !== 'none')
  .reduce((max, current) => max.count > current.count ? max : current, 0).name;
}
```
