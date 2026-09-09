# REST

- Muitos desenvolvedores "já sabem trabalhar com REST"

- Representational state od transfer

- Surgiu em 2000 por Roy Fielding em uma dissertação de doutorado

- Simplicidade

- Stateless

- Cacheável

---

## Níveis de maturidade (RIchardson Maturity Model)

- Nível 0: The Swamp of POX - sem nenhuma padronização

- Nível 1: Utilização de resources
    | Verbo  | URI         | Operação |
    | ------ | ----------- | -------- |
    | GET    | /products/1 | Buscar   |
    | POST   | /product    | Inserir  |
    | PUT    | /products/1 | Alterar  |
    | DELETE | /products/1 | Deletar  |

- Nível 2: Verbos HTTP - utiliza de verdade o que o verbo significa
    | Verbo  | Utilização        |
    | ------ | ----------------- |
    | GET    | Buscar informação |
    | POST   | Inserir           |
    | PUT    | Alterar           |
    | DELETE | Deletar           |

- Nível 3: HATEOAS: Hypermedia as the Engine od Application State - retorna lista de próximos passos que podem ser feitos. No caso abaixo usando os **links**.
    HTTP/1.1 200 OK
    Content-Type: application/vnd.acme.account+json
    Content-Legnth: ...

    {
        "account": {
            "id": "1234",
            "name": "Rafael",
            "links": {
                "deposit": "/account/deposit",
                "withdraw": "/account/withdraw",
                "balance": "/account/balance",
            }
        }
    }