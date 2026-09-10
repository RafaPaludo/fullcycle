# GraphQL

É um tipo de comunicação entre sistemas que permite um client solicitar apenas os recursos pontuais que deseja. Por exemplo solicitar nome,id de uma infinidade de propriedades do usuário da API.

Essa abordagem é muito útil principalmente em BFFs ou aplicações com múltiplas APIs, onde o cliente pode solicitar apenas as informações necessárias para a aplicação.

No curso será visto como implementar um GraphQL server usando Go, através da biblioteca [gqlgen](https://gqlgen.com/) no pacote [modulo-graphql](../modulo-graphql/)

## Instalação

Repo com os códigos: https://github.com/devfullcycle/goexpert/tree/main/13-GraphQL

Instalar o Go: https://go.dev/doc/install

Habilitar extensão VSCode: https://marketplace.visualstudio.com/items?itemName=golang.Go

### GraphQL Playground

Seguir passos de instalação do https://gqlgen.com/ ou:

> Criar arquivos iniciais
```bash
mkdir example
cd example
go mod init example
```

> Instalar as dependências
```bash
go get -tool github.com/99designs/gqlgen
```

> Inicializar o projeto
```bash
go tool gqlgen init
```

> Rodar o servidor
```bash
go run server.go
```

### Criando Schema próprio

Ao invés de usar os dados do próprio projeto, será criado um schema prórpio. Para isso foi mudado o arquivo padrão [schema.graphqls](../modulo-graphql/graph/schema.graphqls).

Habilitar extensão GraphQL do VSCode: https://marketplace.visualstudio.com/items?itemName=GraphQL.vscode-graphql

Após alterar o schema, rodar o comando de geração dos arquivos:

```graphql
type Category {
  id: ID!
  name: String!
  description: String
  courses: [Course!]!
}

type Course {
  id: ID!
  name: String!
  description: String
  category: Category!
}

input NewCategory {
  name: String!
  description: String
}

input NewCourse {
  name: String!
  description: String
  categoryId: ID!
}

type Query {
  categories: [Category!]!
  courses: [Course!]!
}

type Mutation {
  createCategory(input: NewCategory!): Category!
  createCourse(input: NewCourse!): Course!
}
```

```bash
go tool gqlgen generate
```

### Testando playground

Rodar a aplicação na porta 8080 irá mostrar um playground.

```bash
go run tools server.go
```

Nele será possível ver Docs > query:Query > Fields {categories | courses}
Na aba de teste, podemos executar uma consulta de query para verificar o retorno, nesse momento irá dar erro, mas já está funcionando até aqui.

```graphql
query queryCategories {
  categories {
    id
    name
    description
  }
}
```

### Criando Resolver para Category

Nesse passo será criado um resolver para a categoria. Basicamente é criar o arquivo [category.go](../modulo-graphql/internal/database/category.go) e nele criar funções para inserir uma nova categoria no banco de dados.

É necessário importar o resolver criado em [resolver.go](../modulo-graphql/graph/resolver.go)

Após criar esse resolver, é necessário usá-lo dentro de [schema.resolvers.go](../modulo-graphql/graph/schema.resolvers.go) e alterar CreateCategory para usar esse resolver que acabamos de criar.
