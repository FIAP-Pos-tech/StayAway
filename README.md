# StayAway

Plataforma de Hotelaria e Hospitalidade


## Requisições em Curl

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

