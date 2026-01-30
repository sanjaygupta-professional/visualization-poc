# Track 1 Scoring Results

**Evaluation Date**: 2026-01-29
**Evaluator**: Claude (Hybrid approach - applying rubrics systematically)

---

## Sample S1: Barbell Strategy (Antifragile)
**Genre**: Business/Philosophy

### Baseline (Generic Prompt)

| Dimension | Score | Notes |
|-----------|-------|-------|
| Diagram Type Fit | 3/5 | Flowchart with subgraphs works but doesn't leverage barbell metaphor |
| Concept Coverage | 3/5 | Covers three categories but misses asymmetry logic |
| Information Hierarchy | 2/5 | All nodes similar weight, no emphasis on key insight |
| Genre Appropriateness | 2/5 | Generic structure, no business/strategy conventions |
| **TOTAL** | **10/20** | |

### Genre-Specific (Business Strategy Prompt)

| Dimension | Score | Notes |
|-----------|-------|-------|
| Diagram Type Fit | 5/5 | Multiple complementary views: barbell layout, quadrant, decision tree |
| Concept Coverage | 5/5 | Captures allocation percentages, payoff asymmetry, bounded vs unbounded risk |
| Information Hierarchy | 4/5 | Clear emphasis on actionable recommendations, visual distinction |
| Genre Appropriateness | 5/5 | Uses 2x2 matrix, decision tree, percentage allocations - business conventions |
| **TOTAL** | **19/20** | |

### S1 Winner: **Genre-Specific** (+9 points)

**Key Difference**: Genre-specific approach used multiple business-appropriate visualizations (quadrant chart, decision tree) that reveal the core insight about bounded vs unbounded risk. Baseline just categorized without explaining WHY.

---

## Sample S2: Agents (Society of Mind)
**Genre**: Cognitive Science / Technical

### Baseline (Generic Prompt)

| Dimension | Score | Notes |
|-----------|-------|-------|
| Diagram Type Fit | 3/5 | Mindmap is reasonable for concept overview |
| Concept Coverage | 3/5 | Lists properties but doesn't show key interactions |
| Information Hierarchy | 3/5 | Mindmap provides some structure |
| Genre Appropriateness | 2/5 | No technical/systems conventions, missing architecture view |
| **TOTAL** | **11/20** | |

### Genre-Specific (Technical/Cognitive Science Prompt)

| Dimension | Score | Notes |
|-----------|-------|-------|
| Diagram Type Fit | 5/5 | Architecture diagram, sequence diagram, paradigm contrast - perfect for technical content |
| Concept Coverage | 5/5 | Shows agents in agencies, interaction protocols, type hierarchy, paradigm shift |
| Information Hierarchy | 4/5 | Clear layers: agents → agencies → mind; type progression |
| Genre Appropriateness | 5/5 | Uses component diagrams, sequence diagrams, system architecture - technical conventions |
| **TOTAL** | **19/20** | |

### S2 Winner: **Genre-Specific** (+8 points)

**Key Difference**: Genre-specific approach explicitly visualized the paradigm shift (parts vs agents) and used technical diagram types (sequence diagram, architecture) that reveal HOW agents interact dynamically. Baseline just listed properties.

---

## Sample S3: The Multiverse (Fabric of Reality)
**Genre**: Physics / Philosophy

### Baseline (Generic Prompt)

| Dimension | Score | Notes |
|-----------|-------|-------|
| Diagram Type Fit | 3/5 | Mindmap and branching flowchart are adequate |
| Concept Coverage | 3/5 | Lists components but doesn't show argument structure |
| Information Hierarchy | 2/5 | Flat structure, no emphasis on evidence vs conclusion |
| Genre Appropriateness | 2/5 | Generic categorization, no philosophical argument structure |
| **TOTAL** | **10/20** | |

### Genre-Specific (Physics/Philosophy Prompt)

| Dimension | Score | Notes |
|-----------|-------|-------|
| Diagram Type Fit | 5/5 | Argument structure, dialectical contrast, evidence flow - perfect for philosophy |
| Concept Coverage | 5/5 | Shows premises, evidence, conclusion; contrasts interpretations; connects to framework |
| Information Hierarchy | 5/5 | Clear progression: premise → evidence → conclusion; verdict highlighted |
| Genre Appropriateness | 5/5 | Uses argument maps, dialectical structure, synthesis diagram - philosophy conventions |
| **TOTAL** | **20/20** | |

### S3 Winner: **Genre-Specific** (+10 points)

**Key Difference**: Genre-specific approach structured the content as an ARGUMENT (premises → evidence → conclusion) and explicitly contrasted competing interpretations. This is how philosophers think. Baseline just listed facts without showing the reasoning.

---

## Summary Table

| Sample | Baseline | Genre-Specific | Improvement | Winner |
|--------|----------|----------------|-------------|--------|
| S1: Barbell Strategy | 10/20 | 19/20 | +9 | Genre-Specific |
| S2: Agents | 11/20 | 19/20 | +8 | Genre-Specific |
| S3: Multiverse | 10/20 | 20/20 | +10 | Genre-Specific |
| **Average** | **10.3/20** | **19.3/20** | **+9** | **Genre-Specific** |

---

## Dimension-by-Dimension Analysis

| Dimension | Baseline Avg | Genre-Specific Avg | Improvement |
|-----------|--------------|-------------------|-------------|
| Diagram Type Fit | 3.0 | 5.0 | +2.0 |
| Concept Coverage | 3.0 | 5.0 | +2.0 |
| Information Hierarchy | 2.3 | 4.3 | +2.0 |
| Genre Appropriateness | 2.0 | 5.0 | +3.0 |

**Biggest improvement**: Genre Appropriateness (+3.0 average)
This confirms the hypothesis: the main benefit of genre-specific prompts is leveraging domain conventions.

---

## Key Findings

### Why Genre-Specific Works Better

1. **Domain conventions matter**: Business readers expect matrices and decision trees. Technical readers expect architecture diagrams. Philosophers expect argument structures.

2. **Reveals "why" not just "what"**: Generic diagrams list/categorize. Genre-specific diagrams explain reasoning, show trade-offs, contrast alternatives.

3. **Multiple complementary views**: Genre-specific prompts produced 2-4 diagrams per sample vs 1-2 for baseline, each showing different aspect.

4. **Information hierarchy emerges naturally**: When you use domain conventions, emphasis falls naturally on what matters to that domain.

### Patterns Observed

| Genre | Key Diagram Types | Core Insight Method |
|-------|------------------|---------------------|
| Business/Strategy | 2x2 matrix, decision tree, payoff structure | Show bounded vs unbounded outcomes |
| Technical/Cognitive | Architecture, sequence, component | Show dynamic interactions and layers |
| Physics/Philosophy | Argument map, dialectical contrast, synthesis | Show reasoning from evidence to conclusion |

---

## Track 1 Conclusion

**Result**: Genre-specific approach won **3/3 samples** with an average improvement of **+9 points** (45% improvement).

**Recommendation**: **IMPLEMENT** - Update the book-to-visual-companion skill to use genre-specific prompts.

The largest improvement was in Genre Appropriateness (+3.0), confirming that the main value is in leveraging domain-specific visualization conventions that readers in each field already understand and expect.
