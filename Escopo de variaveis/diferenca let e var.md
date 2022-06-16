# Diferenças entre *let* e *var*

Antes do [ES6](https://kenzie.com.br/blog/ecmascript-6/), era possível declarar variáveis apenas com o *var*. Com essa nova  atualização do JavaScript, surgiu o *let* e possibilidade de delcarar constantes com *const*. Apesar das sintaxes parecidas, há diferenças importantes entre *var* e *let*.

- Enquanto variáveis do tipo *let* e *const* têm escopo de bloco, variáveis declaradas com *var* tem escopo na função inteira em que ela está contida. Vamos ver um exemplo:
```javascript
function testScope() {

    {
        var functionScope = 10;
        let blockScope = 5;
        
        {
            console.log(functionScope);
            console.log(blockScope);
        }
        
    }
    
    console.log(functionScope)
    console.log(blockScope);

}

testScope();
//saída:
// 10
// 5
// 10
// Uncaught ReferenceError: blockScope is not defined
```
Perceba que as variáveis *functionScope* e *blockScope* são acessíveis para blocos internos ao bloco em que estão definidas. Mas, fora desse bloco, apenas a *functionScope* está definida, já que o escopo de uma *var* é toda a função. O erro retornado afirma que a variável *blockScope* não foi definida, o que faz sentido, já que não a definimos no escopo da função *testScope* e sim em um bloco interno a ela.

-  Uma variável **global** criada com *var* se torna uma propriedade do objeto global. Ou seja, dando um `console.log(this)`, você pode verificar ela dentre as inúmeras propriedades e métodos disponíveis e pode acessá-la com `this.[variável]`, embora não seja necessário o *this* já que as propriedades do objeto global já estão implícitas. Exemplo:

```javascript
var test = 5;

console.log(this); // ...test: 5,....

console.log(this.test) // 5
```

Variáveis criadas com *let* e *const* não são propriedades do objeto global.

- Diferente de *let*, que retorna um erro, uma variável *var* pode ser redeclarada diversas vezes.

- ***Hoisting***: Quando uma variável *var* é declarada ela é levada para o topo do seu escopo sem a atribuição de valor. Assim, se a linha que acessa a mesma estiver antes de sua declaração, o programa não retornará erro, mas a variável ainda não terá valor definido, o que pode causar confusão. Esse conceito de levar as variáveis para o topo do código se chama ***hoisting*** (elevação, içamento). O *hoisting* não acontece com variáveis declaradas com *const* e *let*, e o programa retorna erro se elas forem acessadas antes da declaração. Veja o exemplo:
```javascript
console.log(test); // saída: undefined
var test = 10;
```
Com o *hoisting*, é como se o programa tivesse escrito como
```javascript
var test;
console.log(test); // saída: undefined
test = 10;
```
Se declarássemos a variável *test* como *let*, o programa retornaria o erro
*Uncaught ReferenceError: Cannot access 'test' before initialization* 