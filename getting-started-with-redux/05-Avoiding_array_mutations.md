# 09. Fugindo das mutações de matrizes

```js
<!DOCTYPE html>
<html>
<script src="https://ajax.googleapis.com/ajax/libs/prototype/1/prototype.js"></script>
<script src="https://ajax.googleapis.com/ajax/libs/scriptaculous/1/scriptaculous.js"></script>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>JS Bin</title>
  <script 
  src="https://cdn.jsdelivr.net/momentjs/2.14.1/moment-with-locales.min.js"></script>
  <script src="https://wzrd.in/standalone/expect"></script>
  <script src="https://wzrd.in/standalone/deep-freeze"></script>
</head>
<body>
  
  
</body>
</html>
  
  
</body>
</html>

const addCounter = (list) => {
  return [...list, 0];
  
};

const removeCounter = (list, index) => {
  return [
    ...list.slice(0, index),
    ...list.slice(index +1)
  ];
};

const incrementCounter = (list, index) => {
  return [
    ...list.slice(0, index),
    list[index] +1,
    ...list.slice(index + 1)
  ];
};

const testAddCounter = () => {
  const listBefore = [];
  const listAfter = [0];
  
  deepFreeze(listBefore);
  
  expect(
    addCounter(listBefore)
    ).toEqual(listAfter);
  
};

const testRemoveCounter = () => {
  const listBefore = [0, 10, 20];
  const listAfter = [0, 20];
  
  deepFreeze(listBefore);

  expect (
    removeCounter(listBefore, 1)
  ).toEqual(listAfter);
};

const testIncrementCounter = () => {
  const listBefore = [0, 10, 20];
  const listAfter = [0, 11, 20];
  
  deepFreeze(listBefore);

  expect (
    incrementCounter(listBefore, 1)
  ).toEqual(listAfter);
};

testAddCounter();
testRemoveCounter();
testIncrementCounter();
console.log('All tests passesd.');
```