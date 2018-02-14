# 05. Escrevendo um contador com testes

Adicionar a lib `expect`:
`<script src="https://unpkg.com/expect@%3C21/umd/expect.min.js"></script>`

```js
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

expect(
  counter(0, { type: 'INCREMENT' })
).toEqual(1);

expect(
  counter(1, { type: 'INCREMENT' })
).toEqual(2);

expect(
  counter(2, { type: 'DECREMENT' })
).toEqual(1);

expect(
  counter(1, { type: 'DECREMENT' })
).toEqual(0);

expect(
    counter(1, { type: 'SOMETHING_ELSE' })
).toEqual(1);

expect(
  counter(undefined, {})
).toEqual(0);

console.log("test passed!");
```

# 06. Métodos da store: getState(), dispatch()e subscribe()

Adicionar a lib `redux`:
`<script src="https://cdnjs.cloudflare.com/ajax/libs/redux/3.0.4/redux.js"></script>`

A loja(`store`) une os 3 princípios de Redux:

1. Contém o atual objeto do estado da aplicação
2. Permite que você envie ações
3. Quando você o cria, você precisa especificar o redutor que informa como o estado é atualizado com as ações.

Neste exemplo, chamamos createStore com `counter` redutor que gerencia as atualizações de estado.

`store` **tem 3 métodos importantes:**
1. `getState()` recupera o estado atual da loja Redux. Se corremos `console.log(store.getState())` com o código acima, poderíamos obter, 0já que é o estado inicial da nossa aplicação.

2. `dispatch()`é o mais utilizado. É assim que despachamos ações para alterar o estado do aplicativo. Se corremos, `store.dispatch( { type: 'INCREMENT' });` seguiremos por `console.log(store.getState());` nós teremos `1`

3. `subscribe()` registra um retorno de chamada que a loja redux chamará sempre que uma ação foi enviada para que você possa atualizar a UI do seu aplicativo para refletir o estado atual do aplicativo.

```js
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

console.log(store.getState());

store.dispatch({type: 'INCREMENT'});
console.log(store.getState());

const render = () => {
  document.body.innerText = store.getState();
};

store.subscribe(render);
render();

document.addEventListener('click', () => {
  store.dispatch({type: 'INCREMENT'});
});
```