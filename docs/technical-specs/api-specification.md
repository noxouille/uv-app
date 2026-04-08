# API Specification

Base URL: `/api/v1`

---

## Authentication

### POST /auth/register

Register a new user account.

**Request**:

```json
{
  "email": "user@example.com",
  "password": "securepassword123"
}
```

**Response 201**:

```json
{
  "id": 1,
  "email": "user@example.com",
  "is_active": true,
  "created_at": "2025-04-08T12:00:00Z"
}
```

### POST /auth/login

Authenticate and receive JWT token.

**Request**:

```json
{
  "email": "user@example.com",
  "password": "securepassword123"
}
```

**Response 200**:

```json
{
  "access_token": "eyJhbGciOiJIUzI1NiIsInR5cCI6...",
  "token_type": "bearer",
  "expires_in": 900
}
```

---

## Profiles

### POST /profiles

Create a new user profile.

**Headers**:

```
Authorization: Bearer <token>  (optional for MVP)
```

**Request**:

```json
{
  "adults_count": 2,
  "children_count": 1,
  "children_ages": [8],
  "diet_type": "vegetarian",
  "allergies": ["nuts", "gluten"],
  "weekly_budget": 150.0,
  "cooking_time": "medium",
  "cooking_mode": "daily",
  "postal_code": "H2X 1Y4",
  "max_travel_distance_km": 10
}
```

**Response 201**:

```json
{
  "id": 1,
  "adults_count": 2,
  "children_count": 1,
  "children_ages": [8],
  "diet_type": "vegetarian",
  "allergies": ["nuts", "gluten"],
  "weekly_budget": 150.0,
  "cooking_time": "medium",
  "cooking_mode": "daily",
  "postal_code": "H2X 1Y4",
  "latitude": 45.5019,
  "longitude": -73.5674,
  "max_travel_distance_km": 10,
  "created_at": "2025-04-08T12:00:00Z"
}
```

### GET /profiles/me

Get current user's profile.

**Response 200**: Profile object  
**Response 404**: Profile not found

### PUT /profiles/me

Update profile (partial update supported).

**Request**:

```json
{
  "weekly_budget": 175.0,
  "cooking_mode": "batch"
}
```

**Response 200**: Updated profile

---

## Zones

### GET /zones/validate

Validate if a postal code is in a serviceable zone.

**Query Parameters**:

- `postal_code` (required): Canadian postal code

**Response 200**:

```json
{
  "postal_code": "H2X 1Y4",
  "serviceable": true,
  "region": "Montreal",
  "message": "Service available in Montreal"
}
```

**Response 200 (not serviceable)**:

```json
{
  "postal_code": "A1A 1A1",
  "serviceable": false,
  "region": null,
  "message": "Service not yet available in your area"
}
```

---

## Error Responses

All errors follow this format:

```json
{
  "detail": "Error description"
}
```

Or for validation errors:

```json
{
  "detail": [
    {
      "loc": ["body", "weekly_budget"],
      "msg": "ensure this value is greater than 0",
      "type": "value_error.number.not_gt"
    }
  ]
}
```

### HTTP Status Codes

| Code | Meaning                                 |
| ---- | --------------------------------------- |
| 200  | OK                                      |
| 201  | Created                                 |
| 400  | Bad Request (validation error)          |
| 401  | Unauthorized (invalid/missing token)    |
| 404  | Not Found                               |
| 422  | Unprocessable Entity (validation error) |
| 500  | Internal Server Error                   |

---

## Rate Limiting

- Authentication endpoints: 5 requests per minute
- All other endpoints: 100 requests per minute per IP

---

## Pagination

List endpoints support:

- `skip`: Number of items to skip (default: 0)
- `limit`: Number of items to return (default: 20, max: 100)

Example: `GET /api/v1/items?skip=20&limit=20`
