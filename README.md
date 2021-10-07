# Mon Petit Bonsai

---
## Operations on Bonsais  
  

### Retrieve all bonsais data
>**GET** /bonsais  

**Response**
```json
[
  {
    "id": "63696432-01a2-4b43-b162-47b4f1e6062a",
    "name": "Pépito",
    "species": "Jade tree",
    "acquisition_date": "10/06/2021",
    "acquisition_age": 25,
    "owner_id": "XXXXXX",
    "last_watering": "20/09/2021",
    "last_repotting":"10/02/2019",
    "last_pruning": "30/04/2021"
  }
]
```

---
  
### Retrieve data on a specific bonsai
>**GET** /bonsais/{id}   
> or   
>**GET** /bonsais/{name}

**Response**
> 200 OK
```json
   {
     "id": "63696432-01a2-4b43-b162-47b4f1e6062a",
     "name": "Pépito",
     "species": "Jade tree",
     "acquisition_date": "10/06/2021",
     "acquisition_age": 25,
     "owner_id": "XXXXXX",
     "last_watering": "20/09/2021",
     "last_repotting":"10/02/2019",
     "last_pruning": "30/04/2021"
   }
   ```
**Resource not found**
> 404  Not found

**Input error**
> 400  Bad request

**The requested bonsai is dead**
> 410  Gone

**The request bonsai has changed name**
> 301 Moved permanently   
> `Location` header sent

---
### Modify information about a bonsai
>**PATCH** /bonsais/{id}

**Response**
> 204 No content

**Resource not found**
> 404 Not found

**Input error**
> 400 Bad request

---
### Delete a bonsai
**DELETE** /bonsais/{id}

**Response**
> 204 No content

**Resource not found**
> 404 Not found

**Input error**
> 400 Bad request

---
### Retrieve information about last bonsai watering
>**GET** /bonsais/{id}/watering

**Response**
> 200 OK
```json
[
  {
    "id": "22dd930c-fe5d-497d-9b60-462f2083541d",
    "datetime": "2022/07/24 18:24:33"
  }
]
```

---
### Retrieve information about last bonsai repotting
>**GET** /bonsais/{id}/repotting  

**Response**
> 200 OK
```json
[
  {
    "id": "22dd930c-fe5d-497d-9b60-462f2083541d",
    "datetime": "2022/07/24 18:24:33"
  }
]
```

---
### Retrieve information about last bonsai pruning
> **GET** /bonsais/{id}/pruning

**Response**
> 200 OK
```json
[
  {
    "id": "22dd930c-fe5d-497d-9b60-462f2083541d",
    "datetime": "2022/07/24 18:24:33"
  }
]
```

---
### Transfer a bonsai from an owner to another

>**POST** /bonsais/{id}/transfer

**Body :** 
```json
{ "newOwnerId": "5c4eb5ad-e825-4444-bbe1-18639330a2a8" }
```

**Response**
```json
{
  "id": "bcb745af-838e-4241-aff4-dc5df67756bb",
  "name": "Pépito",
  "species": "Jade tree",
  "acquisition_date": "10/06/2021",
  "acquisition_age": 25,
  "owner_id": "XXXXXX",
  "last_watering": "20/09/2021",
  "last_repotting":"10/02/2019",
  "last_pruning": "30/04/2021"
}
```
  
---
---
---
---

## Operations on owners

### Get bonsais owners list
> **GET** /owners

**Response**
 ```json
[
  {
    "id": "c95f4c10-a520-4a5c-8a1e-6179eb5cd4e0",
    "name": "Pépito",
    "bonsais": [
      {
        "id": "63696432-01a2-4b43-b162-47b4f1e6062a",
        "name": "Pépito",
        "species": "Jade tree",
        "age": 25
      }
    ]
  }
]
```

---
### Retrieve data on a specific owner
> **GET** /owners/{id}

**Response**
```json
  {
  "id": "c95f4c10-a520-4a5c-8a1e-6179eb5cd4e0",
  "name": "Pépito",
  "bonsais": [
    {
      "id": "63696432-01a2-4b43-b162-47b4f1e6062a",
      "name": "Pépito",
      "species": "Jade tree",
      "age": 25
    }
  ]
}
```

---
### Retrieve bonsais list of a specific owner
> **GET** /owners/{id}/bonsais

**Response**
> 200 OK
```json
[
  {
    "id": "63696432-01a2-4b43-b162-47b4f1e6062a",
    "name": "Pépito",
    "species": "Jade tree",
    "age": 25
  }
]
```
