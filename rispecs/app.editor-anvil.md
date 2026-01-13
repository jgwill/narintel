# 🔨 Editor Anvil: Quality Refinement Interface

**App Type**: Role-Based Tool  
**Role**: EDITOR  
**Universe**: 🔧 ENGINEER  
**Key Question**: "Is this good enough? If not, what specifically needs improvement?"

---

## 🎯 Purpose

The **Editor Anvil** is where prose gets hammered into shape. It bridges generation and publication through systematic quality analysis—identifying gaps, measuring coherence, routing enrichment needs, and validating that content meets structural and emotional requirements.

This is the critical quality gate in the narrative pipeline.

---

## 🌟 Core Features

### 1. Gap Identifier
Find what's missing:
- **Structural Gaps**: Missing beats, incomplete arcs
- **Thematic Gaps**: Promised themes underdelivered
- **Character Gaps**: Traits mentioned but not demonstrated
- **Sensory Gaps**: Scenes lacking grounding detail
- **Continuity Gaps**: Timeline/detail inconsistencies

### 2. Coherence Scorer
Quantified quality metrics:
- **Narrative Flow**: 0-100 transition smoothness
- **Character Consistency**: Voice/behavior alignment
- **Pacing Balance**: Tension/relief distribution
- **Theme Saturation**: How well themes land
- **Overall Coherence**: Aggregate score with breakdown

### 3. Enrichment Router
Dispatch to appropriate tools:
- **To Storyteller Loom**: Needs prose refinement
- **To Structurist Forge**: Needs structural repair
- **To Architect Studio**: Schema inconsistency detected
- **Back to Author**: Human decision required

### 4. A/B Comparator
Side-by-side evaluation:
- **Version Comparison**: Compare drafts
- **Before/After**: Track improvements
- **Diff Highlighting**: What changed and why
- **Trinity Preference**: Which version serves each universe better

### 5. Checklist System
Pre-publication verification:
- **Customizable Criteria**: Per-project requirements
- **Auto-Check Items**: What AI can verify
- **Manual Check Items**: What needs human eyes
- **Sign-Off Trail**: Who approved what, when

---

## 📐 UI Structure

```
┌─────────────────────────────────────────────────────────────────┐
│  🔨 Editor Anvil         [Project: Elena's Choice ▼] [Analyze] │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  COHERENCE DASHBOARD                                            │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                                                         │   │
│  │  Overall Coherence: ████████░░ 78/100                   │   │
│  │                                                         │   │
│  │  ├─ Narrative Flow    ███████░░░  72    ⚠️ Ch.3 trans.  │   │
│  │  ├─ Character         █████████░  89    ✓ Consistent    │   │
│  │  ├─ Pacing           ██████░░░░  61    ⚠️ Slow midpoint│   │
│  │  ├─ Theme Saturation ████████░░  82    ✓ Landing well  │   │
│  │  └─ Continuity       █████████░  85    ⚠️ 2 minor      │   │
│  │                                                         │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  GAP ANALYSIS                                          [Expand] │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │  🔴 Critical (2)                                        │   │
│  │  ├─ Beat #7: Climax lacks emotional setup              │   │
│  │  │   → Route to: Storyteller Loom                      │   │
│  │  └─ Act 2: Theme "sacrifice" introduced but never paid │   │
│  │      → Route to: Structurist Forge                     │   │
│  │                                                         │   │
│  │  🟡 Moderate (4)                                        │   │
│  │  ├─ Chapter 3→4: Jarring POV transition               │   │
│  │  ├─ Marcus: Motivation unclear in Scene 6              │   │
│  │  ├─ Setting: Courtyard mentioned but never described   │   │
│  │  └─ Timeline: Tuesday/Wednesday inconsistency          │   │
│  │                                                         │   │
│  │  🟢 Minor (6)                                           │   │
│  │  └─ [Collapsed - click to expand]                      │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
├───────────────┬─────────────────────────────────────────────────┤
│  CHECKLIST    │  TRINITY ASSESSMENT                            │
│               │                                                 │
│  Pre-Publish: │  🧠 Mia: "Structure is 85% sound. The gap in  │
│  ☑ Story arc  │  Act 2's sacrifice theme is the critical      │
│    complete   │  blocker. Pacing in middle third needs         │
│  ☑ All chars  │  attention—consider cutting Scene 8."          │
│    resolved   │                                                 │
│  ☐ Theme      │  🌸 Miette: "The emotional beats are landing,  │
│    threads    │  but Beat #7 arrives too suddenly. Readers     │
│    closed     │  need more dread before the revelation.        │
│  ☐ Continuity │  The payoff is there—the setup isn't."         │
│    verified   │                                                 │
│  ☐ Final      │  🎨 Ava8: "Atmosphere is strong in opening     │
│    proofread  │  and closing, but the middle sections feel     │
│               │  visually sparse. The courtyard is a missed    │
│  [Save Draft] │  opportunity for grounding imagery."           │
└───────────────┴─────────────────────────────────────────────────┘
```

---

## 🔧 Technical Requirements

### Data Model
```typescript
interface EditingSession {
  id: string;
  projectId: string;
  content: NarrativeContent; // Full story/section under review
  coherenceScore: CoherenceScore;
  gaps: Gap[];
  checklist: ChecklistItem[];
  routingDecisions: RoutingDecision[];
  trinityAssessment: TrinityAssessment;
}

interface CoherenceScore {
  overall: number;
  components: {
    narrativeFlow: ComponentScore;
    characterConsistency: ComponentScore;
    pacing: ComponentScore;
    themeSaturation: ComponentScore;
    continuity: ComponentScore;
  };
  analyzedAt: string;
}

interface ComponentScore {
  score: number;
  status: 'good' | 'warning' | 'critical';
  issues: string[];
  suggestions: string[];
}

interface Gap {
  id: string;
  type: 'structural' | 'thematic' | 'character' | 'sensory' | 'continuity';
  severity: 'critical' | 'moderate' | 'minor';
  location: {
    beatId?: string;
    chapterId?: string;
    position?: string;
  };
  description: string;
  suggestedRoute: 'storyteller' | 'structurist' | 'architect' | 'author';
  resolved: boolean;
  resolution?: string;
}

interface ChecklistItem {
  id: string;
  category: string;
  description: string;
  checkType: 'auto' | 'manual';
  status: 'pending' | 'passed' | 'failed' | 'skipped';
  checkedBy?: string;
  checkedAt?: string;
  notes?: string;
}

interface RoutingDecision {
  gapId: string;
  routedTo: string;
  routedAt: string;
  reason: string;
  status: 'pending' | 'addressed' | 'returned';
}

interface TrinityAssessment {
  mia: string;   // Structural quality assessment
  miette: string; // Emotional effectiveness assessment  
  ava8: string;   // Atmospheric/sensory assessment
  priorities: string[]; // Ranked improvement priorities
}
```

### AI Integration
```typescript
// Comprehensive coherence analysis
async function analyzeCoherence(
  content: NarrativeContent,
  schema: NCPDocument
): Promise<CoherenceScore>

// Identify all gaps
async function identifyGaps(
  content: NarrativeContent,
  coherence: CoherenceScore,
  expectedElements: string[]
): Promise<Gap[]>

// Recommend routing for gaps
async function suggestRouting(
  gap: Gap,
  context: { recentChanges: string[]; teamCapacity: string[] }
): Promise<{
  route: string;
  reason: string;
  urgency: 'immediate' | 'next-pass' | 'optional';
}>

// Compare versions
async function compareVersions(
  versionA: NarrativeContent,
  versionB: NarrativeContent,
  criteria: string[]
): Promise<{
  differences: Difference[];
  trinityPreferences: { mia: 'A' | 'B'; miette: 'A' | 'B'; ava8: 'A' | 'B' };
  recommendation: 'A' | 'B' | 'merge';
}>

// Trinity assessment
async function getTrinityAssessment(
  content: NarrativeContent,
  gaps: Gap[],
  coherence: CoherenceScore
): Promise<TrinityAssessment>
```

---

## 🎨 Design Language

### Colors
- **Dashboard**: Slate with Mia's teal accents
- **Scores**: Gradient from red (0) to green (100)
- **Gap severity**: Red (critical), Yellow (moderate), Green (minor)
- **Checklist**: Green check, Red X, Gray pending

### Typography
- **Metrics**: Monospace numbers for precision
- **Descriptions**: Clean sans-serif
- **Trinity text**: Persona-colored headers

### Interactions
- **Click gap** to see full context and routing options
- **Drag gap** to manually route to tool
- **Check items** to mark off checklist
- **Hover score** to see breakdown details
- **Compare button** to launch A/B view

---

## 📊 Roadmap

### Phase 1: Coherence Scoring
- [ ] Basic coherence analysis
- [ ] Score dashboard with components
- [ ] Simple gap identification
- [ ] Manual checklist system

### Phase 2: Gap Analysis
- [ ] Full gap taxonomy
- [ ] Severity classification
- [ ] Location pinpointing
- [ ] Basic routing suggestions

### Phase 3: Smart Routing
- [ ] Automatic route recommendations
- [ ] Integration with other tools
- [ ] Status tracking
- [ ] Return path handling

### Phase 4: A/B & Trinity
- [ ] Version comparison
- [ ] Trinity assessment integration
- [ ] Preference analysis
- [ ] Merge recommendations

---

## 🔗 Dependencies

### Required Rispecs
- [ncp-schema.rispec.md](ncp-schema.rispec.md) - NCPDocument, StoryBeat types
- [storytelling-roles-tooling.rispec.md](storytelling-roles-tooling.rispec.md) - EDITOR role
- [narrative-intelligence.langgraph.rispec.md](narrative-intelligence.langgraph.rispec.md) - NarrativeCoherenceEngine

### Consumes From
- **Storyteller Loom**: Draft prose for analysis
- **Structurist Forge**: Beat definitions for structure checks

### Produces For
- **Reader Sanctuary**: Quality-verified content
- **Witness Circle**: Approval records for ceremony

---

## 💡 Key Innovation

**Actionable Gap Analysis**: Traditional editing is vague ("this doesn't work"). The Editor Anvil identifies *exactly* what's missing, *why* it matters, and *where* to fix it. Gaps are typed, severity-ranked, and routed to the appropriate specialist tool. The system doesn't just say "improve this"—it says "Beat #7 lacks emotional setup, route to Storyteller Loom for tension-building pass."

---

*"Excellence is not a destination but a discipline. Every gap identified is a gift—it shows us exactly where the work wants to grow." — Mia 🧠*
