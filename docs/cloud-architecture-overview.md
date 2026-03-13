# Cloud Architecture Overview

This monorepo uses a simple local architecture suitable for MVP development.

## System Context

```mermaid
graph LR
    User[User in Browser]
    FE[React Frontend\npackages/frontend]
    API[Express API\npackages/backend]
    MEM[(In-Memory Store\nprocess memory)]

    User -->|Uses UI| FE
    FE -->|HTTP JSON requests| API
    API -->|Read/Write tasks| MEM
    API -->|JSON responses| FE
```

## Sequence: Create a TODO

```mermaid
sequenceDiagram
    autonumber
    actor U as User
    participant FE as React Frontend
    participant API as Express API
    participant MEM as In-Memory Store

    U->>FE: Enter title and submit "Create TODO"
    FE->>API: POST /tasks { title, dueDate?, priority? }
    API->>API: Validate request payload
    API->>MEM: Create task in process memory
    MEM-->>API: Return created task object
    API-->>FE: 201 Created + task JSON
    FE-->>U: Render updated TODO list with new task
```

## Notes

- The frontend is a React single-page application.
- The backend is an Express API running in the same repository.
- Data persistence is in-memory for runtime only; data resets when the backend restarts.
