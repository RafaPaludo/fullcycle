# Uma boa api REST

- Utiliza URIs únicas para serviços e itens que são expostos para esses serviços

- Utiliza todos os verbos HTTP para realizar as operações em seus recursos, incluindo caching

- Provê links relacionais para os recursos exemplificando o que pode ser feito

---

## HAL, Collection + JSON e Siren

- JSON não prevê um padrão de hipermídia para realizar a linkagem

- HAL: Hypermedia Application Language

- Siren

---

## REST: HAL

Este é um tipo específico de JSON que permite a criação de links relacionais para os recursos expostos, ele permite trabalhar no padrão REST adicionando além disso uma riqueza de informações que auxiliam no uso da api.

```json
Media type = application/hal+json
{
    "_links": { // Sempre trás o link atual
        "self": {
            "href": "http://localhost:8080/api/user/rafael",
        }
    },
    "id": "rafael",
    "name": "Rafael Paludo",
    "_embedded": { // Dados de relacionamento
        "family": {
            "_links": {
                "self": {
                    "href": "http://localhost:8080/api/user/bruna"
                }
            },
            "id": "bruna",
            "name": "Bruna Amorim"
        }
    }
}
```

---

## HTTP Method Negotiation

HTTP possui um outro método: OPTIONS. Esse método nos permite informar quais métodos são permitidos ou não em determinado recurso.

```
OPTIONS /api/product HTTP/1.1
Host: localhost:8080
```

Reposta pode ser:

```
HTTP/1.1 200 OK
Allow: GET,POST
```

Caso envie a requisição em outro formato

```
HTTP/1.1 405 Not Allowed
Allow: GET,POST
```

---

## Content Negotiation

O processo de content negotiation é baseado na requisição que o cliente está fazendo para o server. Nesse caso ele solicita o que e como ele quer a resposta. O server então retornará ou não a informação no formato desejado.

**Accept Negotiation**
- Cliente solicita a informação e o tipo de retorno pelo server baseado no media type informado por ordem de prioridade.

```
GET /product
Accept: application/json
```

Resposta pode ser o retorno dos dados ou:

```
HTTP/1.1 406 Not Acceptable
```

---

## Content-Type Negotiation

Atraveś de um content-type no header da request, o servidor consegue verificar se ele irá conseguir processar a informação para retornar a informação desejada.

```
POST /product HTTP/1.1
Accept: application/json
Content-Type: application/json

{
    "name": "Product 1"
}

```

Caso o servidor não aceite o content type, ele poderá retornar:

```
HTTP/1.1 415 Unsupported Media Type
```