graph TB
    subgraph Node1
        subgraph PodA
            A[App A]
        end
        subgraph PodB
            B[App B]
        end
        Z1[ztunnel]
    end
    
    subgraph Node2
        subgraph PodC
            C[App C]
        end
        Z2[ztunnel]
    end
    
    subgraph WaypointProxyLayer
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
    
    style Z1 fill:#f9f,stroke:#333
    style Z2 fill:#f9f,stroke:#333
    style W1 fill:#bbf,stroke:#333
    style W2 fill:#bbf,stroke:#333