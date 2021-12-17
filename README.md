# Mon Petit Bonsai

---
## Operations on Bonsais  
  

### Retrieve all bonsais data
>**GET** /bonsais  

**Parameters**

Name|Type| In |Description
----|----|----|-----------
status|string|query|Filter the bonsais by status. Can be ```alive```, ```unknown``` or ```dead```
older_than|string|query|Only return bonsais which age is greater than
sort|string|query|The field to sort the result by. Can be either ```status```, ```age``` (```last_watering```, ```last_repotting```, ```last_pruning```: optional)
direction|string|query|Sort direction. Can only be ```asc``` or ```desc```. Default is ```desc```

**Response**
```json
[
  {
    "id": "63696432-01a2-4b43-b162-47b4f1e6062a",
    "name": "Pépito",
    "species": "Jade tree",
    "acquisition_date": "10-06-2021",
    "acquisition_age": 25,
    "owner_id": "XXXXXX",
    "last_watering": "20-09-2021",
    "last_repotting":"10-02-2019",
    "last_pruning": "30-04-2021",
    "status": "alive"
  }
]
```

---
### Create a bonsai

>**POST** /bonsais

**Body:**
```json
  {
  "name": "Pépito",
  "species": "Jade tree",
  "acquisition_date": "10-06-2021",
  "acquisition_age": 25,
  "owner_id": "6d009e8f-a55f-4ca0-9ef9-5ff6f79478fb"
}

```

**Parameters**

Name|Type| In |Description
----|----|----|-----------
name|string|body|**Required.** Name of the bonsai to create
species|string|body| Species of the bonsai
acquisition_date|string|body| Date of acquisition
acquisition_age|string|body| Age of the bonsai when it was bought
owner_id|string|body| Id of the owner

**Response**
> 201 Created  
> Location header sent
```json
[
  {
    "id": "63696432-01a2-4b43-b162-47b4f1e6062a",
    "name": "Pépito",
    "species": "Jade tree",
    "acquisition_date": "10-06-2021",
    "acquisition_age": 25,
    "owner_id": "6d009e8f-a55f-4ca0-9ef9-5ff6f79478fb",
    "last_watering": "20/09/2021",
    "last_repotting":"10/02/2019",
    "last_pruning": "30/04/2021",
    "status": "alive"
  }
]
```

---
  
### Retrieve data on a specific bonsai
>**GET** /bonsais/{id}  

or  
>**GET** /bonsais/{name}

**Response**
> 200 OK
```json
   {
     "id": "63696432-01a2-4b43-b162-47b4f1e6062a",
     "name": "Pépito",
     "species": "Jade tree",
     "acquisition_date": "10-06-2021",
     "acquisition_age": 25,
     "owner_id": "6d009e8f-a55f-4ca0-9ef9-5ff6f79478fb",
     "last_watering": "20-09-2021",
     "last_repotting":"10-02-2019",
     "last_pruning": "30-04-2021"
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

```json
  {
  "name": "Pépito",
  "species": "Jade tree",
  "acquisition_date": "10-06-2021",
  "acquisition_age": 25,
}

```

**Parameters**

Name|Type| In |Description
----|----|----|-----------
name|string|body| Name of the bonsai to create
species|string|body| Species of the bonsai
acquisition_date|string|body| Date of acquisition
acquisition_age|string|body| Age of the bonsai when it was bought

**Response**
> 200 OK

```json
   {
     "id": "63696432-01a2-4b43-b162-47b4f1e6062a",
     "name": "Pépito",
     "species": "Jade tree",
     "acquisition_date": "10-06-2021",
     "acquisition_age": 25,
     "owner_id": "6d009e8f-a55f-4ca0-9ef9-5ff6f79478fb",
     "last_watering": "20-09-2021",
     "last_repotting":"10-02-2019",
     "last_pruning": "30-04-2021"
   }
   ```

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
### Change the status of a bonsai (dead or alive)
>**PUT** /bonsais/{id}/status

**Body :**
```json
{"status": "dead"}
```

**Parameters**

Name|Type| In |Description
----|----|----|-----------
status|string|body|**Required.** Allowed statuses are ```dead```, ```alive``` and```unknown```

Response
> 204 No content

Resource not found
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
    "datetime": "2022-07-24 18:24:33"
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
    "datetime": "2022-07-24 18:24:33"
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
    "datetime": "2022-07-24 18:24:33"
  }
]
```
  
---
---
---
---

## Operations on owners

### Get bonsais owners list
> **GET** /owners

**Parameters**

Name|Type| In |Description
----|----|----|-----------
has_more|integer|body|Returns the owner who have more or the same number of bonsais than this parameter


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

**Resource not found**
> 404  Not found

---
### Create an owner
>**POST** /owners

**Body :**
```json
{
  "name": "Pépito",
}
```

**Response**
> 201 Created  
> ```Location``` header sent

```json
{
  "id": "3af50eed-c674-41fc-b7a6-5d0667a4c1fa",
  "name": "Jean-Hugues",
  "bonsais": [
  ]
}
```

Name|Type| In |Description
----|----|----|-----------
name|string|body|**Required.** The name of the owner.
bonsais|array of objects|body|The bonsais of the future owner. Can be an empty array or omitted.

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
    "acquisition_age": 25
  }
]
```

**Resource not found**
> 404  Not found

---
### Transfer a bonsai to an owner

>**POST** /owner/{owner_id}/bonsais/{bonsai_id}/transfer

**Body :**
```json
{ "owner_id": "5c4eb5ad-e825-4444-bbe1-18639330a2a8" }
```

Name|Type| In |Description
----|----|----|-----------
owner_id|string|path|The id of the current owner
bonsai_id|string|path|The id of the bonsai to transfer
new_owner|string|body|**Required** The id of the new owner

**Response :**
```json
{
  "id": "bcb745af-838e-4241-aff4-dc5df67756bb",
  "name": "Pépito",
  "species": "Jade tree",
  "acquisition__age": 25,
}
```

### Add a bonsai to an owner

>**POST** /owner/{owner_id}/bonsais

**Body :**
```json
["5c4eb5ad-e825-4444-bbe1-18639330a2a8","5c4eb5ad-e825-4444-bbe1-18639330a2a8"]
```

Name|Type| In |Description
----|----|----|-----------
owner_id|string|path|The id of the current owner
bonsai_id|string|body|**Required** The id of the bonsai to transfer

**Response :**
```json
{
  "id": "bcb745af-838e-4241-aff4-dc5df67756bb",
  "name": "Pépito",
  "species": "Jade tree",
  "acquisition_age": 25,
}
```
