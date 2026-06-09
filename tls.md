## Usar o git bash
|ele é instalado quando tu baixa o o git |            |


# Para criar a chave

 a Chave 1
 VVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVVV
```bash
openssl genpkey -algorithm RSA -out server.key -pkeyopt rsa_keygen_bits:4096

```
certificado do <https> 
```bash

openssl req -new -x509 -key server.key -out server.crt -days 365 -subj '//CN=localhost'

```

# O <PEM>  da chave
```bash
openssl genpkey -algorithm RSA -out key.pem -pkeyopt rsa_keygen_bits:4096

```

```bash
openssl req -new -key key.pem -out server.csr -config san.cnf

```

Tenho qu3en escutar um a um para entender tudo
