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
uvicorn main:app --host 0.0.0.0 --port 8000

API Endpoints

1. Retrieve All Parking Spots
Returns a list of all parking spots with their status.

GET /v1/parking/spots
