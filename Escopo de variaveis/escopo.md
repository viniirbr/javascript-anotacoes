# Escopo de variáveis
O *escopo* de uma variável é a região do código onde ela está definida e é acessível. Variáveis e constantes declaradas com *let* e *const* têm escopo de bloco.

O exemplo abaixo nos mostra duas variáveis *mathSubject* e *histSubject* criadas com escopo global (não estão dentro de nenhum bloco e, portanto, são acessíveis para todo código). A função *iLikeAndIHate* é executada, criando uma nova variável de mesmo nome *mathSubject*, mas que **não tem nenhuma relação com a variável global de mesmo nome criada**. A função também utiliza a variável *histSubject*, que, como não foi criada localmente, é buscada no escopo global. Perceba que, quando executados os *logs* nas últimas linhas, eles retornam os valores globais declarados inicialmente, já que a variável local *mathSubject* pertence apenas ao escopo da função que já terminou sua execução. O mesmo se aplica à variáveis declaradas com *const*.

``` javascript
let mathSubject = 'math';
let histSubject = 'history';

iLikeAndIHate()

function iLikeAndIHate() {
  let mathSubject = 'math (new value)';
 
  console.log(`I like ${mathSubject} and I hate ${histSubject}`); // `I like math (new value) and I hate history`
}

console.log(mathSubject); // 'math'
console.log(histSubject); // 'history'
```