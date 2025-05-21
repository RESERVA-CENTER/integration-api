
Agenda do Pet - Integração API


- Serviços

---

Todas as rotas precisam de um token para funcionar e para enviar esse token, basta enviar ele na parte Authorization, e em sequência em Bearer Token.
Qualquer dúvida, entre em contato.

---

## Autenticação

`POST` https://devapi.reserva.software/auth/users/login

| Campo | Tipo | Obrigatório | Descrição |
|-------|------|:-------------:|-----------|
| email | string | Sim |
| password | string | Sim |

**Exemplo de Corpo de Requisição**

```json
{
  "email": "test@mail.com",
  "password": "123456"
}
```

**Retornoo**

```json
{
  "status": true,
  "token": "aaa...aaaa",
  "refreshToken": "aaa...aaaa",
  "data": {
      "user": {
          "user_id": 4,
          "name": "test",
          "email": "test@mail.com"
      }
  }
}
```

Nesse caso, eu vou enviar de volta dois tokens.
O token, ele serve para ser usado nas rotas, porém esse token tem um tempo x de duração, após esse tempo ele expira e ele se torna inválido.
**Por favor guarde de forma segura o refresh token.**
Para conseguir um token novo, existe duas maneiras.

A recomendada é utilizar a rota abaixo, para conseguir um token novo válido.

A segunda forma, seria logando novamente na conta de vocês que gerará um novo token e refresh token.

`POST` https://devapi.reserva.software/auth/refresh

| Campo | Tipo | Obrigatório | Descrição |
|-------|------|:-------------:|-----------|
| refresh_token | string | Sim |


**Exemplo de Corpo de Requisição**

Apenas precisa enviar o refresh token no body através do 'x-www-form-urlencoded'

| Key | Value |
|-------|------|
| refresh_token | aaa....aaaa |

O retorno devolve um novo token para refresh e um novo token para uso, **Por favor guarde de forma segura o refresh token.**

**Retornoo**

```json
{
    "token": "aaa..aaa",
    "refreshToken": "aaa...aaa"
}
```

---

## Listagem de todos os negocios

`GET` https://devapi.reserva.software/v1/business

```json
{
    "message": "Empresas retornadas com sucesso",
    "data": {
        "business": [
            {
                "business_id": 1,
                "business_uuid": "860615f7-3655-11f0-bd93-0ec389958a21",
                "being_id": 9,
                "name": "Pet Shop Casa Branca",
                "description": "Aqui no Petshop Casa Branca cuidamos de cada animal como se fosse um dos nossos",
                "shortcut": "Pet Casa Branca",
                "iconUrl": "iconURL",
                "latitude": "-23.71508221",
                "longitude": "-46.66851734",
                "evaluations": 0
            },
            {
                "business_id": 2,
                "business_uuid": "86061ce8-3655-11f0-bd93-0ec389958a21",
                "being_id": 10,
                "name": "Pet Maison Wow",
                "description": "Pet Maison Wow é sensacional!",
                "shortcut": "Pet Maison Wow",
                "iconUrl": "iconURL",
                "latitude": "-23.51508221",
                "longitude": "-46.46851734",
                "evaluations": 0
            }
    ]
  }
}
```

---

---

## Listagem de um negócio

`GET` https://devapi.reserva.software/v1/business/{business_id}

```json
{
    "message": "Empresas retornada com sucesso",
    "data": {
        "business": {
            "business_id": 1,
            "business_uuid": "860615f7-3655-11f0-bd93-0ec389958a21",
            "being_id": 9,
            "name": "Pet Shop Casa Branca",
            "description": "Aqui no Petshop Casa Branca cuidamos de cada animal como se fosse um dos nossos",
            "shortcut": "Pet Casa Branca",
            "iconUrl": "iconURL",
            "latitude": "-23.71508221",
            "longitude": "-46.66851734",
            "evaluations": 0
        }
    }
}
```

---

## Listagem de todos os serviços

`GET` https://devapi.reserva.software/v1/business/{business_id}/business-services

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
        "business_service_id": 18,
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

`POST` https://devapi.reserva.software/v1/business/{business_id}/business-services


| Campo | Tipo | Obrigatório | Descrição |
|-------|------|:-------------:|-----------|
| business_id | int | Sim | Id do estabelecimento |
| service_id | int | Sim | Id de um serviço base, como Banho, Tosa |
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

`PUT` https://devapi.reserva.software/v1/business/{business_id}/business-services/{business_service_id}

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

`GET` https://devapi.reserva.software/v1/users/{user_id}/bookings

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

`GET` https://devapi.reserva.software/v1/business/{business_id}/bookings

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

- Agendamento

## Listagem de um agendamento especifico

`GET` https://devapi.reserva.software/v1/bookings/{booking_id}

**Retorno de um agendamento**

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

## Criação de um agendamento

`POST` https://devapi.reserva.software/v1/bookings


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
    "user_id": 123,
    "plannedStart": "2025-02-21 13:00:00",
    "plannedFinish": "2025-02-21 13:30:00",
    "booking_items": [
        {
            "business_service_id": 1,
            "business_service_name": "Banho",
            "being_id_from": 2,
            "being_name_from": "Vinicius",
            "being_id_to": 2,
            "being_name_to": "Fred",
            "quantity": 2
        },
        {
            "business_service_id": 1,
            "business_service_name": "Banho",
            "being_id_from": 2,
            "being_name_from": "Vinicius",
            "being_id_to": 2,
            "being_name_to": "Fred",
            "quantity": 2
        }
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

## Reagendamento de um agendamento de usuário

Para reagendar um agendamento, basta passar o id do agendamento.

`PATCH` https://devapi.reserva.software/v1/bookings/{booking_id}/rescheduleUserBooking
 
| Campo | Tipo | Obrigatório | Descrição |
|-------|------|:-------------:|-----------|
| plannedStart | String | Sim |
| plannedFinish | String | Sim |
| user_id | int | Sim | Por que o user_id? O motivo é, se o usuario dvjpet que possui o id 123, fez um agendamento, apenas ele com o user_id pode remarcar ou cancelar o agendamento dele. |

**Exemplo de Corpo de Requisição**

```json
{
    "user_id": 122,
    "plannedStart": "2025-02-22 13:00",
    "plannedFinish": "2025-02-22 15:00"
}

```
 
**Retorno**

```json
{
  "message": "Agendamento cancelado com sucesso",
}
 

```

---

## Cancelamento de um agendamento de usuário

Para cancelar um agendamento, basta passar o id do agendamento.

`PATCH` https://devapi.reserva.software/v1/bookings/{booking_id}/cancelUserBooking

| Campo | Tipo | Obrigatório | Descrição |
|-------|------|:-------------:|-----------|
| user_id | int | Sim | Por que o user_id? O motivo é, se o usuario dvjpet que possui o id 123, fez um agendamento, apenas ele com o user_id pode remarcar ou cancelar o agendamento dele. |
 

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
 
`PATCH` https://devapi.reserva.software/v1/bookings/{booking_id}/cancelBusinessBooking

| Campo | Tipo | Obrigatório | Descrição |
|-------|------|:-------------:|-----------|
| business_id | int | Sim | Por que o business_id? O motivo é, se o estabelecimento dvjpet que possui o id 123, e um usuário qualquer, vamos supor o user_id 1 e o user_2 fez um agendamento para o estabelecimento dvjpet, caso por algum imprevisto esse estabelecimenti não consiga atender, ele pode cancelar.


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
 

