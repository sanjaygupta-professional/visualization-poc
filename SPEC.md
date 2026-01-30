# Visualization POC Specification

> **Version**: 1.0
> **Last Updated**: 2026-01-29
> **Status**: Ready for Implementation

---

## 1. Background

### 1.1 Current State

The book companion application generates visual summaries using Mermaid diagrams with:

- **7 diagram types**: flowchart, mindmap, flowchart TB/LR, subgraphs, stateDiagram, graph
- **6-color semantic palette**: Mapping concepts to colors (agent=blue, outcome=green, etc.)
- **Progressive reveal pattern**: Simple → Basic → Intermediate → Full complexity
- **No genre detection**: Claude implicitly chooses diagram types without formal rules

**Location**: `/home/sanjayegupta/projects/society-of-mind-visual/skills/book-to-visual-companion.md`

### 1.2 Problems to Solve

| Problem | Impact |
|---------|--------|
| Generic diagram logic | Business books get same treatment as physics books |
| Limited diagram types | 7 Mermaid types may not cover all conceptual structures |
| Rendering quality ceiling | Mermaid is convenient but visually basic |
| No evaluation framework | Can't objectively compare improvements |

---

## 2. POC Objectives

### 2.1 Track 1: Diagram Logic Quality

**Hypothesis**: Genre-specific visualization prompts produce more relevant and insightful diagrams than generic prompts.

**Approach**: Compare outputs from:
- **(A) Baseline**: Current generic `book-to-visual-companion.md` approach
- **(B) Genre-specific**: Use specialized prompts per book type

**Genre Categories**:

| Genre | Visualization Focus | Example Diagram Types |
|-------|--------------------|-----------------------|
| **Business/Strategy** | Frameworks, competitive analysis, growth models | 2x2 matrices, value chains, strategy maps |
| **Technical/Engineering** | Architecture, data flow, system design | Component diagrams, sequence diagrams, ERDs |
| **Narrative/History** | Timelines, cause-effect chains, character relationships | Timeline flows, event cascades, relationship graphs |
| **Philosophy/Ideas** | Argument structures, concept decomposition, dialectics | Argument maps, concept hierarchies, thesis-antithesis flows |

### 2.2 Track 2: Diagram Rendering Quality

**Hypothesis**: Alternative rendering tools can produce higher visual quality than Mermaid for specific use cases.

**Candidates**:

| Tool | Type | Strengths | Weaknesses |
|------|------|-----------|------------|
| **Mermaid** (baseline) | Text → SVG | Easy, Git-friendly, integrated | Limited styling, basic aesthetics |
| **D3.js** | JavaScript → SVG | Full control, interactive, beautiful | Complex, requires JS knowledge |
| **Graphviz (DOT)** | Text → SVG | Excellent for graphs, automatic layout | Less flexible styling |
| **Excalidraw** | JSON → SVG | Hand-drawn aesthetic, approachable | Less precise, different feel |

**Not pursuing** (for this POC):
- AI image generation (Gemini Imagen) - Too expensive, inconsistent text labels
- Manim - Overkill for static diagrams
- React Flow - More suited for interactive editors

---

## 3. Implementation Plan

### 3.1 Sample Selection

Select **3 content samples** representing different genres:

| Sample | Source Book | Genre | Chapter/Section |
|--------|-------------|-------|-----------------|
| S1 | Antifragile (Taleb) | Business/Philosophy | Barbell Strategy concept |
| S2 | Society of Mind (Minsky) | Cognitive Science | Agents and Agencies |
| S3 | Fabric of Reality (Deutsch) | Physics/Philosophy | Multiverse explanation |

**Rationale**: These span business frameworks, technical concepts, and philosophical arguments.

### 3.2 Track 1 Experiments

#### Experiment 1A: Baseline Diagram Generation

For each sample:
1. Extract ~500 words of source content
2. Use current generic prompt from `book-to-visual-companion.md`
3. Generate Mermaid diagram
4. Save to `results/track1/baseline/`

#### Experiment 1B: Genre-Specific Diagram Generation

For each sample:
1. Use same source content
2. Apply genre-specific prompt (see Section 4)
3. Generate Mermaid diagram
4. Save to `results/track1/genre-specific/`

#### Experiment 1C: Evaluation

1. Score both outputs using EVAL.md rubrics
2. Document scores in `results/track1/scores.md`
3. Analyze patterns

### 3.3 Track 2 Experiments

#### Experiment 2A: Multi-Tool Rendering

Select **1 diagram** from Track 1 results:
1. Take the Mermaid source
2. Recreate equivalent in:
   - D3.js (manual implementation)
   - Graphviz DOT syntax
3. Save all versions to `results/track2/`

#### Experiment 2B: Evaluation

1. Score all renderings using EVAL.md rubrics
2. Measure objective metrics (file size, render time)
3. Document in `results/track2/scores.md`

---

## 4. Genre-Specific Prompt Templates

### 4.1 Business/Strategy Books

```markdown
## Visualization Strategy for Business/Strategy Content

Focus on:
- **Frameworks**: 2x2 matrices, quadrant analysis
- **Competitive dynamics**: Porter's forces style, value chain
- **Growth models**: S-curves, adoption funnels
- **Decision structures**: Decision trees, option comparisons

Diagram type selection:
- Strategic choice → 2x2 matrix using subgraphs
- Process/workflow → Horizontal flowchart with stages
- Comparison → Side-by-side subgraphs
- Hierarchy → Top-down flowchart with clear levels

Color semantics:
- Opportunity/Growth: Green tones
- Risk/Threat: Red/Orange tones
- Current state: Blue tones
- Future state: Purple tones
```

### 4.2 Technical/Engineering Books

```markdown
## Visualization Strategy for Technical Content

Focus on:
- **Architecture**: Component relationships, layers
- **Data flow**: Input → Process → Output patterns
- **System states**: State machines, transitions
- **Sequences**: Step-by-step operations

Diagram type selection:
- System architecture → Flowchart with subgraphs for components
- Data pipeline → Left-to-right flowchart
- State changes → stateDiagram-v2
- API/interaction → Sequence-style vertical flow

Color semantics:
- Input/Source: Blue tones
- Processing: Yellow/Orange tones
- Output/Result: Green tones
- Error/Exception: Red tones
```

### 4.3 Narrative/History Books

```markdown
## Visualization Strategy for Narrative Content

Focus on:
- **Timelines**: Chronological event sequences
- **Cause-effect**: Event cascades, consequences
- **Relationships**: Character/entity connections
- **Parallel threads**: Multiple storylines

Diagram type selection:
- Timeline → Horizontal flowchart with date markers
- Cause-effect → Top-down cascade flowchart
- Relationships → Graph with named connections
- Parallel events → Subgraphs side by side

Color semantics:
- Era/Period: Distinct color per timeframe
- Positive events: Green/Blue tones
- Negative events: Red/Orange tones
- Key figures: Purple/highlighted
```

### 4.4 Philosophy/Ideas Books

```markdown
## Visualization Strategy for Philosophical Content

Focus on:
- **Arguments**: Premise → Conclusion structures
- **Dialectics**: Thesis vs Antithesis → Synthesis
- **Concept decomposition**: Abstract → Concrete
- **Intellectual lineage**: Influence flows

Diagram type selection:
- Argument → Top-down flowchart (premises at top, conclusion at bottom)
- Dialectic → Three-part structure with synthesis emerging
- Concept breakdown → Mindmap or hierarchical flowchart
- Influence → Graph with directional edges

Color semantics:
- Core thesis: Purple/primary tone
- Supporting evidence: Blue tones
- Counter-arguments: Orange tones
- Synthesis/Resolution: Green tones
```

---

## 5. File Structure

```
visualization-poc/
├── README.md                    # Overview and quick links
├── SPEC.md                      # This file
├── EVAL.md                      # Evaluation criteria and rubrics
├── samples/
│   ├── s1-antifragile.md        # Business/Philosophy sample
│   ├── s2-society-of-mind.md    # Cognitive Science sample
│   └── s3-fabric-of-reality.md  # Physics/Philosophy sample
└── results/
    ├── track1/
    │   ├── baseline/
    │   │   ├── s1-baseline.md
    │   │   ├── s2-baseline.md
    │   │   └── s3-baseline.md
    │   ├── genre-specific/
    │   │   ├── s1-genre.md
    │   │   ├── s2-genre.md
    │   │   └── s3-genre.md
    │   └── scores.md
    └── track2/
        ├── mermaid/
        ├── d3/
        ├── graphviz/
        └── scores.md
```

---

## 6. Tools & Dependencies

### 6.1 Required

- **Context7 MCP**: For up-to-date Mermaid, D3.js, Graphviz documentation
- **Claude**: For diagram generation with different prompts
- **Node.js 20+**: For any scripting needs

### 6.2 Optional (for Track 2)

```bash
# Graphviz (for DOT rendering)
sudo apt-get install graphviz

# D3.js (via npm if creating standalone visualizations)
npm install d3
```

---

## 7. Constraints & Boundaries

### 7.1 In Scope

- Testing diagram logic approaches
- Comparing rendering tools
- Creating evaluation framework
- Documenting findings

### 7.2 Out of Scope (for this POC)

- Full implementation in book-to-visual-companion skill
- Automated genre detection
- Interactive diagrams
- Animation/video generation
- Production deployment

---

## 8. Dependencies on Other Work

| Dependency | Status | Notes |
|------------|--------|-------|
| Existing book companions | Available | society-of-mind-visual, antifragile-visual, etc. |
| viz-* skills | Available | viz-business, viz-technical, viz-narrative, viz-philosophical |
| Context7 MCP | Verified | Working as of 2026-01-29 |

---

## 9. Risk Mitigation

| Risk | Likelihood | Mitigation |
|------|------------|------------|
| Subjective evaluation bias | Medium | Use rubrics, multiple samples, document reasoning |
| D3.js complexity too high | Medium | Limit to one simple diagram, accept "effort" as a data point |
| Samples not representative | Low | Choose diverse content types |
| POC scope creep | Medium | Strict boundaries in Section 7.2 |

---

## 10. Next Steps

1. [ ] Review this spec and EVAL.md
2. [ ] Extract sample content into `samples/` folder
3. [ ] Run Track 1 experiments (baseline vs genre-specific)
4. [ ] Run Track 2 experiments (multi-tool rendering)
5. [ ] Score results using EVAL.md rubrics
6. [ ] Document recommendation
