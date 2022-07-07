# API de Clientes
[![License: GPL-3.0](https://img.shields.io/badge/License-GPL3-blue.svg)](https://opensource.org/licenses/gpl-3.0.html)
[![Quality Gate Status](https://sonarcloud.io/api/project_badges/measure?project=fga-eps-mds_2021-2-SiGeD-Clients&metric=alert_status)](https://sonarcloud.io/summary/new_code?id=fga-eps-mds_2021-2-SiGeD-Clients)


Essa API faz parte da arquitetura de microsserviços do projeto [`SiGeD`](https://github.com/fga-eps-mds/2021-2-SiGeD-Doc), sua funcionalidade é possibilitar o controle dos dados dos clientes. 

## Como contribuir?

Gostaria de contribuir com nosso projeto? Acesse o nosso [guia de contribuição](https://fga-eps-mds.github.io/2021-2-SiGeD-Doc/contribuicao/) onde são explicados todos os passos.
Caso reste alguma dúvida, você também pode entrar em contato conosco criando uma issue.

## Documentação

A documentação dessa API foi gerada pelo postman e pode ser acessada [nessa url](https://documenter.getpostman.com/view/5363481/UUxwDV7D)

A documentação do projeto pode ser acessada pelo nosso site em https://fga-eps-mds.github.io/2021-2-SiGeD-Doc/.

## Testes

Todas as funções adicionadas nessa API devem ser testadas, o repositório aceita até 20% do total de lihas não testadas. Para rodar os testes nesse repositório deve ser executado o comando:

```bash
docker-compose run api_clients bash -c  "yarn && yarn jest --coverage --forceExit"
```

## Como rodar?

O arquivo .env possui configurações iniciais que podem ser alteradas de acordo com a necessidade. São elas:
 - SECRET: chave para criptografia das senhas.
 - DB_USER: usuário de acesso ao banco de dados.
 - DB_PASS: senha de acesso ao banco de dados.
 - DB_NAME: nome da base de dados.
 - DB_HOST: host da base de dados.
 - USERS_URL: conexão entre a api de usuários e clientes.

Se os servidores mudarem, deve-se colocar o IP os campos CLIENTS_URL e USERS_URL.

Veja o exemplo abaixo:

```
SECRET=chavedesegredo
DB_USER=api_user
DB_PASS=api_password
DB_NAME=clients_database
DB_HOST=db_clients
USERS_URL=backend_users
```

Para rodar a API é preciso usar os seguintes comandos usando o docker:

Crie uma network para os containers da API, caso não exista:

```bash
docker network create siged_backend
```

Suba o container com o comando:

```bash
docker-compose up
```
A API estará rodando na [porta 3002](http://localhost:3002).

## Seeders

Para popular a base de dados (após subir o docker-compose) com dados exemplos use os seguintes comandos:

```bash
docker exec -it backend_clients bash -c "node src/seeders/seedClient.js && node src/seeders/seedFeature.js && node src/seeders/seedLotacao.js"
```

Para resetar o banco use o comando:

```bash
docker-compose rm
```

## Rotas

**GET: `/clients/`**

Para receber os dados dos clientes ativos.

**GET: `/clients/:id`**

Para receber os dados de um cliente específico utilizando o `id`.

**GET: `/clients/newest-four`**

Para receber os dados dos últimos quatro clientes cadastrados.

**GET: `/clients/history:id`**

Para receber o historico de setores de um cliente específico utilizando o `id`.


**GET: `/features/`**

Para receber os dados de todas as características cadastradas.

**POST: `/featuresbyid/`**

Para adicionar novas características à um cliente.

```json
{
    "featuresList": "[ id, id2, ... ]",
}
```

**POST: `/feature/create`**

Para criar uma nova característica.

```json
{
    "name": "Nome da Caractrística",
    "description": "Descrição da Característica",
    "color": "#000000",
}
```

**POST: `/clients/create`**

Para criar um novo cliente, envie os dados nesse formato:

```json
{
    "name": "Nome do Cliente",
    "cpf": "00000000000",
    "email": "cliente@email.com",
    "phone": "999999999",
    "office": "Cargo",
    "policeStation": "Locação",
    "city": "Cidade"
}
```
 
**PUT: `/clients/update/:id`**

Para atualizar os dados do cliente, envie os dados atualizados seguindo o padrão:
 
```json
{
    "name": "Nome do Cliente",
    "cpf": "00000000000",
    "email": "cliente@email.com",
    "phone": "999999999",
    "office": "Cargo Atualizado",
    "policeStation": "Locação Atualizada",
    "city": "Cidade Atualizada"
}
```

**PUT: `/clients/toggleStatus/:id`**

Para desativar ou reativar um cliente pelo `id`.

**PUT: `/feature/update/:id`**

Para atualizar uma característica existente pelo `id`.

```json
{
    "name": "Nome da Caractrística",
    "description": "Descrição da Característica",
    "color": "#000000",
}
```


**DELETE: `/feature/delete/:id`**

Para deletar uma característica pelo `id`.
