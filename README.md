# ParkerParkAPI

ParkPilot API provides a structured way to manage parking spots in a facility. It allows users to check availability, make reservations, and release spots when done. The system tracks usage based on client IP and includes admin tools for maintenance.

## Installation

### 1. Clone the repository
```bash
git clone https://github.com/Retroplaya135/ParkerParkAPI/
cd parkpilot-api
```

2. Install dependencies

pip install fastapi uvicorn pydantic

3. Start the API server
```
uvicorn main:app --host 0.0.0.0 --port 8000
```

API Endpoints

1. Retrieve All Parking Spots
2. Returns a list of all parking spots with their status.

```
GET /v1/parking/spots
```

Response

```

[
  {
    "id": 1,
    "location": "Spot-1",
    "status": "available",
    "reserved_by": null,
    "reservation_time": null
  },
  {
    "id": 2,
    "location": "Spot-2",
    "status": "reserved",
    "reserved_by": "user123",
    "reservation_time": "2024-02-03T12:30:00Z"
  }
]
```

2. Retrieve a Specific Parking Spot
Gets details for a specific spot.

```
GET /v1/parking/spots/{spot_id}
```

Response

```
{
  "id": 2,
  "location": "Spot-2",
  "status": "reserved",
  "reserved_by": "user123",
  "reservation_time": "2024-02-03T12:30:00Z"
}
```

3. Reserve a Parking Spot
Marks a parking spot as reserved.

```
POST /v1/parking/reserve
```

Payload
```
{
  "spot_id": 3,
  "user": "user456"
}
```

Response
```

{
  "id": 3,
  "location": "Spot-3",
  "status": "reserved",
  "reserved_by": "user456",
  "reservation_time": "2024-02-03T13:00:00Z"
}
```


Errors
```404 Spot not found – The spot ID does not exist.```

```400 Spot already reserved – The spot is taken.```


4. Release a Parking Spot
Frees up a reserved parking spot.

Request
```

POST /v1/parking/release
```


Payload
```

{
  "spot_id": 3,
  "user": "user456"
}
```


Response
```
{
  "id": 3,
  "location": "Spot-3",
  "status": "available",
  "reserved_by": null,
  "reservation_time": null
}
```


Errors

``` 404 Spot not found – The spot ID does not exist. ```

```400 Spot is not reserved – The spot is already available.```

```403 User not authorized – The user does not own the reservation.```


