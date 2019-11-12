# JSON Server

[GitHub](https://github.com/typicode/json-server)

[Simulando uma API REST com JSON Server de maneira simples](http://www.fabricadecodigo.com/json-server/)

## Passo a passo para simular uma API

1. [Começando com JSON Server](#comeando-com-json-server)
2. [Rotas](#rotas)
3. [Filtros](#filtros)
4. [Paginação](#paginao)
5. [Ordenação](#ordenao)

## Começando com JSON Server

### Instalação

    `npm install -g json-server`

### Criando o arquivo de banco de dados

Crie um arquivo de nome **db.json** na pasta do projeto.
    
> Exemplo:
```json
    {
      "produtos": [
        {
          "id": 1,
          "nome": "Hambúrguer",
          "descricao": "Pão, bife de hambúrguer 90g, salada e batata.",
          "preco": 8.5,
          "categoria_id": 1
        },
        {
          "id": 2,
          "nome": "X-Búrguer",
          "descricao": "Pão, bife de hambúrguer 90g, 1 fatia de queijo, salada e batata.",
          "preco": 10.5,
          "categoria_id": 1
        },
        {
          "id": 3,
          "nome": "X-Bacon",
          "descricao": "Pão, bife de hambúrguer 90g, 1 fatia de queijo, 2 fatia de bacon, salada e batata.",
          "preco": 12.5,
          "categoria_id": 1
        },
        {
          "id": 4,
          "nome": "X-Tudo",
          "descricao": "Pão, 2 bifes de hambúrguer 90g, 2 fatias de queijo, 4 fatias de bacon, salada e batata.",
          "preco": 14.5,
          "categoria_id": 1
        },
        {
          "id": 5,
          "nome": "Coca cola 350ml",
          "descricao": "",
          "preco": 5.5,
          "categoria_id": 2
        },
        {
          "id": 6,
          "nome": "Coca cola 600ml",
          "descricao": "",
          "preco": 7.5,
          "categoria_id": 2
        }
      ],
      "categorias": [
        {
          "id": 1,
          "nome": "Hambúrgueres"
        },
        {
          "id": 2,
          "nome": "Refrigerantes"
        }
      ]
    }
```
  
### Iniciando o servidor

Agora é só rodar o comando abaixo e seu servidor estará iniciado.
Lembrando que, por padrão, a API vai funcionar no endereço [http://localhost:3000](http://localhost:3000).

    `json-server --watch db.json`
    
    `json-server --watch db.json --port 3004`
    
## Rotas

As rotas definem como você vai acessar a API.

### As rotas são:

| Request | URL         | Detalhes                            |
|:------- | ----------- | -----------------------------------:|
| GET     | /produtos   | Busca todos os produtos             |
| GET     | /produtos/1 | Busca um produto                    |
| POST    | /produtos   | Salva um produto                    |
| PUT     | /produtos/1 | Atualiza os dados do produto        |
| PATCH   | /produtos/1 | Atualiza parte dos dados do produto |
| DELETE  | /produtos/1 | Remove um produto                   |

As rotas serão compostas pelo endereço base (localhost:3000) mais o recurso que você quer acessar, como por exemplo "produtos".

Para executar os requests de exemplo abaixo, você pode usar o **[Postman](https://www.getpostman.com/)** ou alguma outra de sua preferência.

> Exemplos:

1. Buscar todos os produtos
    ```http request
    GET http://localhost:3000/protudos/
    Content-Type: application/json
    ```

2. Buscar apenas um produto
    ```http request
    GET http://localhost:3000/produtos/1
    Content-Type: application/json
    ```

3. Salvar um produto
    ```http request
    POST http://localhost:3000/produtos/
    Content-Type: application/json
   
    {
        "nome": "Hambúrguer de frango",
        "descricao": "Pão, bife de hambúrguer 90g de frango, salada e batata.",
        "preco": 9.5,
        "categoria_id": 1
    }
    ```
   
4. Altera um produto
    ```http request
    PUT http://localhost:3000/produtos/1
    Content-Type: application/json
    
   {
        "nome": "Hambúrguer de frango",
        "descricao": "Pão, bife de hambúrguer 90g de frango, salada e batata.",
        "preco": 10.5,
        "categoria_id": 1
    }
    ```
   
5. Alterar apenas o nome de um produto
    ```http request
    PATCH http://localhost:3000/produtos/1
    Content-Type: application/json
    
   {
        "nome": "Hambúrguer de frango artezanal"
    }
    ```
   
6. Excluir um produto
    ```http request
    DELETE http://localhost:3000/produtos/1
    Content-Type: application/json
    ```
   
## Filtros

Para executar filtros é bem simples, você só precisa usar o nome das propriedades do objeto que você quer pesquisar.

No exemplo abaixo, estou pesquisando por produtos que o nome é "X-Burguer"

```http request
GET http://localhost:3000/produtos?nome=X-Burguer
Content-Type: application/json
```

## Paginação

Para efetuar a paginação, você vai usar o parâmetro `_page` e, por padrão, cada página terá 10 itens.
Se você quiser alterar a quantidade de itens que é retornada por página, basta usar o parâmetro `_limit`.

No exemplo abaixo, vou buscar a página 1 e quero 2 itens por página.

```http request
GET http://localhost:3000/produtos/?_page=1&_limit=2
Content-Type: application/json
```

## Ordenação

Para ordenar os dados, você pode usar os parâmetros `_sort` para informação qual campo vai sofrer a ordenação e `_order` para definir se é ascendente ou descendente.
Lembrando que é possível ordenar por mais de um campo.

No exemplo abaixo, vou ordenar os produtos por nome e em ordem descendente.

```http request
GET http://localhost:3000/produtos/?_sort=nome&amp;_order=desc
Content-Type: application/json
```