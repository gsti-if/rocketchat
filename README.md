## RocketChat funcional por trás do Treafik 2.4 com ICP Edu Ativo
Este projeto pode implementa o RocketChat 4.0.0 +Mongo 4.2 em com Docker-Compose atrás do proxy reverso Traefik, já com as configurações 
do ICP Edu  do campus.

## Estrutura de arquivos e pastas

- docker-compose.yml é o arquivo principal para construção da pilha de serviços. Nesse caso constrói o ambiente RocketChat usando imagens oficias do Rocket e do Mongo.
- ./uploads é o volume (em _bind mount_) montado na própria pasta do projeto que armazena os arquivos de usuário
- mongodb-rocket é o volume nomeado ( montado em /var/lib/docker/volumes) que persiste o banco de dados.

> Importante! Em caso de backup e restauração, para garantir a persistência dos dados, é necessário cuidado especial com os volumes _uploads_ e mongodg-rocket.

## Executando o projeto 
Para rodar o docker-compose.yml e subir uma versão funcional do Rocket Chat é necessário criar o arquivo .env-rocket na raiz do projeto e executar o docker-compose.

### Variáveis Ambiente
O docker-compose chama um arquivo (env_file: env-rocket) que, nesse caso, precisa ser preenchido com as configurações básicas de acesso à plataforma. Por exemplo:

```bash
ADMIN_USERNAME=admin_rocket
ADMIN_PASS=senha_do_adm
ADMIN_EMAIL=mail@example.com

```

> Aparentemente o usuário **admin** é previamente bloqueado na plataforma, portanto é necessário definir um nome de usuário diferente.

### Usando variáveis ambiente para carregar configurações a partir do .ENV
Para personalizar as variáveis precisamos do ID. Conseguimos isso de forma simples, inspecionando elementos da aplicação Web RocketChat, onde o nome da propriedade é esse ID que pode ser, inclusive, usado para sobrescrever as configurações logo no carregamento (execução docker-compose).

```shell
# Configurações SMTP que vão sobrescrever registros feitos pela Web
OVERWRITE_SETTING_SMTP_Protocol=smtps
OVERWRITE_SETTING_SMTP_Host=smtp.gmail.com
OVERWRITE_SETTING_SMTP_Port=465

```
> Os nomes identificadores após OVERWRITE_SETTING_ foram obtidos inspecionando o HTML da aplicação.

### Executando o compose

```bash
docker-compose up -d

rocketchat-prod_mongo_1 is up-to-date
rocketchat-prod_rocketchat_1 is up-to-date
Starting rocketchat-prod_mongo-init-replica_1 ... done


```
A saída dos logs do compose deve chegar em:
```bash


```
