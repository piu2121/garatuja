#criptografia e Assinatura

Ambos geram hash,uma sequencia de caracteres, eles utilizam duas lógicas que dependendo da escolhida a forma de você trabalahr varia

#Simétrica
apenas uma chave,nessa as informações são 'hasheadas',está chave é enviada para o outro lado da conversa para descriptografar,no entanto
fazer isso com segurança é dificil.


#Assimétrica
utiliza duas chaves a mestra fica com aquele que envia o conteudo,junto com o conteudo uma chave pública também é enviada.
no etanto a lógica da ###assimétrica faz que somente a mestre possa criar hash 'válidos',somente ela cria hash autenticados para a pública e visse versa
.Basicamente a pública só consegue ler da privada e a privada da pública.

##Assinatura
Serve como o nome sugere,ela garante a identidade do remetente.se um dado for alterado ele não vai bater com a Assinatura

##criptografia
Tem alguns algoritmos de criptografia que funciona com assinaturas,caso o valor for   interceptado e alterado,
criptografia basicamente a  publica criptografa e a mestre lê
