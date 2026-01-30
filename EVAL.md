# Visualization POC Evaluation Framework

> **Version**: 1.0
> **Last Updated**: 2026-01-29
> **Approach**: Hybrid (automated metrics + manual rubric scoring)

---

## 1. Evaluation Philosophy

### 1.1 Why Eval-Driven Development?

Before writing code, we define:
- **What success looks like** (acceptance criteria)
- **How we measure it** (rubrics and metrics)
- **What evidence we need** (test protocols)

This prevents:
- Subjective "I think this is better" conclusions
- Scope creep ("let's also try X")
- Inconclusive results

### 1.2 Hybrid Approach

| Type | What | How |
|------|------|-----|
| **Automated** | Objective, measurable properties | Scripts, file analysis |
| **Manual** | Subjective quality dimensions | Human scoring with rubrics |
| **Comparative** | Relative rankings | Side-by-side preference |

---

## 2. Track 1: Diagram Logic Evaluation

### 2.1 Evaluation Rubric

Score each diagram on these dimensions (1-5 scale):

#### Dimension 1: Diagram Type Fit

> Does the chosen diagram type effectively represent the content structure?

| Score | Description | Example |
|-------|-------------|---------|
| 1 | **Wrong type** - Diagram type obscures or misrepresents content | Using mindmap for sequential process |
| 2 | **Poor fit** - Type works but another would be much better | Using flowchart for comparison content |
| 3 | **Acceptable** - Reasonable choice, conveys information | Generic flowchart for most content |
| 4 | **Good fit** - Type matches content structure well | Timeline for historical sequence |
| 5 | **Optimal** - Best possible type, reveals hidden structure | 2x2 matrix for strategic tradeoffs |

#### Dimension 2: Concept Coverage

> Does the diagram capture the key concepts and their relationships?

| Score | Description | Example |
|-------|-------------|---------|
| 1 | **Missing key concepts** - Core ideas absent | Diagram about X misses central concept |
| 2 | **Partial coverage** - Some concepts, missing important ones | Has main idea but misses supporting concepts |
| 3 | **Adequate** - Main concepts present, relationships basic | Covers content but surface-level |
| 4 | **Good coverage** - Key concepts and meaningful relationships | Shows how concepts connect |
| 5 | **Comprehensive** - Captures nuances, implicit relationships | Reveals insights not obvious from text |

#### Dimension 3: Information Hierarchy

> Is there clear visual distinction between primary, secondary, and supporting elements?

| Score | Description | Example |
|-------|-------------|---------|
| 1 | **Flat** - Everything looks equally important | All nodes same size/color |
| 2 | **Minimal** - Some hierarchy but unclear | Slight variations but not meaningful |
| 3 | **Adequate** - Primary/secondary distinguishable | Main concept highlighted |
| 4 | **Clear** - Three levels of hierarchy visible | Primary, secondary, supporting clear |
| 5 | **Excellent** - Hierarchy guides eye to key insights | Visual flow leads to understanding |

#### Dimension 4: Genre Appropriateness

> Does the visualization leverage domain conventions and expectations?

| Score | Description | Example |
|-------|-------------|---------|
| 1 | **Generic** - Could be from any domain | Standard flowchart, no domain awareness |
| 2 | **Minimal awareness** - Some domain terms but generic structure | Uses business terms but flowchart structure |
| 3 | **Adequate** - Recognizable as domain content | Looks like a business/technical/etc diagram |
| 4 | **Good fit** - Uses domain conventions | Uses 2x2 matrix for strategy, timeline for history |
| 5 | **Expert level** - Professional in the domain would recognize and appreciate | Uses established frameworks (Porter's, etc.) |

### 2.2 Scoring Template

```markdown
## Track 1 Scoring: [Sample Name]

### Baseline (Generic Prompt)
- Diagram Type Fit: _/5
- Concept Coverage: _/5
- Information Hierarchy: _/5
- Genre Appropriateness: _/5
- **Total: _/20**

Notes:
- [Observations about the diagram]

### Genre-Specific Prompt
- Diagram Type Fit: _/5
- Concept Coverage: _/5
- Information Hierarchy: _/5
- Genre Appropriateness: _/5
- **Total: _/20**

Notes:
- [Observations about the diagram]

### Comparison
- Winner: [Baseline / Genre-Specific / Tie]
- Key difference: [What made the difference]
```

### 2.3 Success Criteria for Track 1

| Criterion | Target | How Measured |
|-----------|--------|--------------|
| Genre-specific scores higher | ≥2 of 3 samples | Total rubric score |
| Genre appropriateness improves | +1 point average | Dimension 4 scores |
| No regression on basics | No dimension scores lower | Compare all dimensions |

**Track 1 POC Success** = Genre-specific approach wins on majority of samples with no significant regressions.

---

## 3. Track 2: Diagram Rendering Evaluation

### 3.1 Automated Metrics

These can be measured programmatically:

| Metric | How to Measure | Target |
|--------|----------------|--------|
| **Render Success** | Did it render without errors? | 100% |
| **File Size** | `ls -la` output file | <50KB |
| **Node Count** | Parse diagram source | Captured for comparison |
| **Edge Count** | Parse diagram source | Captured for comparison |
| **Label Length (avg)** | Parse and calculate | <30 chars average |

#### Automated Check Script

```bash
#!/bin/bash
# Save as: results/track2/measure.sh

echo "=== Rendering Metrics ==="

for tool in mermaid d3 graphviz; do
    echo "\n--- $tool ---"
    if [ -f "$tool/output.svg" ]; then
        echo "Render: SUCCESS"
        echo "Size: $(ls -lh $tool/output.svg | awk '{print $5}')"
    else
        echo "Render: FAILED"
    fi
done
```

### 3.2 Manual Rubric

Score each rendering on these dimensions (1-5 scale):

#### Dimension 1: Visual Clarity

> Can you quickly understand the diagram structure?

| Score | Description |
|-------|-------------|
| 1 | **Confusing** - Hard to follow, overlapping elements |
| 2 | **Cluttered** - Understandable with effort |
| 3 | **Clear** - Structure apparent, some noise |
| 4 | **Very clear** - Easy to follow, good layout |
| 5 | **Excellent** - Instantly comprehensible, guides the eye |

#### Dimension 2: Text Readability

> Are all labels legible at normal viewing size?

| Score | Description |
|-------|-------------|
| 1 | **Illegible** - Text too small, overlapping, or cut off |
| 2 | **Difficult** - Some labels hard to read |
| 3 | **Adequate** - All readable with some strain |
| 4 | **Good** - All labels clear, appropriate sizing |
| 5 | **Excellent** - Perfect typography, easy on eyes |

#### Dimension 3: Aesthetic Appeal

> Is the diagram visually pleasing?

| Score | Description |
|-------|-------------|
| 1 | **Ugly** - Unpleasant colors, poor spacing |
| 2 | **Basic** - Functional but uninspired |
| 3 | **Acceptable** - Looks fine, nothing special |
| 4 | **Attractive** - Pleasing colors, good proportions |
| 5 | **Beautiful** - Professional quality, memorable |

#### Dimension 4: Maintainability

> How easy is it to modify the diagram source?

| Score | Description |
|-------|-------------|
| 1 | **Very hard** - Complex code, fragile |
| 2 | **Difficult** - Requires expertise to modify |
| 3 | **Moderate** - Editable with some learning |
| 4 | **Easy** - Clear structure, self-documenting |
| 5 | **Very easy** - Anyone could modify, text-based |

### 3.3 Effort Tracking

For each tool, also record:

| Metric | Mermaid | D3.js | Graphviz |
|--------|---------|-------|----------|
| Time to create | ___ min | ___ min | ___ min |
| Lines of code | ___ | ___ | ___ |
| External deps needed | ___ | ___ | ___ |
| Learning curve (1-5) | ___ | ___ | ___ |

### 3.4 Scoring Template

```markdown
## Track 2 Scoring: [Diagram Name]

### Mermaid
**Automated:**
- Render Success: Yes/No
- File Size: ___ KB
- Node Count: ___
- Edge Count: ___

**Manual:**
- Visual Clarity: _/5
- Text Readability: _/5
- Aesthetic Appeal: _/5
- Maintainability: _/5
- **Total: _/20**

**Effort:**
- Time: ___ min
- Lines: ___
- Learning: _/5

---

### D3.js
[Same structure]

---

### Graphviz
[Same structure]

---

### Comparison Matrix

| Dimension | Mermaid | D3.js | Graphviz | Winner |
|-----------|---------|-------|----------|--------|
| Visual Clarity | | | | |
| Text Readability | | | | |
| Aesthetic Appeal | | | | |
| Maintainability | | | | |
| Effort (inverse) | | | | |
| **Overall** | | | | |
```

### 3.5 Success Criteria for Track 2

| Criterion | Target | How Measured |
|-----------|--------|--------------|
| All tools render successfully | 100% | Automated check |
| Clear quality ranking emerges | Decisive winner or understood tradeoffs | Manual rubric totals |
| Effort documented | All fields filled | Effort tracking table |

**Track 2 POC Success** = Clear recommendation on which tool to use for which scenarios, with evidence.

---

## 4. Overall POC Success Criteria

### 4.1 Must Have (POC is successful if)

- [ ] **Track 1 completed**: ≥3 samples compared with rubric scores
- [ ] **Track 2 completed**: ≥1 diagram rendered in ≥2 tools with scores
- [ ] **Evidence documented**: All scores captured in `results/` folder
- [ ] **Recommendation made**: Clear next steps based on evidence

### 4.2 Nice to Have

- [ ] Automated metrics script working
- [ ] Side-by-side visual comparison images
- [ ] Cost/benefit analysis written up
- [ ] Updated skill file draft (for future implementation)

### 4.3 Definition of Done

```markdown
POC is DONE when:

1. [ ] samples/ folder has 3 content samples
2. [ ] results/track1/ has 6 diagrams (3 baseline + 3 genre-specific)
3. [ ] results/track1/scores.md has all rubric scores
4. [ ] results/track2/ has 1 diagram in 3 formats
5. [ ] results/track2/scores.md has all rubric scores + effort data
6. [ ] README.md updated with findings and recommendation
7. [ ] Decision made: Proceed with implementation / Pivot / Need more data
```

---

## 5. Test Protocol

### 5.1 Pre-Experiment Checklist

- [ ] SPEC.md reviewed and understood
- [ ] EVAL.md reviewed and understood
- [ ] Sample content extracted to `samples/`
- [ ] Folder structure created per SPEC.md

### 5.2 Track 1 Protocol

```
For each sample (S1, S2, S3):

1. BASELINE GENERATION
   a. Read sample content
   b. Use generic book-to-visual-companion prompt
   c. Generate Mermaid diagram
   d. Save to results/track1/baseline/sX-baseline.md
   e. Verify diagram renders

2. GENRE-SPECIFIC GENERATION
   a. Read same sample content
   b. Identify genre (business/technical/narrative/philosophical)
   c. Use genre-specific prompt from SPEC.md Section 4
   d. Generate Mermaid diagram
   e. Save to results/track1/genre-specific/sX-genre.md
   f. Verify diagram renders

3. SCORING
   a. Open both diagrams side by side
   b. Score baseline using rubric (Section 2.1)
   c. Score genre-specific using rubric (Section 2.1)
   d. Record in results/track1/scores.md
   e. Note observations and reasoning
```

### 5.3 Track 2 Protocol

```
1. SELECT DIAGRAM
   a. Choose one diagram from Track 1 results
   b. Preference: One that has moderate complexity (5-10 nodes)

2. MERMAID (baseline)
   a. Use existing Mermaid code
   b. Render to SVG
   c. Save to results/track2/mermaid/
   d. Record time spent

3. D3.JS
   a. Look up D3.js documentation via Context7
   b. Recreate equivalent diagram
   c. Render to SVG/HTML
   d. Save to results/track2/d3/
   e. Record time spent and lines of code

4. GRAPHVIZ
   a. Look up Graphviz DOT syntax via Context7
   b. Recreate equivalent diagram
   c. Render to SVG (using `dot -Tsvg`)
   d. Save to results/track2/graphviz/
   e. Record time spent and lines of code

5. SCORING
   a. Run automated metrics script
   b. Score each on manual rubric (Section 3.2)
   c. Fill in effort tracking table
   d. Record in results/track2/scores.md
```

---

## 6. Evaluation Outputs

After completing the POC, we should have:

```
results/
├── track1/
│   ├── baseline/
│   │   ├── s1-baseline.md      # Mermaid diagram + rendered preview
│   │   ├── s2-baseline.md
│   │   └── s3-baseline.md
│   ├── genre-specific/
│   │   ├── s1-genre.md
│   │   ├── s2-genre.md
│   │   └── s3-genre.md
│   └── scores.md               # All Track 1 rubric scores
└── track2/
    ├── mermaid/
    │   └── output.svg
    ├── d3/
    │   ├── diagram.js
    │   └── output.svg (or .html)
    ├── graphviz/
    │   ├── diagram.dot
    │   └── output.svg
    ├── scores.md               # All Track 2 scores + effort
    └── measure.sh              # Automated metrics script
```

---

## 7. Decision Framework

After scoring, use this framework to decide:

### Track 1 Decision

| Result | Decision |
|--------|----------|
| Genre-specific wins 3/3 samples | **Implement**: Update skill with genre-specific prompts |
| Genre-specific wins 2/3 samples | **Implement with caution**: Update skill, monitor results |
| Tie or mixed results | **Iterate**: Refine prompts, test more samples |
| Baseline wins | **Keep current**: Generic approach is sufficient |

### Track 2 Decision

| Result | Decision |
|--------|----------|
| Clear winner on quality AND effort | **Adopt**: Use winner for all diagrams |
| Winner on quality, high effort | **Selective use**: Use for hero diagrams only |
| Mermaid competitive | **Keep Mermaid**: Effort savings outweigh quality gap |
| All tools similar | **Keep Mermaid**: Simplicity wins |

### Overall Recommendation Template

```markdown
## POC Recommendation

### Track 1: Diagram Logic
- **Finding**: [Genre-specific / Generic] approach produced better results
- **Evidence**: [X/3 samples scored higher, +Y points average]
- **Recommendation**: [Implement / Iterate / Keep current]

### Track 2: Diagram Rendering
- **Finding**: [Tool] offers best quality/effort balance
- **Evidence**: [Scores and effort data]
- **Recommendation**: [Adopt / Selective use / Keep Mermaid]

### Next Steps
1. [Specific action]
2. [Specific action]
3. [Specific action]
```

---

## 8. Appendix: Blank Scoring Sheets

### Track 1 Blank Score Sheet

```markdown
## Sample: _______________
## Genre: _______________

### Baseline
| Dimension | Score | Notes |
|-----------|-------|-------|
| Diagram Type Fit | /5 | |
| Concept Coverage | /5 | |
| Information Hierarchy | /5 | |
| Genre Appropriateness | /5 | |
| **TOTAL** | /20 | |

### Genre-Specific
| Dimension | Score | Notes |
|-----------|-------|-------|
| Diagram Type Fit | /5 | |
| Concept Coverage | /5 | |
| Information Hierarchy | /5 | |
| Genre Appropriateness | /5 | |
| **TOTAL** | /20 | |

### Winner: _______________
```

### Track 2 Blank Score Sheet

```markdown
## Diagram: _______________

### Automated Metrics
| Metric | Mermaid | D3.js | Graphviz |
|--------|---------|-------|----------|
| Render Success | | | |
| File Size (KB) | | | |
| Node Count | | | |
| Edge Count | | | |

### Manual Scores
| Dimension | Mermaid | D3.js | Graphviz |
|-----------|---------|-------|----------|
| Visual Clarity | /5 | /5 | /5 |
| Text Readability | /5 | /5 | /5 |
| Aesthetic Appeal | /5 | /5 | /5 |
| Maintainability | /5 | /5 | /5 |
| **TOTAL** | /20 | /20 | /20 |

### Effort
| Metric | Mermaid | D3.js | Graphviz |
|--------|---------|-------|----------|
| Time (min) | | | |
| Lines of Code | | | |
| Learning Curve | /5 | /5 | /5 |

### Winner: _______________
```
