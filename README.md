# Api Bestuse

##### HTTP REST API
##### Content-Type: application/json

### Centros de Custo

* **Listar**

```
GET http://v2.bestuse.com.br/api/v1/centrocusto?token=CHAVE_DA_API
```

---

* **Criar**

```
POST http://v2.bestuse.com.br/api/v1/centrocusto?token=CHAVE_DA_API
```

> Paramêtros

```javascript
{
  "emailsResponsaveis": [
    "email@email.com"
  ],
  "numerosDestinatarios": [
    "9999999999"
  ],
  "codigoCustom": "000123",
  "descricao": "teste",
  "cliente": {
  	"_id": "577a75e5dd2a119027031a9f"
  }
}
```

> Resposta

```javascript
{
  "success": true, //Status da requisição
  "data": {
    "__v": 0,
    "cliente": "577a75e5dd2a119027031a9f",
    "codigoCustom": "000123",
    "descricao": "teste",
    "_id": "577ab26b9e155d5732e9b9da", //ID do centro de custo gerado
    "numerosDestinatarios": [
      9999999999
    ],
    "emailsResponsaveis": [
      "email@email.com"
    ]
  },
  "err": null, //Se o status for false o erro será exibido aqui
  "form": { //Para debugar o que está sendo mandado para API
    "emailsResponsaveis": [
      "email@email.com"
    ],
    "numerosDestinatarios": [
      "9999999999"
    ],
    "codigoCustom": "000123",
    "descricao": "teste"
  }
}
```

---

* **Alterar**

```
PUT http://v2.bestuse.com.br/api/v1/centrocusto?token=CHAVE_DA_API
```

> Paramêtros

```javascript
{
  "_id": "577ab8e49e155d5732e9b9db",
  "emailsResponsaveis": [
    "email@email.com"
  ],
  "numerosDestinatarios": [
    "9999999999",
    "9999999999"
  ],
  "codigoCustom": "000123",
  "descricao": "teste",
  "cliente": {
  	"_id": "577a75e5dd2a119027031a9f" //o cliente._id é pego na resposta de uma criação ou listagem dos centros de custo
  }
}
```


> Resposta

```javascript
{
  "success": true, //Status da requisição
  "data": {
    "ok": 1,
    "nModified": 1,
    "n": 1
  },
  "err": null, //Se o status for false o erro será exibido aqui
  "form": {  //Para debugar o que está sendo mandado para API
    "_id": "577ab8e49e155d5732e9b9db",
    "emailsResponsaveis": [
      "email@email.com"
    ],
    "numerosDestinatarios": [
      "9999999999",
      "9999999999"
    ],
    "codigoCustom": "000123",
    "descricao": "teste",
    "cliente": {
      "_id": "577a75e5dd2a119027031a9f"
    }
  }
}
```

---


