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
  "total": 8,
  "data": [
    {
      "_id": "5772cd66e787dcaf1ae1361d",
      "cliente": {
        "_id": "5772cabce787dcaf1ae1361c",
        "cliente": true,
        "fornecedor": false,
        "nome": "Websix",
        "isentoIcms": false,
        "optanteSimples": false,
        "referencias": [],
        "enderecos": [],
        "dataCadastro": "2016-06-28T19:06:36.537Z",
        "contatos": [],
        "__v": 0,
        "ativo": true
      },
      "codigoCustom": "cc-testes",
      "descricao": "Centro de custo de testes",
      "__v": 0,
      "numerosDestinatarios": [
        9999999999
      ],
      "emailsResponsaveis": [
        {
          "email": "email@email.com",
          "receberRetornos": "true",
          "recebeInvalidos": "true",
        }
      ]
    },
]
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
    {
        "email":"email@email.com",
        "recebeInvalidos": true,
        "recebeRetornos": true
    }
  ],
  "numerosDestinatarios": [
    "99999999599"
  ],
  "codigoCustom": "00014523",
  "descricao": "teste",
  "cliente": {
    "_id": "577a75e5dd2a119027031a9f"
  }
}
```

> Resposta

```javascript
{
  "success": true,//Status da requisição
  "data": {
    "__v": 0,
    "codigoCustom": "00014523",
    "descricao": "teste",
    "cliente": "577a75e5dd2a119027031a9f",
    "_id": "579127a02d86e30e3580b81c",//ID do centro de custo gerado
    "numerosDestinatarios": [
      99999999599
    ],
    "emailsResponsaveis": [
      {
        "email": "email@email.com",
        "recebeInvalidos": "true",
        "recebeRetornos": "true",
        "_id": "579127a02d86e30e3580b81d"
      }
    ]
  },
  "err": null,  //Se o status for false o erro será exibido aqui
  "form": { //Para debugar o que está sendo mandado para API
    "emailsResponsaveis": [
      {
        "email": "email@email.com",
        "recebeInvalidos": true,
        "recebeRetornos": true
      }
    ],
    "numerosDestinatarios": [
      "99999999599"
    ],
    "codigoCustom": "00014523",
    "descricao": "teste",
    "cliente": {
      "_id": "577a75e5dd2a119027031a9f"
    }
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
  {
        "email":"email@email.com",
        "recebeInvalidos": true,
        "recebeRetornos": true
  }
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
  "success": true,//Status da requisição
  "data": {
    "__v": 0,
    "_id": "577ab8e49e155d5732e9b9db", 
    "codigoCustom": "00014523",
    "descricao": "teste",
    "cliente": "577a75e5dd2a119027031a9f",
    "numerosDestinatarios": [
      99999999599
    ],
    "emailsResponsaveis": [
      {
        "email": "email@email.com",
        "recebeInvalidos": "true",
        "recebeRetornos": "true",
        "_id": "579127fd2d86e30e3580b8cf"
      }
    ]
  },
  "err": null, //Se o status for false o erro será exibido aqui
  "form": { //Para debugar o que está sendo mandado para API
    "_id": "577ab8e49e155d5732e9b9db",
    "emailsResponsaveis": [
      {
        "email": "email@email.com",
        "recebeInvalidos": true,
        "recebeRetornos": true
      }
    ],
    "numerosDestinatarios": [
      "99999999599"
    ],
    "codigoCustom": "00014523",
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



---

### Envio avulso

* **Enviar**

```
POST http://v2.bestuse.com.br/api/v1/envioApi/envioAvulso?token=CHAVE_DA_API

```

> Paramêtros


**numero** - (string) Número de telefone para envio.

**validar** - (bool) Define se o número será ou não validado pelo Vertele.

**mensagem** - (string) Mensagem para envio.

**centroCusto** - (string) Identificação do centro de custo.

```javascript
{
  "numero" : "9999999999",
  "validar" : true,
  "mensagem" : "Uma mensagem legal para enviar",
  "centroCusto": "5772cd66e787dcaf1ae1361d",
}
```

> Resposta

```javascript
{
  "success": true,
  "data": {
    "arquivoGerado": "envioAPI/envio_api_2016-07-05 17:38:30:188_Websix.api",
    "smssEnviados": 1,
    "codigoDaOperadora": "55341"
  },
  "msg": "Sms enviado com sucesso"
}
```

```javascript
//em caso de erros

{
  "success": false,
  "data": "",
  "err": "O número é inválido"
}
```