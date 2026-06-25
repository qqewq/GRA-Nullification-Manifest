# Backend Architecture

## Overview

The GRA backend is built on Python 3.11+ with FastAPI, providing RESTful and WebSocket APIs for thought capture, foam analysis, and nullification operations.

## Microservices

```
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│   API Gateway   │────▶│  Auth Service   │     │  Capture Svc    │
│   (FastAPI)     │     │  (OAuth2/JWT)   │────▶│  (/capture)     │
└─────────────────┘     └─────────────────┘     └─────────────────┘
         │                                               │
         ▼                                               ▼
┌─────────────────┐     ┌─────────────────┐     ┌─────────────────┐
│  Foam Engine    │◄────│  Nullify Svc    │◄────│  Analysis Svc   │
│  (Python Core)  │     │  (/nullify)     │     │  (/foam)        │
└─────────────────┘     └─────────────────┘     └─────────────────┘
         │
         ▼
┌─────────────────┐     ┌─────────────────┐
│   PostgreSQL    │     │     Redis       │
│  (Persistent)   │     │   (Cache/Queue) │
└─────────────────┘     └─────────────────┘
```

## Core Modules

### 1. Capture Service
- **Endpoint**: `POST /capture`
- **Payload**: `{"content": "string", "emotion": "float", "level": "int"}`
- **Processing**: Semantic embedding → cluster assignment → foam delta

### 2. Foam Engine
- Computes $\Phi(k)$ for each hierarchy level
- Updates in real-time via Redis pub/sub
- Supports batch and streaming modes

### 3. Nullify Service
- **Endpoint**: `POST /nullify`
- **Payload**: `{"level": "int", "strategy": "soft|hard|wave"}`
- **Strategies**:
  - `soft`: Gradual recalibration
  - `hard`: Immediate reset
  - `wave`: Quantum-inspired superposition collapse

### 4. Report Service
- **Endpoint**: `GET /report?user_id=X&period=Y`
- Returns: $\Phi(k)$ timeline, $R_{	ext{hier}}$, recommendations

## Data Models

```python
class Thought(BaseModel):
    id: UUID
    user_id: UUID
    content: str
    embedding: List[float]
    emotion: float  # -1 to 1
    level: int
    timestamp: datetime

class FoamProfile(BaseModel):
    user_id: UUID
    phi_levels: Dict[int, float]
    r_hier: int
    stability_score: float
```

## Deployment

- Docker + Docker Compose for local development
- Kubernetes for production
- CI/CD via GitHub Actions
