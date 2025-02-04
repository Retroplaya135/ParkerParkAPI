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

GET /v1/parking/spots

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
