# 08. Implementando a store do zero

```js
<!DOCTYPE html>
<html>
<head>
  <meta charset="utf-8">
  <meta name="viewport" content="width=device-width">
  <title>JS Bin</title>
  <script 
  src="https://cdn.jsdelivr.net/momentjs/2.14.1/moment-with-locales.min.js"></script>
  <script src="https://fb.me/react-0.14.0.js"></script>
  <script src="https://fb.me/react-dom-0.14.0.js"></script>
  <script src="https://cdnjs.cloudflare.com/ajax/libs/redux/3.0.4/redux.js"></script>
</head>
  
<body>
  <div id='root'></div>
</body>
</html>

const counter = (state = 0, action) => {
  switch (action.type) {
    case 'INCREMENT':
      return state + 1;
    case 'DECREMENT':
      return state - 1;
    default:
      return state;
  }
}

const { createStore } = Redux;
const store = createStore(counter);


const Counter = ({
  value,
  onIncrement,
  onDecrement
}) => (
  <div>
    <h1>{value}</h1>
    <button onClick={onIncrement}>+</button>
    <button onClick={onDecrement}>-</button>
  </div>
);

const render = () => {
  ReactDOM.render(
    <Counter
      value={store.getState()}
      onIncrement={() =>
        store.dispatch({
          type: 'INCREMENT'
        })
      }
      onDecrement={() =>
        store.dispatch({
          type: 'DECREMENT'
        })
      }
    />,
    document.getElementById('root')
  );
}

store.subscribe(render);
render();

```