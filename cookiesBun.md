```ts
cookies.set("user_id", "12345", {
        maxAge: 60 * 60 * 24 * 7, / 1 week /tempo de vida cookie,funciona em segundos
        httpOnly: true,/  não fica visivel para o js local do browser,ou seja não pode ser acessado pelo lado do cliente,evita <XSS>
        secure: true,/só enviar em requisições https
        path: "/",\rotas que esse cookie é válido
      });

```
