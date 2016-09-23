# Api Bestuse


##### HTTP REST API
#### Se o Content-Type não for especificado provalmente sua aplicação não vai funcionar.
##### Content-Type: application/json

> Para gerar seu **token** acesse a plataforma [V2](http://v2.bestuse.com.br) Navegue até **cadastros -> usuários** clique em editar o usuário que deseja fornecer acesso via api, nessa tela vamos ter um campo chamado **Chave da API** e nessa mesma tela o **Cliente ID**

![](./img/chave.png)

> Para fins de testes recomendamos usar o [POSTMAN](https://chrome.google.com/webstore/detail/postman/fhbjgbiflinjbdggehcddcbncdddomop?hl=en). Um aplicativo que roda com o chrome para testar requisições para API, o content type deve sempre ser especificado conforme exemplo:

![](./img/postman.png)

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


**Exemplos**

```javascript
{
  "smss":[
       {
          "numero": "1199999999",
          "mensagem": "Sr(a) Fulano. Aproveite esta oportunidade e resolva suas pendencias educacionais."
       },
       {
          "numero": "+551199999999",
          "mensagem": "Sr(a) Fulano. Aproveite esta oportunidade e resolva suas pendencias educacionais."
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

**ou para envio imediato**


```javascript
{
  "smss":[
       {
          "numero": "4299999999",
          "mensagem": "Sr(a) Fulano. Aproveite esta oportunidade e resolva suas pendencias educacionais. Ligue 70 7070-7070"
       },
       {
          "numero": "1199999999",
          "mensagem": "Sr(a) Marcio. Aproveite esta oportunidade e resolva suas pendencias educacionais. Ligue 70 7070-7070"
       }
   ],
   "envioImediato": true,
   "centroCusto": "5772cd66e787dcaf1ae1361d"
}
```

> Resposta

```javascript
{
 "success": true,
 "data": {
   "totalSmsSalvos": 2,
   "arquivoGerado": "envioAPI/envio_api_LOTES_2016-09-20 10:03:26:200_Websix.api",
   "id": "57e1339ee9158a6211534279" <- id do arquivo gerado
 },
 "err": "",
 "msg": "Lote submetido com sucesso!"
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

**Envio avulso possui uma limitação de 1 request por segundo, se sua demanda é maior que 100 smss opte por usar o [Envio em lote](#envio-em-lote) para um desempenho superior.**

* **Enviar**

```
POST http://v2.bestuse.com.br/api/v1/envioApi/envioAvulso?token=CHAVE_DA_API

```

> Paramêtros


**numero** - (string) Número de telefone para envio.

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
    "id": "57e3d2ded823852aac935fed"
  },
  "err": "null"
  "msg": "Sms enviado com sucesso"
}
```

***O data.id pode ser usado para consultar o relatorio da mensagem enviada usando o metodo [Relatorio de sms de arquivo](#relatorio-de-sms-de-arquivo)***

```javascript
//em caso de erros

{
  "success": false,
  "data": "",
  "err": "O número é inválido"
}
```

### Relatorio de sms de arquivo

* **Solicitar relatório**

```
GET http://v2.bestuse.com.br/api/v1/resumoArquivoApi?arquivo=ID_DO_ARQUIVO&token=CHAVE_DA_API

```

> Resposta

```javascript
[
  {
    "_id": "57dd5a920612f8a14c98734f",
    "mensagem": "Mensagem enviada",
    "numero": "9999999999",
    "dataHoraEnvio": "2016-09-17 12:05:35",
    "status": "ENVIADO"
  },
  {
    "_id": "57dd5a920612f8a14c987350",
    "mensagem": "Mensagem enviada 2",
    "numero": "8888888888",
    "dataHoraEnvio": "2016-09-17 12:05:35",
    "status": "ENVIADO"
  },
  {
    "_id": "57dd5a920612f8a14c98734e",
    "mensagem": "Mensagem enviada 3",
    "numero": "7777777777",
    "dataHoraEnvio": "2016-09-17 12:05:34",
    "status": "ENVIADO"
  },
]
```

```javascript
//em caso de erros

{
  "success": false,
  "err": "Erro ao encontrar arquivo"
}
```

### Retornos (Caixa de entrada)

* **Solicitar relatório**

```
POST http://bestusenew.dev/api/v1/retornos?token=CHAVE_DA_API

```

> Paramêtros

```javascript
{
  "dataInicial": "2016-09-12",
  "dataFinal": "2016-09-14",
  "skip": 0,
  "limit": 50,
  "centroCusto": "579680389a7cc35d62f906a2"
}
```

> Resposta

```javascript
{
  "total": 1,
  "data": [
    {
      "_id": "57d944c9624118816766c27c",
      "data": "2016-09-14T12:38:26.000Z",
      "mensagem": "Pode creditar na conta",
      "numero": "11999939292",
      "sms": "57d18345f12490f22ce96e2c",
      "cliente": "578fb9df4c8d7d6f498227be",
      "arquivo": "57d18345f12490f22ce96b03",
      "__v": 0,
      "centroCusto": "579680389a7cc35d62f906a2",
      "dataHora": "2016-09-14T12:38:26.000Z",
      "sended": true
    }
  ]
}
```