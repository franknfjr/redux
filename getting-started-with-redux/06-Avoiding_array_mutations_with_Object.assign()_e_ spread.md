# 10. Fugindo das mutações de matrizes

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

//const toggleTodo = (todo) => {
//  return Object.assign({}, todo, {
//    completed: !todo.completed
//  });
//};

const toggleTodo = (todo) => {
  return {
    ...todo,
      completed: !todo.completed
  };
};

const testToggleTodo = () => {
  const todoBefore = {
    id: 0,
    text: 'Learn Redux',
    completed: false
  };
  
  const todoAfter = {
    id: 0,
    text: 'Learn Redux',
    completed: true
  };
  
  deepFreeze(todoBefore);
  
  expect(toggleTodo(todoBefore)
    ).toEqual(todoAfter);
};

testToggleTodo();
console.log('All tests passed.');
```