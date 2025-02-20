flowchart TD
    subgraph N1[Node 1]
        A[App A]
        B[App B]
        Z1[ztunnel]
    end
    
    subgraph N2[Node 2]
        C[App C]
        Z2[ztunnel]
    end
    
    subgraph WP[Waypoint Layer]
        W1[Waypoint A]
        W2[Waypoint B]
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
    
    style Z1 fill:#f9f,stroke:#333
    style Z2 fill:#f9f,stroke:#333
    style W1 fill:#bbf,stroke:#333
    style W2 fill:#bbf,stroke:#333