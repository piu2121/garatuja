
  GIt INIT : inicia o git no projeto,ou cria a pasta”git.” caso não tenha,está pasta é a que gerencia os comandos do git.

Git Add : serve para selecionar quais arquivos foram alterados caso haja, esse comando possui duas variações => GIt Add . :seleciona todos os arquivos
Git ADD “nome do arquivo.js”.

Git Commit -m “mensagem”: serve para adicionar um comentário no arquivo alterado.

**observação sequência obrigatória => Git ADD,Git Commit.**

GIT Push : envia para o repositório selecionado

Git remote add origin :”https:// página do github do repositório“.

Git Push -u Main branch:’Main é o nome da ramificação’,caso não haja ela ela é criada.

**Ramificações são “versões de códigos”.**

Git status:mostra se foi feita alterações no arquivo e em qual branch vocês está.

Git restore :excluir as alterações do arquivo =>Git restore “nome do arquivo”

Git commit -a =>este comando é a junção do git add com o commit.

Git log :mostra o histórico de comitês da branch na qual você esteja

Git diff :mostra a diferença entre o arquivo atual e o hospedado no repositório

Git branch :mostra qual ramificação está

Git checkout :cria uma branch => Git checkout -B ” nome da branch”

Git checkout :muda de branch => Git checkout ” nome da branch”

Git merge :adiciona as diferenças da branch selecionada e adiciona na que você está mexendo. => Git merge “nome da branch”.

Git push origin “nome da branch”: envia para o github.

Git pull origin “ nome da branch” :pega as alterações que foram feitas do arquivo no repositório,esse comando é para quando você já está trabalhando com o arquivo.caso não esteja use git clone

Git clone “https da página do repositório” : pega uma cópia dos arquivos

Git fetch : ele pega todas as branch existentes,e todas as alterações do projeto salvo na sua máquina,basicamente além de pegar branchs ele pega todo o histórico

link do vídeo para conhecimento mais aprofundado => **https://youtu.be/pyM5QLS2h6M?si=TEG_lxIZ6iBSMMmU**
