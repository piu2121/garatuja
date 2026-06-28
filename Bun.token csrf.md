```ts
const token = Bun.CSRF.generate("my-secret"//palavra chave do token, {
  sessionId: "user-session-id", //id do token
  expiresIn: 60 * 60 * 1000, //tempo em milisegundo
  encoding: "hex", //estilo de hash hex=>hexadecimal
  algorithm: "sha512" /algoritmo de hashusado
});
```
esse token é de verificação  de ação,ele não fica salvo no navegador de forma explicita,ele é enviado somente quando a requisição é feita e tem que 
ser colocado no header,não podendo ser acessado do lado do cliente.já o JWT,mesmo colocando no session da pra pegar.
