# 🔨 Structurist Forge: Narrative Architecture Workspace

**App Type**: Role-Based Tool  
**Role**: STRUCTURIST  
**Universe**: 📖 STORY_ENGINE  
**Key Question**: "What happens, to whom, and why does it matter?"

---

## 🎯 Purpose

The **Structurist Forge** is where narrative architecture takes shape. Here, users define the **meaning** of their story—story points, beats, character arcs, thematic throughlines—independent of how it will eventually be told.

This is the **skeleton** of story: the underlying logic that makes narrative coherent.

---

## 🌟 Core Features

### 1. Story Point Editor
Define the major structural waypoints:
- **Inciting Incident**: What disrupts the ordinary world
- **Progressive Complications**: Rising tension beats
- **Climax**: Point of no return
- **Resolution**: New equilibrium

Each point includes:
- Title and description
- Associated beats (expandable)
- Thematic anchor (what meaning this point carries)
- Character positions (who is where in their arc)

### 2. Beat Timeline
Visual representation of narrative sequence:
- **Horizontal timeline** with beats as nodes
- **Bézier connectors** showing causal relationships
- **Color coding** by narrative function (setup, confrontation, resolution)
- **Zoom levels**: Overview → Detail → Beat focus

### 3. Character Arc Mapper
Track character transformation:
- **Arc start state** → **Arc end state**
- **Key moments** pinned to beats
- **Emotional trajectory** curve
- **Relationship evolution** with other characters

### 4. Theme Weaver
Manage thematic throughlines:
- **Theme definition**: Name + core question
- **Strength tracking**: How present is theme in each beat
- **Echo detection**: Where themes reinforce each other
- **Absence alerts**: Beats where expected theme is missing

### 5. Dependency Graph
Visualize narrative causality:
- **If Beat A changes, which beats are affected?**
- **Constraint propagation** preview
- **Coherence scoring** for structural integrity

---

## 📐 UI Structure

```
┌─────────────────────────────────────────────────────────────────┐
│  🔨 Structurist Forge    [New Point] [Add Beat] [Export NCP]   │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  STORY GRAPH (Timeline View)                                   │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │                                                         │   │
│  │  ○━━━━○━━━━○━━━━●━━━━○━━━━○━━━━○━━━━●━━━━○━━━━○       │   │
│  │  │    │    │    │    │    │    │    │    │    │       │   │
│  │  1    2    3    4    5    6    7    8    9    10      │   │
│  │  Setup      Rising Action    Climax    Resolution     │   │
│  │                                                         │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
├─────────────────┬───────────────────────────────────────────────┤
│  STORY POINTS   │  FOCUSED BEAT                                │
│                 │                                               │
│  ◆ Inciting     │  Beat #4: "The Wound Revealed"               │
│    [2 beats]    │  ─────────────────────────────────           │
│                 │  Summary: Protagonist discovers the betrayal  │
│  ◆ Midpoint     │                                               │
│    [3 beats]    │  Narrative Function: [Revelation ▼]          │
│                 │  Appreciation: [Progression ▼]               │
│  ◆ Climax       │                                               │
│    [2 beats]    │  Characters Present:                         │
│                 │  ┌────────────┐ ┌────────────┐               │
│  ◆ Resolution   │  │ Elena      │ │ Marcus     │               │
│    [1 beat]     │  │ Arc: 0.35  │ │ Arc: 0.40  │               │
│                 │  └────────────┘ └────────────┘               │
├─────────────────┤                                               │
│  THEMES         │  Theme Resonance:                            │
│                 │  ■■■■■□□□ Power of Love (62%)                │
│  ● Betrayal     │  ■■■□□□□□ Trust (38%)                        │
│  ● Redemption   │                                               │
│  ● Trust        │  Dependencies: ← Beat 3 | → Beat 5, 7       │
│                 │                                               │
├─────────────────┴───────────────────────────────────────────────┤
│  TRINITY STRUCTURAL ANALYSIS                                    │
│  ┌───────────────────────────────────────────────────────────┐ │
│  │ 🧠 Mia: "This beat logically follows from Beat 3's       │ │
│  │ discovery. The causal chain is sound. Consider adding    │ │
│  │ explicit stakes to strengthen the progression."           │ │
│  ├───────────────────────────────────────────────────────────┤ │
│  │ 🌸 Miette: "The emotional weight here is heavy—perfect   │ │
│  │ for this position. Elena's arc needs this wound to       │ │
│  │ justify her later transformation."                        │ │
│  ├───────────────────────────────────────────────────────────┤ │
│  │ 🎨 Ava8: "Atmospherically, this beat wants darkness—     │ │
│  │ consider visual motifs of shadows, mirrors, or shattered │ │
│  │ glass to echo the internal fracturing."                   │ │
│  └───────────────────────────────────────────────────────────┘ │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🔧 Technical Requirements

### Data Model
```typescript
interface NarrativeStructure {
  id: string;
  storyId: string;
  storyPoints: StoryPoint[];
  beats: StoryBeat[];
  characters: CharacterArc[];
  themes: ThematicThread[];
  dependencies: BeatDependency[];
}

interface StoryPoint {
  id: string;
  type: 'inciting' | 'midpoint' | 'climax' | 'resolution' | 'custom';
  title: string;
  description: string;
  beatIds: string[];
  thematicAnchor: string;
}

interface StoryBeat {
  id: string;
  sequence: number;
  summary: string;
  narrative_function: 'setup' | 'development' | 'revelation' | 'crisis' | 'resolution';
  appreciation: 'progression' | 'change' | 'static';
  characterPositions: { characterId: string; arcPosition: number }[];
  themeResonance: { themeId: string; strength: number }[];
  tone: {
    abstraction: number; // 0-100
    spatial: number;
    temporal: number;
  };
}

interface CharacterArc {
  id: string;
  name: string;
  archetype: 'mia' | 'miette' | 'ava8' | 'custom';
  startState: string;
  endState: string;
  keyMoments: { beatId: string; description: string }[];
  relationships: { characterId: string; evolution: string[] }[];
}

interface ThematicThread {
  id: string;
  name: string;
  coreQuestion: string;
  presenceByBeat: { beatId: string; strength: number }[];
}

interface BeatDependency {
  fromBeatId: string;
  toBeatId: string;
  type: 'causes' | 'enables' | 'contrasts' | 'echoes';
}
```

### AI Integration
```typescript
// Generate Trinity analysis for a beat
async function analyzeBeat(
  beat: StoryBeat,
  context: { prevBeat?: StoryBeat; nextBeat?: StoryBeat; themes: ThematicThread[] }
): Promise<{
  mia: string;   // Structural/logical analysis
  miette: string; // Emotional/arc analysis
  ava8: string;   // Atmospheric/sensory suggestions
}>

// Check arc coherence
async function validateCharacterArc(arc: CharacterArc, beats: StoryBeat[]): Promise<{
  coherent: boolean;
  gaps: string[];
  suggestions: string[];
}>

// Detect thematic echoes
async function findThematicEchoes(themes: ThematicThread[], beats: StoryBeat[]): Promise<{
  echoes: { beat1: string; beat2: string; theme: string; strength: number }[];
  absences: { beatId: string; expectedTheme: string }[];
}>
```

---

## 🎨 Design Language

### Colors
- **Timeline**: Gradient from amber (beginning) to violet (end)
- **Beat nodes**: Sized by importance, colored by function
- **Arc curves**: Character-specific colors with opacity for intensity
- **Theme bars**: Hue mapped to theme category

### Interactions
- **Click beat** to focus and see details
- **Drag beat** to reorder (with dependency impact preview)
- **Connect beats** by drawing dependency arrows
- **Double-click theme** to edit resonance across all beats
- **Hover character** to highlight their arc on timeline

---

## 📊 Roadmap

### Phase 1: Core Structure
- [ ] Story point CRUD
- [ ] Beat timeline with basic editing
- [ ] Sequence management
- [ ] NCP JSON export

### Phase 2: Character & Theme
- [ ] Character arc mapper
- [ ] Theme weaver
- [ ] Resonance tracking
- [ ] Arc visualization

### Phase 3: Dependencies
- [ ] Dependency graph view
- [ ] Constraint propagation
- [ ] Impact preview on edit
- [ ] Coherence scoring

### Phase 4: Trinity Integration
- [ ] Beat-level Trinity analysis
- [ ] Character arc validation
- [ ] Thematic echo detection
- [ ] Unified synthesis panel

---

## 🔗 Dependencies

### Required Rispecs
- [ncp-schema.rispec.md](ncp-schema.rispec.md) - Beat, Character, Theme types
- [storytelling-roles-tooling.rispec.md](storytelling-roles-tooling.rispec.md) - STRUCTURIST role
- [narrative-intelligence.langgraph.rispec.md](narrative-intelligence.langgraph.rispec.md) - CharacterArcGenerator, ThematicAnalyzer

### Consumes From
- **Architect Studio**: Schema definitions

### Produces For
- **Storyteller Loom**: Structured beats ready for prose
- **Editor Anvil**: Structural context for quality analysis

---

## 💡 Key Innovation

**Dependency-Aware Editing**: Unlike simple beat lists, the Structurist Forge understands that narrative elements are causally connected. When you edit Beat 4, it shows you exactly which downstream beats may need revision—preventing the "domino collapse" of inconsistent stories.

---

*"Structure is not constraint—it is the trellis on which meaning climbs toward the light." — Miette 🌸*
