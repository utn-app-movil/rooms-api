# 📘 Rooms API — README

A simple REST API to manage rooms and bookings.

---

## 🔗 Base URL

```
http://localhost:5001
```

---

## 📚 Endpoints Overview

- **POST** `/rooms` — Create a new room  
- **GET** `/rooms` — List all rooms  
- **GET** `/rooms/:roomName` — Get details for a specific room  
- **PUT** `/rooms/booking` — Book a room for a user  
- **PUT** `/rooms/unbooking` — Release a room booking  
- **POST** `/users/auth` — Authenticate a user
- **GET** `/users` — List all users

> ℹ️ The examples below use the sample payloads and responses you provided.

---

## 🔐 Authentication

- `POST /users/auth`  
  Authenticate a user with username and password.

### Request

```http
POST /users/auth HTTP/1.1
Content-Type: application/json

{
  "username": "estudiante",
  "password": "123"
}
```

### Response (example)

```json
{
  "responseCode": "SUCESSFUL",
  "message": "Action executed sucessfully."
}
```

---

## 🏗️ Rooms

### 1) Create Room

**POST** `/rooms`

#### Request

```http
POST /rooms HTTP/1.1
Content-Type: application/json

{
  "room": "ZA-100",
  "capacity": 100
}
```

#### Response (example)

```json
{
  "responseCode": "SUCESSFUL",
  "message": "Action executed sucessfully."
}
```

---

### 2) List Rooms

**GET** `/rooms`

#### Response

```json
{
  "data": [
    {
      "room": "CR1-200",
      "capacity": 4,
      "is_busy": false,
      "user": "",
      "date": null
    },
    {
      "room": "CR1-100",
      "capacity": 6,
      "is_busy": false,
      "user": "",
      "date": null
    },
    {
      "room": "ZA-100",
      "capacity": 6,
      "is_busy": false,
      "user": "",
      "date": null
    }
  ],
  "responseCode": "SUCESSFUL",
  "message": "Action executed sucessfully."
}
```

---

### 3) Get Room by Name

**GET** `/rooms/:roomName`

#### Response

```json
{
  "data": {
    "room": "CR1-100",
    "capacity": 6,
    "is_busy": false,
    "user": "",
    "date": null
  },
  "responseCode": "INFO_FOUND",
  "message": "Action executed sucessfully."
}
```

---

### 4) Book a Room

**PUT** `/rooms/booking`

#### Request

```http
PUT /rooms/booking HTTP/1.1
Content-Type: application/json

{
  "room": "ZA-100",
  "username": "ebarahona@utn.ac.cr"
}
```

---

### 5) Unbook a Room

**PUT** `/rooms/unbooking`

#### Request

```http
PUT /rooms/unbooking HTTP/1.1
Content-Type: application/json

{
  "room": "ZA-100"
}
```

---



---

### 6) List Users

**GET** `/users`

> Returns a list of all users with their details.

#### Request

```http
GET /users HTTP/1.1
```

#### Response

```json
{
    "data": [
        {
            "username": "estudiante",
            "password": "123456",
            "name": "Estudiante",
            "isActive": true,
            "lastname": "Representante Estudiantil",
            "email": "estudiante@est.utn.ac.cr"
        },
        {
            "username": "mvillalta",
            "password": "123456",
            "name": "Jose",
            "isActive": true,
            "lastname": "Mora Villal†a",
            "email": "mvillalta@est.utn.ac.cr"
        },
        {
            "username": "maraya",
            "password": "123456",
            "name": "Carlos",
            "isActive": false,
            "lastname": "Mena Araya",
            "email": "maraya@est.utn.ac.cr"
        }
    ],
    "responseCode": "SUCESSFUL",
    "message": "Action executed sucessfully."
}
```


## 🧪 cURL Examples

```bash
curl -X POST http://localhost:5001/rooms   -H "Content-Type: application/json"   -d '{"room":"ZA-100","capacity":100}'

curl http://localhost:5001/rooms

curl http://localhost:5001/rooms/CR1-100

curl -X PUT http://localhost:5001/rooms/booking   -H "Content-Type: application/json"   -d '{"room":"ZA-100","username":"ebarahona@utn.ac.cr"}'

curl -X PUT http://localhost:5001/rooms/unbooking   -H "Content-Type: application/json"   -d '{"room":"ZA-100"}'

curl -X POST http://localhost:5001/users/auth   -H "Content-Type: application/json"   -d '{"username":"estudiante","password":"123"}'
```

---

## 🧱 Data Model (as inferred)

```ts
type Room = {
  room: string;
  capacity: number;
  is_busy: boolean;
  user: string;
  date: string|null;
}

type ApiResponse<T> = {
  data?: T;
  responseCode: "SUCESSFUL" | "INFO_FOUND" | string;
  message: string;
}
```


