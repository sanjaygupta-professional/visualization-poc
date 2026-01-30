# Track 2 Mermaid: Paradigm Shift Diagram

**Source**: S2 Genre-Specific - Agents (Society of Mind)
**Diagram**: Parts vs Agents paradigm shift
**Tool**: Mermaid
**Time to create**: ~2 minutes (already had template)

---

## Mermaid Source

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

## Metrics

- **Lines of code**: 28
- **Render method**: Paste into any Mermaid-enabled tool
- **Output format**: SVG (rendered by JS)
- **Learning curve**: Low (markdown-like syntax)
