``` typescript


import todo from "./core.ts";
/* Importa a lógica contida no core.ts,ele estão no mesmo nível por iso não precisa '..'*/
const server = Bun.serve({
  port: 3000,
/* inicia o servidor e insere a porta da aplicação */
  routes: { /*rotas da aplicação*/
    "/": new Response(Bun.file("./public/index.html")),

    "/api/todo": {
      GET: async () => {
        const items = await todo.getItems()
        return Response.json(items)
      },/* rota do metodo get,ela não passa parametro só pega e fecha a canexão*/

      POST: async (req) => {
        const data = await req.json() as any;
        const item = data.item || null;
        if (!item)
          return Response.json('Por favor, forneça um item para adicionar.', { status: 400 });
        await todo.addItem(item);
        return Response.json(data);
      },/* Rota do metodo Post,ele passa parametros e esses parametr4os são salvos na sua aplicação se tu fizer pra ser salvo né*/
    },

    "/api/todo/:index": {
      PUT: async (req) => {
        const index = parseInt(req.params.index);
        if (isNaN(index))
          return Response.json('Índice inválido. um número inteiro é esperado.', { status: 400 });
        const data = await req.json() as any;
        const newItem = data.newItem || null;
        if (!newItem)
          return Response.json('Por favor, forneça um novo item para atualizar.', { status: 400 });
        try {
          await todo.updateItem(index, newItem);
          return Response.json(`Item no índice ${index} atualizado para "${newItem}".`);
        } catch (error: any) {
          return Response.json(error.message, { status: 400 });
        }/* Rota do metodo post, a lógica dessa rota é atualizar o item, e ele verifica sé é um número o índice*/
      },

      DELETE: async (req) => {
        const index = parseInt(req.params.index);
        if (isNaN(index))
          return Response.json('Índice inválido.', { status: 400 });
        try {
          await todo.removeItem(index);
          return Response.json(`Item no índice ${index} removido com sucesso.`);
        } catch (error: any) {
          return Response.json(error.message, { status: 400 });
        }/* rota Delete,deleta algo com base no parametro que essa rota recebe*/
      },
    },

    // EXEMPLO BÁSICO

    "/api/exemplo": {
      GET: () => {
        return new Response(`Esse é o exemplo: ${Date.now()}`)
      },

      POST: async (req) => {
        const data = await req.json() as any;
        data.recebidoEm = new Date().toLocaleDateString("pt-BR");
        return Response.json(data);
      },
    },

    "/api/exemplo/:id": {
      PUT: async (req, params) => {
        const { id } = req.params;
        const data = await req.json() as any;
        data.id = id;
        data.recebidoEm = new Date().toLocaleDateString("pt-BR");
        return Response.json(data);
      },

      PATCH: async (req, params) => {
        const { id } = req.params;
        const data = await req.json() as any;
        data.chavesAtualizadas = Object.keys(data);
        data.id = id;
        data.atualizadoEm = new Date().toLocaleDateString("pt-BR");
        return Response.json(data);
      },

      DELETE: (req, params) => {
        const { id } = req.params;
        return new Response(`Recurso com id ${id} deletado`, { status: 200 });
      }/* metodo delete, passa parametro e deleta no servidor*/
    }
    // FIM DO EXEMPLO BÁSICO
  },

  async fetch(req) {
    return new Response(`Not Found`, { status: 404 });
  },
});

console.log(`Server running at http://localhost:${server.port}`);

```





