**Promisse
```js
Promisse.all( 
await asyncfunction1()
await asyncfunction2()
await asyncfunction3()
await asyncfunction4()
await asyncfunction5()
await asyncfunction6()
```
faz com que todas sejam executadas no mesmo tempo no entanto o tempo de conclusão é da função que mais demorar,isso é bom quando tu precisa de mais perfomace,mas tu perde
controle,não podendo decidir a sequencia,não usando 'all' eles vão ser executados em sequencia
