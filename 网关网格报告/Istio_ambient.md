flowchart TD
    subgraph Node1["Node 1"]
        direction TB
        subgraph PodA["Pod A"]
            A[App A]
        end
        subgraph PodB["Pod B"]
            B[App B]
        end
        Z1[ztunnel]
    end
    
    subgraph Node2["Node 2"]
        direction TB
        subgraph PodC["Pod C"]
            C[App C]
        end
        Z2[ztunnel]
    end
    
    subgraph WaypointLayer["Waypoint Proxy Layer"]
        direction LR
        W1[Waypoint Proxy A]
        W2[Waypoint Proxy B]
    end
    
    A --> Z1
    B --> Z1
    C --> Z2
    
    Z1 --> W1
    Z1 --> W2
    Z2 --> W1
    Z2 --> W2
    
    W1 --> A
    W1 --> B
    W2 --> C
    
    style Z1 fill:#f9f,stroke:#333,stroke-width:2px
    style Z2 fill:#f9f,stroke:#333,stroke-width:2px
    style W1 fill:#bbf,stroke:#333,stroke-width:2px
    style W2 fill:#bbf,stroke:#333,stroke-width:2px