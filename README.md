# StayAway

Plataforma de Hotelaria e Hospitalidade

## Como rodar a aplicação

Executar o seguinte comando a partir da raiz do projeto:

```bash
docker compose up
```

## Vídeo de funcionalidade

https://youtu.be/G-TTvIoELRg


## Requisições

Endereço da coleção de requisições no Postman: https://documenter.getpostman.com/view/28287436/2sA2xnxA7G

## Requisiçõem em Curl

### Serviço de Clientes e Autenticação

POST
register customer
---

Registra novo cliente.

```curl
curl --location 'localhost:8083/api/auth/register/customer' \
--data '{
    "name": "Enrico",
    "email": "enrico@email.com",
    "password": "2024-01-28"
}'
```

POST
login
---

Login na plataforma.

```curl
curl --location 'localhost:8083/api/auth/register/customer' \
--data '{
    "email": "enrico@email.com",
    "password": "2024-01-28"
}'
```

### Serviço de Hóteis

POST
POST hotel
---

Cadastro de hótel.

```curl
curl --location 'localhost:8081/api/hotel' \
--data '{
    "nome" : "hotel-2",
    "endereco" : "Rua Hotel",
    "numero" : "123",
    "cep" : "12345-100",    
    "cidade" : "sao paulo",
    "estado" : "SP",
    "pais" : "Brasil"
}'
```

GET
GET hotels
---

Lista hóteis.

```curl
curl --location 'localhost:8081/api/hotel'

```

POST
POST quarto
---

Cadastro de Quarto.

```curl
curl --location 'localhost:8081/api/quarto/65f5b585b59250215279e3e9' \
--data '{
    "tipo" : "PREMIUM",
    "quantidade" : 5,
    "totalPessoas" : 50
}'
```

GET
GET quartos
---

Lista quartos.

```curl
curl --location 'localhost:8081/api/quarto'
```

DELETE
DEL quarto by id
---

Remove quarto.

```curl
curl --location --request DELETE 'localhost:8081/api/quarto?Id=65f5b75d05b36f6c27fd102b'
```

POST
POST adicional
---

Cadastra adicionais.

```curl
curl --location --request POST 'localhost:8081/api/adicional' \
--data '{
    "tipo" : "ITEM",
    "valor" : 10.9,
    "quantidade" : 3,
    "obs" : "Cerveja Invicta produzida em RP",
    "hotelId" : "65f59af3ee74d63c155fd560"
}'
```

DELETE
DEL adicional
---

Remove cadastro de adicional.

```curl
curl --location --request DELETE 'localhost:8081/api/adicional?id=65f5a52eb59250215279e3d3'
```

POST
POST ListaIdQuantidade
---

```curl
curl --location --request POST 'localhost:8081/api/adicional/lista' \
--data '[
    {
        "id" : "65f5a4f7acdc16345ec7450e",
        "quantidade" : 200
    },
    {
        "id" : "65f5bde3575c6e4045bbc40b",
        "quantidade" : 12
    }
]'
```

GET
GET adicional
---

Lista adicionais.

```curl
curl --location 'localhost:8081/api/adicional'
```


### Serviço de Reserva

POST 
create reservation for client
---

Cria uma reserva com o status em Aberto (OPENED).

```curl
curl --location 'localhost:8083/reservation' \
--data '{
    "clientId": "C005",
    "numberOfguests": 5,
    "checkin": "2024-01-28",
    "checkout": "2024-02-03",
    "hotelId": "H003",
    "bookedRooms": [
        {
            "roomId": "R027",
            "numberOfRooms": 5
        },
        {
            "roomId": "R0028",
            "numberOfRooms": 9
        }
    ]
}'
```

POST
create reservation for maintenence
---

Cria uma reserva com o status em manutenção (MAINTENENCE).

```curl
curl --location 'localhost:8083/reservation/admin/maintenence' \
--data '{
    "userId": "A002",
    "checkin": "2024-03-14",
    "checkout": "2024-03-17",
    "hotelId": "H003",
    "bookedRooms": [
        {
            "roomId": "R005",
            "numberOfRooms": 2
        },
        {
            "roomId": "R006",
            "numberOfRooms": 1
        }
    ]
}'
```

GET
getAll
---

Lista todas as reservas.

```curl
curl --location 'localhost:8083/reservation'
```

GET
getReservationById
---

Retorna uma reserva por Id.

```curl
curl --location 'localhost:8083/reservation/65f4d504cda03a3a6800eb35'
```

PUT
updateReservation
---

Atualiza uma reserva.

```curl

```

PUT
updateAdditional
---

Insere ou atualiza um item adicionam em um reserva.

```curl
curl --location --request PUT 'localhost:8083/reservation/additional/65f5d053a81fe30a551ea630' \
--data '{
    "id": "AD001",
    "quantity": 1
}'
```

DELETE
removeAdditional
---

Remove um item adicional de uma reserva.

```curl
curl --location --globoff --request DELETE 'localhost:8083/reservation/additional/{{reservationId}}/{{additionalId}}'
```

GET
hotel-bookings
---

Retorna uma lista de agendamentos para os quartos de um hótel. Endpoint para fins administrativos.

```curl
curl --location 'localhost:8083/reservation/bookings/admin/hotel-bookings?hotelId=H001&checkInDate=2024-03-14&checkOutDate=2024-03-17'
```

GET
room-bookings
---

Retorna uma lista de agendamentos de apenas um quarto. Endpoint para fins administrativos.

```curl
curl --location 'localhost:8083/reservation/bookings/admin/room-bookings?roomId=R001&checkInDate=2024-03-14&checkOutDate=2024-03-17'
```

GET
booking-calendar
---

Retorna uma lista ordenada por dia com a quantidade de quartos 

```curl
curl --location 'localhost:8083/reservation/bookings/api/booking-calendar?roomId=R001&checkInDate=2024-03-14&checkOutDate=2024-03-17'
```

