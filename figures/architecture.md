flowchart TB
User[User / Web Browser]

    subgraph Host["Application Host"]
        Nginx[Nginx Reverse Proxy]

        subgraph Frontend
            React[React Frontend]
        end

        subgraph Backend
            API[NestJS API]
            PBSCollector["PBS Collector<br/>Microservice"]
        end
    end

    subgraph External["External Systems"]
        PBS[PBS Server]
        Perun[PERUN<br/>Push-based]
        Prometheus[Prometheus<br/>OpenStack Metrics]
        PostgreSQL[(PostgreSQL<br/>Accounting DB)]
    end

    %% Connections
    User --> Nginx
    Nginx --> React
    Nginx --> API
    API --> PostgreSQL
    API --> PBSCollector
    PBSCollector --> PBS
    Perun --> API
    API --> Prometheus

    %% Styles (Blue / Light Blue only)
    classDef user fill:#f5f9ff,stroke:#1e3a8a,stroke-width:1px,color:#000
    classDef proxy fill:#659aee,stroke:#1e40af,stroke-width:1px,color:#000
    classDef frontend fill:#659aee,stroke:#1e40af,stroke-width:1px,color:#000
    classDef backend fill:#659aee,stroke:#1d4ed8,stroke-width:1px,color:#000
    classDef database fill:#659aee,stroke:#2563eb,stroke-width:1px,color:#000
    classDef external fill:#659aee,stroke:#1e40af,stroke-width:1px,color:#000
    classDef host fill:#91b9f7,color:#000
    classDef parts fill:#91b9f7,color:#000
    classDef externalHost fill:#fff,color:#000
    classDef externalParts fill:#fff,color:#000

    %% Apply classes
    class User user
    class Nginx proxy
    class React frontend
    class API,PBSCollector backend
    class PostgreSQL database
    class PBS,Perun,Prometheus external
    class Host host
    class Frontend parts
    class Backend parts
    class External externalHost
