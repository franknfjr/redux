# 01. A única árvore de estado imutável

O `primeiro` princípio do Redux (independentemente da complexidade):

**Todo o estado do aplicativo será representado por um objeto JavaScript.**

Todas as alterações e mutações do aplicativo são explícitas. Essas mutações, que incluem os dados e o estado da UI, estão contidas em um único objeto que chamamos de estado(`state`).

Uma vez que todo o estado é representado em um único objeto, podemos acompanhar as mudanças ao longo do tempo

# 02. Descrevendo as mudanças de estado com as ações

O `segundo` princípio do Redux é que a árvore do estado é somente leitura . Sempre que quiser mudar o estado, você precisa enviar uma ação . Uma ação é um objeto JS simples descrevendo a mudança. Assim como o estado é a representação mínima dos dados, a ação é a representação mínima da mudança para esses dados.

O único requisito para uma ação é que ele possui uma propriedade de tipo (convencionalmente uma String).

Por exemplo, em um app contador, existem INCREMENTe DECREMENTações. No caso de um aplicativo ToDo, os componentes da tela não sabem como um item foi adicionado à lista - tudo o que eles sabem é que uma ADD_TODOação foi enviada, com o textconteúdo "hey" e um seqüencial id.

O princípio geral aqui é que o estado é somente leitura e só pode ser modificado por ações de despacho.

# 03. Funções puras e impuras

** Puro: **
```js
    function square(x){
        return x * x;
    }
    function squareAll(items){
        return items.map(square)
    } 
```

** Impuro: **

```js
    function square(x) {
    updateXInDatabase(x);
    return x * x;
    }
    function squareAll(items) {
        for (let i = 0; i < items.length; i++) {
            items[i] = square(items[i]);
        }
    }
```
# 03. A Funções de redução

React introduziu a ideia de que a camada UI é mais previsível quando é descrita como uma função pura do estado da aplicação.

O Redux complementa essa abordagem, exigindo que as mutações do estado em seu aplicativo precisem ser descritas por uma função pura que leva o estado anterior e a ação sendo despachada e retorna o próximo estado do seu aplicativo.

**Dentro de uma aplicação Redux, existe uma função específica que leva o estado anterior e a ação sendo despachada e retorna o próximo estado do aplicativo inteiro.** É importante que a função seja pura (ou seja, o estado que está sendo dado não é modificado) porque ele deve retornar o novo objeto que representa o novo estado do aplicativo.

Mesmo em grandes aplicativos, ainda existe apenas uma única função que calcula o novo estado da aplicação. Não precisa ser lento - se certas partes do estado não mudaram, suas referências podem permanecer como estão. No exemplo do aplicativo ToDo, ao alterar a visibilidade entre "All / Completed / Active", os próprios itens reais não mudaram, então a referência à versão anterior da `todos` matriz é deixada intacta.

Este é o 3º e último princípio do Redux: para descrever as mutações do estado, você deve escrever uma função que leva o estado anterior do aplicativo e a ação que está sendo despachada e retorna o próximo estado do aplicativo. Esta função é chamada de Redutor(`reducers`) .
