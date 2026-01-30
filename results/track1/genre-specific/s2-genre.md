# S2 Genre-Specific: Agents (Technical/Cognitive Science Approach)

**Approach**: Technical visualization strategy
- Use component/architecture diagram style
- Show system layers and interactions
- Emphasize the paradigm shift (parts vs agents)
- Use data flow patterns (technical convention)

---

## Core Architecture Diagram

```mermaid
flowchart TB
    subgraph Mind["THE MIND (Emergent System)"]
        subgraph Agency1["Agency: BUILDER"]
            A1["Agent: FIND"]
            A2["Agent: GET"]
            A3["Agent: PUT"]
            A1 -->|"activates"| A2
            A2 -->|"activates"| A3
        end

        subgraph Agency2["Agency: SEE"]
            B1["Agent: EDGE"]
            B2["Agent: COLOR"]
            B3["Agent: SHAPE"]
            B1 -.->|"signals"| B2
            B2 -.->|"signals"| B3
        end

        Agency1 <-->|"communicate"| Agency2
    end

    Input["Sensory Input"] --> Mind
    Mind --> Output["Behavior Output"]

    style Mind fill:#f5f5f5,stroke:#333,stroke-width:2px
    style Agency1 fill:#e3f2fd,stroke:#1976d2
    style Agency2 fill:#fff3e0,stroke:#f57c00
```

---

## Paradigm Shift: Parts vs Agents

```mermaid
flowchart LR
    subgraph Old["❌ Traditional View: PARTS"]
        direction TB
        P1["Part A"]
        P2["Part B"]
        P3["Part C"]
        W["Whole"]
        P1 --> W
        P2 --> W
        P3 --> W
    end

    Arrow["→"]

    subgraph New["✓ Minsky's View: AGENTS"]
        direction TB
        AG1["Agent α"]
        AG2["Agent β"]
        AG3["Agent γ"]
        AGY["Agency"]
        MIND["Mind"]

        AG1 <-->|"signal"| AG2
        AG2 <-->|"signal"| AG3
        AG1 --> AGY
        AG2 --> AGY
        AG3 --> AGY
        AGY --> MIND
    end

    Old --> Arrow --> New

    style Old fill:#ffcdd2,stroke:#c62828
    style New fill:#c8e6c9,stroke:#2e7d32
```

---

## Agent Interaction Protocol

```mermaid
sequenceDiagram
    participant E as Environment
    participant A1 as Agent: DETECT
    participant A2 as Agent: PROCESS
    participant A3 as Agent: ACT
    participant M as Memory

    E->>A1: stimulus
    A1->>M: query state
    M-->>A1: context
    A1->>A2: activation signal
    A2->>A2: compute
    A2->>A3: output signal
    A3->>E: action

    Note over A1,A3: Each agent is simple<br/>Intelligence emerges from interaction
```

---

## Agent Type Hierarchy

```mermaid
flowchart TB
    subgraph Types["Agent Type System"]
        direction TB

        Basic["BASIC AGENTS<br/>Simple stimulus-response<br/>(SEE, GRASP, MOVE)"]

        Memory["MEMORY AGENTS<br/>K-lines: reconnect past states<br/>(Remember, Recall)"]

        Control["CONTROL AGENTS<br/>Manage other agents<br/>(Suppress, Activate)"]

        Detector["DETECTOR AGENTS<br/>Pattern recognition<br/>(Recognize, Match)"]

        Basic --> Memory
        Memory --> Control
        Control --> Detector
    end

    style Basic fill:#e3f2fd,stroke:#1976d2
    style Memory fill:#fff3e0,stroke:#f57c00
    style Control fill:#f3e5f5,stroke:#7b1fa2
    style Detector fill:#e8f5e9,stroke:#388e3c
```

---

## Analysis

**What this diagram does:**
- Shows system architecture (agencies containing agents)
- Visualizes the paradigm shift explicitly
- Uses sequence diagram for interaction protocol (technical convention)
- Shows type hierarchy with progression (technical pattern)
- Bidirectional arrows show dynamic interaction

**Technical/Cognitive Science improvements:**
- Component diagram style familiar to technical readers
- Sequence diagram shows temporal interaction
- Type system shows specialization hierarchy
- Architecture view reveals emergent structure
- Explicit contrast between old and new paradigms
