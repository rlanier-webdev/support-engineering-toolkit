flowchart TD

A[API Issue Reported] --> B[Validate Request Layer]
B --> C{Request Valid?}

C -->|No| D[Fix Payload / Endpoint / Method]
C -->|Yes| E[Check Auth Layer]

E --> F{Auth OK?}

F -->|No| G[Fix Token / Scope / Permissions]
F -->|Yes| H[Check Response Code]

H --> I{4xx or 5xx?}

I -->|4xx| J[Client-side issue analysis]
I -->|5xx| K[Application Layer Debugging]

K --> L{Dependency Issue?}
L -->|Yes| M[External / DB / Service Check]
L -->|No| N[Internal Logic Investigation]

J --> O[Reproduce + Validate Fix]
M --> O
N --> O