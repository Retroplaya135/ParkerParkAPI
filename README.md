# ParkPilotAPI

ParkPilot API provides a structured way to manage parking spots in a facility. It allows users to check availability, make reservations, and release spots when done. The system tracks usage based on client IP and includes admin tools for maintenance.

 for parking management.

---

## 🚀 Key Features

- **View Parking Availability**: Check available and reserved spots.
- **Reserve a Parking Spot**: Users can reserve a spot by providing their details.
- **Release a Parking Spot**: Only the reserving user can release their spot.
- **Real-Time Status Updates**: Parking spot statuses update instantly.
- **Usage Tracking**: API usage is logged per client IP.
- **Admin Functions**: Reset parking spots and clear usage logs.
- **Health & Stats**: Monitor API health, usage, and version information.

---

```
+-------------------------------+
|       Parker Park API         |
+-------------------------------+
        |          |          |
        v          v          v
+----------------+  +----------------+  +----------------+
|  User API     |  | Admin API      |  | Health & Stats |
| (Reserve,     |  | (Reset Spots,  |  | (Monitor API)  |
| Release, View)|  |  Clear Logs)   |  |                |
+----------------+  +----------------+  +----------------+
        |          |          |
        v          v          v
+----------------------------------------------------+
|                FastAPI Backend                    |
| (Handles requests, validation, & responses)      |
+----------------------------------------------------+
        |
        v
+----------------------------------------------------+
|              SQLite / PostgreSQL Database         |
| (Tracks reservations, users, and logs)           |
+----------------------------------------------------+
```

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


Errors:

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

5. Get Parking Occupancy Status
Provides a summary of total spots, reserved spots, and available spots.

Request
```
GET /v1/parking/status
```

Response
```

{
  "total": 10,
  "reserved": 2,
  "available": 8
}
```


6. API Health Check
   
Ensures the API is running properly.

Request
```
GET /v1/health
```


Response
```
{
  "status": "ok",
  "timestamp": "2024-02-03T12:45:00Z"
}
```


7. API Usage Statistics
Tracks API usage by IP.

Request
```
GET /v1/stats
```

Response
```
{
  "usage": {
    "192.168.1.10": 5,
    "192.168.1.11": 7
  },
  "timestamp": "2024-02-03T12:50:00Z"
}
```

### Admin Endpoints

1. Reset All Parking Spots
   
Resets all parking spots to their default state.

Request

```
POST /v1/admin/reset
```

Response

```
{
  "status": "parking spots reset",
  "timestamp": "2024-02-03T12:55:00Z"
}
```

2. Reset API Usage Logs
Clears the recorded usage statistics.

Request

```
POST /v1/admin/reset_usage
```

Response
```
{
  "status": "usage log reset",
  "timestamp": "2024-02-03T13:00:00Z"
}
```

How It Works

FastAPI Backend
The API is built using FastAPI for speed and scalability.
Fully asynchronous to handle multiple requests efficiently.
Reservation & Release System
Users can reserve a parking spot and release it when done.
Only the reserving user can release their spot.


## Reset API Usage Logs

Clear all logged API usage.

Request:
```
POST /v1/admin/reset_usage
```
Response:
```
{
  "status": "usage log reset",
  "timestamp": "2024-02-04T13:05:00Z"
}
```

#Local Deployment

```
uvicorn main:app --host 0.0.0.0 --port 8000
```

Deploy with Docker

Create a Dockerfile

```
FROM python:3.10
WORKDIR /app
COPY . .
RUN pip install -r requirements.txt
CMD ["uvicorn", "main:app", "--host", "0.0.0.0", "--port", "8000"]
```

Build and Run Docker Container

```
docker build -t parkpilot-api .
docker run -p 8000:8000 parkpilot-api
```

Technical Overview

FastAPI Backend
Built using FastAPI for high-speed request handling. Fully asynchronous to support multiple concurrent API calls.
Parking Reservation System
Users can reserve a parking spot. Only the user who reserved the spot can release it.
Real-Time Parking Status
View current availability and total reservations. Instant updates when spots are reserved or released.
Usage Tracking
API logs requests per client IP. Admins can reset logs when needed.
Admin Controls
Reset all parking spots to clear existing reservations. Clear usage logs to reset tracked data.


License

This project is licensed under the MIT License. 
