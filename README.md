
Agenda do Pet - Integração API


- Serviços

## Listagem de todos os serviços

`GET`

```json
{
  "data": {
    "business_services": [
      {
        "business_id": 9,
        "business_service_id": 17,
        "service_id": 1,
        "name": "name-test",
        "description": "description-test",
        "photoUrl": "https://url.com/imagem",
        "defaultPrice": "R$ 70,00",
        "promoPrice": "R$ 0,00",
        "bookingLimit": 2,
        "defaultTime": "00:30",
        "defaultLeadtime": "00:10",
        "status": 1,
        "creation": "2024-11-21T21:14:01.000Z",
        "modification": null
      },
      {
        "business_id": 9,
        "business_service_id": 17,
        "service_id": 1,
        "name": "name-test",
        "description": "description-test",
        "photoUrl": "https://url.com/imagem",
        "defaultPrice": "R$ 70,00",
        "promoPrice": "R$ 0,00",
        "bookingLimit": 2,
        "defaultTime": "00:30",
        "defaultLeadtime": "00:10",
        "status": 1,
        "creation": "2024-11-21T21:14:01.000Z",
        "modification": null
      },
    ]
  }
}
```

---

## Criação de um serviço

`POST` 


| Campo | Tipo | Obrigatório | Descrição |
|-------|------|:-------------:|-----------|
| business_id | int | Sim |
| service_id | int | Sim |
| user_id | int | Sim |
| name | string | Sim |
| description | int | Não |
| bookingLimit | int | Não |
| defaultPrice | int | Sim |
| defaultTime | string | Sim | "01:00" = 1 hora, não tem a necessidade dos segundos
| defaultLeadtime | string | Sim | Tempo que leva para ser feito um serviço, exemplo: 40min
| speciesIds | int | Não |
| image | string | Não |


**Exemplo de Corpo de Requisição**

```json
{
  "business_id": 2,
  "service_id": 2,
  "user_id": 1,
  "name": "name-test",
  "description": "description-test",
  "bookingLimit": 3,
  "defaultPrice": 88.88,
  "defaultTime": "01:00",
  "defaultLeadtime": "00:30",
  "species": [
      {
          "specie_id": 1
      },
      {
          "specie_id": 2
      }
  ],
  "image": "data:image/png;base64,....",
  "professionals": [
      {
          "professional_id": 1
      },
      {
          "professional_id": 2
      }
  ],
  "category_id": 2
}
```

---

## Edição de um serviço

`PUT`

| Campo | Tipo | Obrigatório | Descrição |
|-------|------|:-------------:|-----------|
| business_id | int | Sim |
| service_id | int | Sim |
| user_id | int | Sim |
| name | string | Sim |
| description | int | Não |
| bookingLimit | int | Não |
| defaultPrice | int | Sim |
| defaultTime | string | Sim | "01:00" = 1 hora, não tem a necessidade dos segundos
| defaultLeadtime | string | Sim | Tempo que leva para ser feito um serviço, exemplo: 40min
| species | Array | Não |
| specie_id | int | Não |
| image | string | Não |


**Exemplo de Corpo de Requisição**

```json
{
  "business_id": 2,
  "service_id": 2,
  "name": "name-test",
  "description": "description-test",
  "bookingLimit": 3,
  "defaultPrice": 88.88,
  "defaultTime": "01:00",
  "defaultLeadtime": "00:30",
  "image": "data:image/png;base64,....",
  "professionals": [
      {
          "professional_id": 1
      },
      {
          "professional_id": 2
      }
  ],
  "category_id": 2 
}
```

---

## Remoção de um serviço

`DELETE`

| Campo | Tipo | Obrigatório |
|-------|------|:-------------:|
| business_id | int | Sim |


**Exemplo de Corpo de Requisição**

```json
{
  "business_id": 2
}
```


---

- Agendamento

## Listagem de agendamentos de um usuário

`GET`

**Retorno de todos os agendamentos de um usuário**

```json
{
  "data": {
    "bookings": [
      {
        "booking_id": 169,
        "status_id": -2,
        "business_id": 2,
        "uusr_id_for": 2,
        "being_id_from": 2,
        "being_name_from": "Vinicius",
        "user_phoneNumber": "+55 (11) 99999-8888",
        "business_phoneNumber": "+55 (11) 99999-8888",
        "plannedStart": "2025-03-12 17:00",
        "plannedFinish": "2025-03-12 18:30",
        "plannedPrice": "R$ 119,90",
        "bookItems": [
          {
            "booking_item_id": 398,
            "being_id_to": 32,
            "being_name_to": "Fred",
            "professional_id": null,
            "professional_name": null,
            "business_service_id": 1,
            "business_service_name": "Banho e tosa simples de 8 a 15kg",
            "quantity": 1,
            "unitPrice": "R$ 119,90",
            "itemPrice": "R$ 119,90",
            "customerNotes": null,
            "businessNotes": null
          },
        ]
      },
    ]
  }
}
```

---

## Listagem de agendamentos de um negócio/estabelecimento

`GET`

**Retorno de todos os agendamentos de um negócio**

```json
{
  "data": {
    "bookings": [
      {
        "booking_id": 169,
        "status_id": -2,
        "business_id": 2,
        "uusr_id_for": 2,
        "being_id_from": 2,
        "being_name_from": "Vinicius",
        "user_phoneNumber": "+55 (11) 99999-7777",
        "business_phoneNumber": "+55 (11) 99999-8888",
        "plannedStart": "2025-03-12 17:00",
        "plannedFinish": "2025-03-12 18:30",
        "plannedPrice": "R$ 119,90",
        "bookItems": [
          {
            "booking_item_id": 398,
            "being_id_to": 32,
            "being_name_to": "Fred",
            "professional_id": null,
            "professional_name": null,
            "business_service_id": 1,
            "business_service_name": "Banho e tosa simples de 8 a 15kg",
            "quantity": 1,
            "unitPrice": "R$ 119,90",
            "itemPrice": "R$ 119,90",
            "customerNotes": null,
            "businessNotes": null
          },
        ]
      },
    ]
  }
}
```

---

## Criação de um agendamento

`POST`


| Campo | Tipo | Obrigatório | Descrição |
|-------|------|:-------------:|-----------|
| business_id | int | Sim |
| user_id | int | Sim |
| plannedStart | string | Sim |
| plannedFinish | string | Sim |
| booking_items | array | Sim |
| business_service_id | int | Sim |
| business_service_name | string | Sim |
| being_id_from | int | Sim | Id de quem está realizando o agendamento.
| being_name_from | string | Sim |
| being_id_to | int | Sim | Id de quem irá para o agendamento no dia marcado.
| being_name_to | string | Sim |
| quantity | int | Sim |



**Exemplo de Corpo de Requisição**

```json
{
  "business_id": 2,
  "user_id": 3,
  "plannedStart": "2025-03-20 20:00:00",
  "plannedFinish": "2025-03-20 20:00:00",
  "booking_items": [
    {
      "business_service_id": 2,
      "business_service_name": "Tosa",
      "being_id_from": 2,
      "being_name_from": "Vinicius",
      "being_id_to": 32,
      "being_name_to": "Fred",
      "quantity": 5
    },
  ]
}
```


**Retorno de uma criação**

```json
{
  "message": "Agendamento realizado com sucesso",
  "data": {
    "booking_id": 1,
  }
}
```


---

## Cancelamento de um agendamento de usuário

`PATCH`


| Campo | Tipo | Obrigatório | Descrição |
|-------|------|:-------------:|-----------|
| user_id | int | Sim |


**Exemplo de Corpo de Requisição**

```json
{
  "user_id": 11,
}
```

**Retorno**

```json
{
  "message": "Agendamento cancelado com sucesso",
}
```

---

## Cancelamento de um agendamento de negócio/estabelecimento

`PATCH`


| Campo | Tipo | Obrigatório | Descrição |
|-------|------|:-------------:|-----------|
| business_id | int | Sim |


**Exemplo de Corpo de Requisição**

```json
{
  "business_id": 2,
}
```


**Retorno**

```json
{
  "message": "Agendamento cancelado com sucesso",
}
```

---
