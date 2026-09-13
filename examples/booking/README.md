# Booking API Example

A sample booking API that demonstrates how Schemathesis automatically discovers various types of bugs that manual testing typically misses.

> 📚 **Tutorial available:** This API is used in the **[Schemathesis Tutorial](../../docs/tutorial.md)** - a 15-20 minute walkthrough of its core features.

## Overview

- Hotel booking creation and retrieval
- Bearer token authentication
- Room type validation (returns 400 for invalid room types)
- Open API 3.1 schema provided by FastAPI

## Quick Start

Start the API:
```bash
docker compose up -d
```

Verify it's running:

Open [http://localhost:8080/docs](http://localhost:8080/docs) to see the interactive API documentation.

The API will be available at:

- **Base URL**: http://localhost:8080

- **OpenAPI Schema**: http://localhost:8080/openapi.json

## Authentication

All booking endpoints require bearer token authentication.

```bash
Authorization: Bearer secret-token
```

## Test with Schemathesis

```bash
uvx schemathesis run http://localhost:8080/openapi.json \
  --header 'Authorization: Bearer secret-token'
```

## GitHub Actions

The **Manual build API example** workflow (`.github/workflows/example-build.yml`) runs Schemathesis against this API in CI.

1. Enable Actions on your fork: [Actions tab](https://github.com/Simon111302/schemathesis/actions) → **I understand my workflows, go ahead and enable them**
2. Trigger manually: **Actions → Manual build API example → Run workflow**
3. Or push changes under `examples/booking/` to trigger automatically

## Example Usage

Create a booking:
```bash
curl -X POST "http://localhost:8080/bookings" \
  -H "Authorization: Bearer secret-token" \
  -H "Content-Type: application/json" \
  -d '{
    "guest_name": "John Doe",
    "room_type": "deluxe",
    "nights": 3
  }'
```

Retrieve booking:
```bash
curl -H "Authorization: Bearer secret-token" \
  http://localhost:8080/bookings/42
```
