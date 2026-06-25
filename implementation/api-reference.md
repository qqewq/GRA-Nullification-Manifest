# API Reference

## Base URL

```
Production: https://api.gra-manifest.org/v1
Staging: https://staging-api.gra-manifest.org/v1
Local: http://localhost:8000/v1
```

## Authentication

All endpoints require a Bearer token:
```
Authorization: Bearer <jwt_token>
```

## Endpoints

### POST /capture
Capture a new thought.

**Request:**
```json
{
  "content": "Feeling anxious about the presentation",
  "emotion": -0.6,
  "level": 1,
  "tags": ["work", "anxiety"]
}
```

**Response:**
```json
{
  "id": "550e8400-e29b-41d4-a716-446655440000",
  "embedding": [0.12, -0.34, ...],
  "foam_delta": 0.15,
  "cluster_id": 7,
  "timestamp": "2026-06-25T07:04:00Z"
}
```

### GET /foam
Get current foam profile.

**Response:**
```json
{
  "user_id": "550e8400-e29b-41d4-a716-446655440000",
  "phi_levels": {
    "0": 0.05,
    "1": 0.23,
    "2": 0.11,
    "3": 0.02
  },
  "r_hier": 3,
  "stability_score": 0.78,
  "total_phi": 0.41
}
```

### POST /nullify
Apply nullification to a specific level.

**Request:**
```json
{
  "level": 1,
  "strategy": "soft",
  "confirm": true
}
```

**Response:**
```json
{
  "success": true,
  "phi_before": 0.23,
  "phi_after": 0.08,
  "reduction": 0.15,
  "new_r_hier": 3,
  "recommendations": [
    "Consider reviewing cluster 7 patterns"
  ]
}
```

### GET /report
Generate a report for a time period.

**Query Parameters:**
- `start_date`: ISO 8601 date
- `end_date`: ISO 8601 date
- `format`: `json` | `pdf`

**Response:**
```json
{
  "period": "2026-06-01 to 2026-06-25",
  "thoughts_count": 1847,
  "avg_phi": 0.34,
  "r_hier_trend": [2, 2, 3, 3, 3, 4, 3],
  "top_clusters": [
    {"id": 7, "label": "work anxiety", "count": 42},
    {"id": 3, "label": "morning plans", "count": 38}
  ]
}
```

### WebSocket /ws/stream
Real-time foam updates.

**Messages:**
```json
// Server → Client
{
  "type": "foam_update",
  "data": {
    "level": 1,
    "phi": 0.19,
    "timestamp": "2026-06-25T07:04:00Z"
  }
}
```

## Error Codes

| Code | Description |
|------|-------------|
| 400 | Bad Request |
| 401 | Unauthorized |
| 404 | User/Resource not found |
| 422 | Validation Error |
| 429 | Rate Limited |
| 500 | Internal Server Error |
