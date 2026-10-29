# Persistindo Category

Nesse passo, é necessário criar uma conexão com o banco de dados. No caso vamos usar o sqlite3.

Importar o sqlite3 no arquivo server.go

```bash
_ "github.com/mattn/go-sqlite3"
```

Adicionar a conexão com o banco e injetar o category no resolver:

```bash
	db, err := sql.Open("sqlite3", "./data.db")

	if err != nil {
		log.Fatalf("failed to open database: %v", err)
	}

	defer db.Close()


    ....

    srv := handler.New(graph.NewExecutableSchema(graph.Config{Resolvers: &graph.Resolver{
		CategoryDB: categoryDb,
	}}))
```

## Criar tabela no sqlite3

Em um terminal novo, na pasta raiz do projeto, acessar o sqlite3 e criar a tabela "categories"

```bash
sqlite3

create table categories (id string, name, string, description string);
```

## Criar dados no playground

Depois no playground, basta criar um mutation na interface e dar play nela. Irá criar com os dados passados.

```bash
mutation createCategory {
  createCategory(input: { name:"Tecnologia", description:"Cursos de tecnologia"}) {
    id
    name
    description
  }
}
```

## Listar todas categories

Deve-se criar uma função na category.go para listar as categories. 
Depois criar o resolver no schema.
Depois efetuar a query no playground.

```bash
query queryCategories {
  categories {
    id
    name
    description   
  }
}
```