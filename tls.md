## Usar o git bash
**ele é instalado quando tu baixa o  git**


# Para criar a chave

 a Chave 1
 VVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVV
```bash

openssl genpkey -algorithm RSA -out server.key -pkeyopt rsa_keygen_bits:4096

```

+ **openssl**	É o executável da biblioteca **OpenSSL**. É ela quem faz toda a mágica criptográfica.
+ **genpkey**	Subcomando para gerar uma chave privada (private key). É a forma mais moderna e recomendada (substitui o antigo genrsa).
+ **-algorithm RSA**	Define que o algoritmo usado será o RSA (o mais comum para servidores web/SSL).
+ **-out server.key**	Define o nome do arquivo de saída. O arquivo será salvo na pasta atual onde você está no Git Bash com o nome **server.key.**
+ **-pkeyopt rsa_keygen_bits:4096**	Define o tamanho da chave em 4096 bits. Quanto maior, mais seguro 
 (o padrão antigo era 2048, mas 4096 é excelente para segurança atual).

certificado do **https** 
```bash
openssl req -new -x509 -key server.key -out server.crt -days 365 -subj '//CN=localhost'
```
+ **openssl**	O executável da biblioteca.
+ **req**	Subcomando para gerenciar Certificate Requests (CSR) e certificados.
+ **-new**	Indica que estamos criando um novo certificado (ou uma nova requisição).
+ **-x509**	Faz o OpenSSL gerar um certificado autoassinado no formato X.509 (o padrão mundial para SSL/TLS) em vez de gerar uma requisição (CSR) que precisaria ser enviada a uma Autoridade Certificadora (CA).
+ **-key server.key**	Aponta para o arquivo da chave privada que você gerou no comando anterior. É ela que vai "assinar" digitalmente o certificado.
+ **-out server.crt**	Define o nome do arquivo de saída onde o certificado será salvo (a extensão .crt é padrão para certificados).
+ **-days 365**	Define o prazo de validade: 365 dias (1 ano). Após esse período, o certificado expira e precisa ser renovado.
+ **-subj** '//CN=localhost'	Define o "assunto" (Subject Distinguished Name) do certificado diretamente na linha de comando, sem fazer perguntas interativas (como País, Estado, etc.).

# O PEM  da chave
```bash
openssl genpkey -algorithm RSA -out key.pem -pkeyopt rsa_keygen_bits:4096
```
mesmo comando que o primeiro só  muda o tipo de arquivo,agora ele é tipo pem,arquivo de base 64,embora o outro também seja ele é tipado como uma chave.este 
como um arquivo base64 comum

+ **configurações,arquivo em txt**
```txt
[req]
distinguished_name = req_distinguished_name
req_extensions = req_ext
prompt = no

[req_distinguished_name]
CN = localhost

[req_ext]
subjectAltName = @alt_names

[alt_names]
DNS.1 = localhost
IP.1 = 127.0.0.1

```
+**req**	Seção principal do comando req.
+ **distinguished_name = req_distinguished_name**	Aponta para a seção que contém os dados do "Dono" do certificado.
+ **req_extensions = req_ext**	A chave mais importante aqui! Diz ao OpenSSL para incluir as extensões definidas na seção [req_ext] dentro da CSR.
+ **prompt = no** Desativa o modo interativo. O OpenSSL NÃO vai perguntar "País?", "Estado?", "Organização?". Ele vai ler tudo automaticamente do arquivo.
+ **req_distinguished_name**	Define o Distinguished Name (DN).
+ **CN = localhost**	Define o Common Name como localhost. (Hoje em dia os navegadores ignoram o CN para validação de domínio, mas ainda é bom preencher).
+ **req_ext**	Seção que lista quais extensões serão pedidas no certificado.
+ **subjectAltName = @alt_names**	Puxa a lista de nomes alternativos da seção [alt_names].
+ **alt_names**	A estrela do show (e a salvação contra erros de navegador!).
+ **DNS.1 = localhost**	Define que o certificado é válido para o domínio localhost.
+ **IP.1 = 127.0.0.1**	Define que o certificado também é válido para o endereço IP 127.0.0.1.


**comando para gerar uma requisição,tu manda essa requisição para entidades de assinaturas https para eles assinarem e tua criptografia ter credibildiade**
```bash
openssl req -new -key key.pem -out server.csr -config san.cnf

```
+ **openssl req**	Ferramenta para gerenciar CSR e certificados.
+ **-new**	Cria uma nova CSR.
+ **-key key.pem**	Usa a chave privada key.pem (gerada no passo anterior) para assinar a requisição.
+ **-out server.csr**	Salva a saída no arquivo server.csr. (.csr é a extensão padrão para Certificate Signing Requests).
+ **-config san.cnf**	Força o OpenSSL a usar o seu arquivo san.cnf em vez do arquivo de configuração padrão do sistema (openssl.cnf). Isso é essencial, pois o arquivo padrão geralmente não habilita o envio de SAN pela CSR.

```
openssl x509 -req -in server.csr -signkey key.pem -out server.crt -days 365 -extensions req_ext -extfile san.cnf
```
+ Ele pega a server.csr, assina com a key.pem, gera o server.crt válido por 365 dias.
+ Os parâmetros -extensions req_ext -extfile san.cnf garantem que as extensões SAN que você definiu no arquivo de configuração sejam copiadas para o certificado final.
+ Pronto! Agora você tem key.pem (privada) + server.crt (público com SAN). Ao instalar isso no seu servidor local, o navegador vai confiar em https://localhost e https://127.0.0.1 sem aqueles avisos terríveis (exceto o aviso padrão de "autoassinado", mas você pode clicar em "Avançado" e "Prosseguir" tranquilamente).
