## Usar o git bash
**ele é instalado quando tu baixa o o git **


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

# O <PEM>  da chave
```bash
openssl genpkey -algorithm RSA -out key.pem -pkeyopt rsa_keygen_bits:4096
```
mesmo comando que o primeiro só  muda o tipo de arquivo,agora ele é tipo pem,arquivo de base 64,embora o outro também seja ele é tipado como uma chave

+ **configurações**
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
```bash
openssl req -new -key key.pem -out server.csr -config san.cnf

```
