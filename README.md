# Api Bestuse


##### HTTP REST API
##### Content-Type: application/json

### Centros de Custo

* **Listar**

```
GET http://v2.bestuse.com.br/api/v1/centrocusto?token=CHAVE_DA_API
```

> Paramêtros

Não é necessário passar nenhum paramêtro



> Resposta

```javascript
{
  "total": 1,
  "data": [
    {
      "_id": "5772cd66e787dcaf1ae1361d",
      "cliente": {
        "_id": "5772cabce787dcaf1ae1361c",
        "__v": 0,
      },
      "codigoCustom": "cc-testes",
      "descricao": "Centro de custo de testes",
      "__v": 0,
      "numerosDestinatarios": [
        10000000000
      ],
      "emailsResponsaveis": [
        "teste@teste.com.br"
      ]
    }
  ]
}
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

### Envio em lote


* **Enviar**

```
POST http://v2.bestuse.com.br/api/v1/envioApi?token=CHAVE_DA_API
```

> Paramêtros

**smss** - Array contendo as mensagens a enviar.

    smss.numero - (string) Número de destino da mensagem

    smss.mensagem - (string) Mensagem

**envioImediato** - (bool) Iniciar o envio imediatamente, ignora o agendamento.

**centroCusto** - (string) Identificação do centro de custo.

**agendamento** - Array com os agendamentos.

    agendamento.quantidade - (string) Quantidade em porcentagem do envio.

    agendamento.dataHoraInicio - (string) Data e hora para começar o envio, formato yyyy-mm-dd hh:mm:ss

    agendamento.dataHoraFim - (string) Data e hora para começar o envio, formato yyyy-mm-dd hh:mm:ss


```javascript
{
  "smss":[
       {
          "numero": "4299234180",
          "mensagem": "Sr(a) #NOME#. Aproveite esta oportunidade e resolva suas pendencias educacionais. Ligue 71 3015-5890 ou 31 2534-3001 e Confira excelentes condicoes."
       },
       {
          "numero": "+554299813593",
          "mensagem": "Sr(a) #NOME#. Aproveite esta oportunidade e resolva suas pendencias educacionais. Ligue 71 3015-5890 ou 31 2534-3001 e Confira excelentes condicoes."
       }
   ],
   "envioImediato": false,
   "centroCusto": "5772cd66e787dcaf1ae1361d",
   "agendamento": [
       {
           "quantidade": "100",
           "dataHoraInicio": "2016-07-04 08:00:00",
           "dataHoraFim": "2016-07-04 10:00:00"
       }
   ]
}
```

> Resposta

```javascript
{
 "success": true,
 "data": {
   "smss": [   ],
   "envioImediato": "false",
   "centroCusto": "573243641a1b21c07cd8fbad",
   "agendamento": [],
   "token": "eyJhbGciOiJIUzI1NiJ9.NTc3MmM4YjRhODg4MDAzMTI4ODExM2Qx.IAtPk5LVYarlrWqR0zBMyF9ohGDa3AuTa46AYBREtzA"
 },
 "err": "",
 "msg": "Smss enviados com sucesso"
}
```

```javascript
//em caso de erros

{
 "success": false,
 "data": {
        "smss": [],
        "envioImediato": "false",
        "centroCusto": "573243641a1sb21c07cd8fbad",
        "agendamento": [],
        "token": "eyJhbGciOiJIUzI1NiJ9.NTc3MmM4YjRhODg4MDAzMTI4ODExM2Qx.IAtPk5LVYarlrWqR0zBMyF9ohGDa3AuTa46AYBREtzA"
 },
 "err": "Erro ao enviar.Centro de custo não encontrado"
}
```