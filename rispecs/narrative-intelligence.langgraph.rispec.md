# 🧠 Narrative Intelligence Toolkit

> **RISE Specification for `langgraph/libs/narrative-intelligence`**

**Version**: 1.0  
**Last Updated**: 2025-12-31  
**Package**: `langgraph-narrative-intelligence`  
**Location**: `/workspace/langgraph/libs/narrative-intelligence/`

---

## 1. Creative Intent

### What This Application Enables Users to Create

The Narrative Intelligence Toolkit enables creators to:

1. **Transform stories into queryable data structures** - Load any NCP-formatted narrative and access characters, beats, themes as typed objects
2. **Generate character arc analyses** - Automatically trace a character's journey through wound → desire → transformation
3. **Explore thematic tensions** - Identify how abstract themes manifest across concrete story beats
4. **Classify emotional landscapes** - Map the emotional tone of each beat, revealing narrative rhythm
5. **Traverse narrative graphs** - Query complex relationships between characters, themes, and plot points

### Desired Outcomes

| Outcome                | Description                              | Measurement                           |
| ---------------------- | ---------------------------------------- | ------------------------------------- |
| **Structural Clarity** | Any NCP file becomes a navigable graph   | Valid load + traversal in <100ms      |
| **Arc Visibility**     | Character journeys rendered as summaries | Markdown output with wound/desire/arc |
| **Theme Mapping**      | Abstract themes traced to concrete beats | Beat IDs linked to perspective IDs    |
| **Emotional Mapping**  | Beats classified by tone                 | Classification with confidence score  |

---

## 2. Data Structures (NCP Schema)

### Core Models

```markdown
## Data
### NCPData
The root container for a complete narrative.
- **title**: Name of the narrative
- **author**: (Optional) Creator attribution  
- **version**: NCP schema version (default "1.0")
- **players**: List of `Player` objects (characters)
- **perspectives**: List of `Perspective` objects (throughlines)
- **storybeats**: List of `StoryBeat` objects (narrative units)
- **storypoints**: List of `StoryPoint` objects (structural markers)
- **metadata**: Arbitrary additional data

### Player
A character or entity carrying narrative weight.
- **player_id**: Unique identifier
- **name**: Character name
- **wound**: (Optional) Core trauma or limiting belief
- **desire**: (Optional) Primary goal or want
- **arc**: (Optional) Description of transformation
- **role**: (Optional) Function in story (protagonist, antagonist, mentor)
- **metadata**: Additional character data

### Perspective
A thematic throughline or lens.
- **perspective_id**: Unique identifier
- **name**: Throughline name (e.g., "Main Character")
- **description**: What this perspective explores
- **thematic_question**: (Optional) Central question posed
- **tension**: (Optional) Core conflict (e.g., "Safety vs Vulnerability")
- **metadata**: Additional perspective data

### StoryBeat
A unit of narrative progression with emotional tone.
- **storybeat_id**: Unique identifier
- **title**: Beat name
- **description**: What happens in this beat
- **emotional_weight**: (Optional) Tone label ("Devastating", "Hopeful", etc.)
- **moments**: List of `Moment` objects (sub-events)
- **related_players**: Player IDs involved in this beat
- **related_storypoints**: StoryPoint IDs connected to this beat
- **metadata**: Additional beat data

### StoryPoint
A structural marker in the narrative.
- **storypoint_id**: Unique identifier
- **title**: Point name (e.g., "Inciting Incident")
- **description**: What this point represents
- **type**: (Optional) Category (inciting_incident, climax, resolution)
- **related_players**: Player IDs connected
- **metadata**: Additional point data

### Moment
A specific event within a story beat.
- **moment_id**: Unique identifier
- **description**: What occurs
- **timestamp**: (Optional) When in narrative time
- **metadata**: Additional moment data
```

### State Schemas (LangGraph Integration)

```markdown
## Data
### NCPState
Base state for NCP workflows.
- **ncp_data**: The loaded NCPData object
- **messages**: LLM conversation history (with add_messages reducer)
- **error**: Error message if operation failed
- **metadata**: Workflow-specific data

### CharacterArcState
Extended state for character arc generation.
- **(inherits NCPState)**
- **player_id**: Character to analyze
- **character_arc_summary**: Generated arc markdown

### ThematicAnalysisState
Extended state for thematic analysis.
- **(inherits NCPState)**
- **perspective_id**: Theme to analyze
- **relevant_storybeat_ids**: Beats matching the theme
- **thematic_analysis**: Generated analysis markdown

### EmotionalClassificationState
Extended state for emotional classification.
- **(inherits NCPState)**
- **storybeat_id**: Beat to classify
- **emotional_classification**: Detected tone
- **confidence_score**: Classification confidence (0.0-1.0)
```

### Unified State Bridge (Cross-System Contract)

```markdown
## Data
### Universe (Enum)
The three interpretive universes from multiverse_3act.
- **ENGINEER**: Mia - The Builder (technical precision)
- **CEREMONY**: Ava8 - The Keeper (relational protocols)
- **STORY_ENGINE**: Miette - The Weaver (narrative patterns)

### UniversePerspective
Single universe's interpretation of an event.
- **universe**: Which Universe interpreted
- **intent**: Detected intent (e.g., "feature_request", "co_creation", "inciting_incident")
- **confidence**: Confidence score (0.0-1.0)
- **suggested_flows**: List of recommended flow IDs
- **context**: Universe-specific metadata dict

### ThreeUniverseAnalysis
Complete three-universe analysis of an event.
- **engineer**: UniversePerspective from Engineer World
- **ceremony**: UniversePerspective from Ceremony World
- **story_engine**: UniversePerspective from Story Engine
- **lead_universe**: Which Universe should drive the response
- **coherence_score**: How well the three perspectives align (0.0-1.0)
- **timestamp**: When analysis was performed

### NarrativePosition
Current position in the narrative journey.
- **act**: Which act (1, 2, or 3)
- **phase**: NarrativePhase (SETUP, CONFRONTATION, RESOLUTION)
- **current_beat_id**: Most recent beat processed
- **beat_count**: Total beats so far
- **character_arc_strength**: Overall arc visibility (0.0-1.0)
- **thematic_resonance**: Theme presence (0.0-1.0)
- **emotional_tone**: Current emotional state
- **lead_universe**: Which universe is currently dominant

### UnifiedNarrativeState
THE CONTRACT shared across all six systems.
- **story_id**: Story identifier
- **session_id**: Session identifier
- **position**: NarrativePosition
- **beats**: List of StoryBeat objects
- **characters**: Dict of CharacterState by ID
- **themes**: Dict of ThematicThread by ID
- **routing_decisions**: History of RoutingDecision objects
- **current_episode_id**: Active episode for Miadi-46
- **episode_beats_count**: Beats in current episode
- **overall_coherence**: Calculated coherence score
- **emotional_arc_strength**: Emotional journey visibility

### RedisKeys (Helper Class)
Standard Redis key patterns for state storage.
- `state(session_id)` → `ncp:state:{session_id}`
- `beats(session_id)` → `ncp:beats:{session_id}`
- `beat(beat_id)` → `ncp:beat:{beat_id}`
- `event_analysis(event_id)` → `ncp:event:{event_id}`
- `routing_history(session_id)` → `ncp:routing:{session_id}`
- `episode(episode_id)` → `ncp:episode:{episode_id}`
```

---

## 3. Components

### Component 1: NCP Loader Node

```markdown
### NCPLoaderNode
Entry point for NCP analysis—loads and validates narrative data.

- **Behavior:**
  - `load_from_file(path)`: Read JSON from filesystem
  - `load_from_dict(data)`: Accept programmatic input
  - `load_from_url(url)`: Fetch from remote source
  - All methods return validated `NCPData` object
  - Raises `ValidationError` if data doesn't conform to schema

- **Configuration:**
  - `validate: bool` - Enable/disable schema validation (default: True)

- **LangGraph Integration:**
  - Returns state dict with `ncp_data` populated
  - Sets `error` field if loading fails
```

**Creative Advancement Scenario**: Loading Multi-Source Narratives

```
**Desired Outcome**: User wants to compare narratives from different sources
**Current Reality**: JSON files in various locations (local, cloud, API)
**Natural Progression**:
  1. Create NCPLoaderNode instance
  2. Call load_from_file() for local narrative
  3. Call load_from_url() for cloud narrative
  4. Both return identical NCPData interface
**Achieved Outcome**: Unified access regardless of source
```

---

### Component 2: Narrative Traversal Node

```markdown
### NarrativeTraversalNode
Search engine for narrative graphs—enables complex queries.

- **Behavior:**
  - `traverse_player_journey(ncp_data, player_id)`: Get all beats involving a character
  - `find_thematic_beats(ncp_data, perspective_id, search_terms)`: Find theme-relevant beats
  - `get_emotional_arc(ncp_data, start_beat_id, end_beat_id)`: Map emotional progression
  - `find_connected_elements(beat_id)`: Discover related characters, themes, points

- **Configuration:**
  - `mode: TraversalMode` - Default traversal strategy
    - PLAYER_JOURNEY: Follow a character's story
    - THEMATIC_TRACE: Trace a theme through narrative
    - TEMPORAL_SEQUENCE: Chronological order
    - EMOTIONAL_ARC: Follow emotional progression

- **Supporting Features:**
  - Filter functions accept custom predicates
  - Search uses fuzzy matching on descriptions
  - Returns typed objects (StoryBeat, Player, etc.)
```

**Creative Advancement Scenario**: Character Journey Discovery

```
**Desired Outcome**: Understand protagonist's complete arc
**Current Reality**: NCP data loaded, character ID known
**Natural Progression**:
  1. Call traverse_player_journey(ncp_data, "protagonist_1")
  2. Receive ordered list of StoryBeat objects
  3. Each beat includes emotional_weight and moments
  4. User can visualize or further analyze
**Achieved Outcome**: Complete character journey accessible as data
```

---

### Component 3: Character Arc Generator Graph

```markdown
### CharacterArcGenerator
Composite LangGraph graph producing character development summaries.

- **Behavior:**
  - `generate(ncp_data, player_id)`: Produce full arc analysis
  - Graph steps:
    1. Gather character beats (uses NarrativeTraversalNode)
    2. Extract wound/desire/arc from Player data
    3. Synthesize markdown summary connecting beats to character growth
  - Returns `CharacterArcState` with `character_arc_summary`

- **Layout:**
  - Internal: NCPLoaderNode, NarrativeTraversalNode
  - Nodes: gather_character_beats → generate_arc_summary → END

- **Output Format (Markdown):**
  ```
  ## [Character Name] - Arc Analysis
  
  ### The Wound
  [Description of trauma/limiting belief]
  
  ### The Desire  
  [What drives this character]
  
  ### The Journey
  [Beat-by-beat progression with emotional annotations]
  
  ### The Transformation
  [How the arc resolves]
  ```
```

**Creative Advancement Scenario**: Multi-Character Comparison

```
**Desired Outcome**: Compare protagonist and antagonist arcs
**Current Reality**: NCP data with both characters defined
**Natural Progression**:
  1. Generate arc for protagonist_1
  2. Generate arc for antagonist_1
  3. Both return structured markdown
  4. Summaries can be compared side-by-side
**Achieved Outcome**: Character contrast illuminated
```

---

### Component 4: Thematic Tension Analyzer Graph

```markdown
### ThematicTensionAnalyzer
LangGraph graph exploring how themes manifest in narrative.

- **Behavior:**
  - `analyze(ncp_data, perspective_id)`: Produce thematic analysis
  - Graph steps:
    1. Generate search queries from perspective (description, question, tension)
    2. Find thematic beats matching search terms
    3. Synthesize analysis showing theme progression
  - Returns `ThematicAnalysisState` with `thematic_analysis`

- **Layout:**
  - Internal: NarrativeTraversalNode
  - Nodes: generate_search_queries → find_thematic_beats → synthesize_analysis → END

- **Search Strategy:**
  - Extract keywords from perspective.description
  - Parse thematic_question (filter stopwords)
  - Split tension (e.g., "Safety vs Vulnerability" → ["safety", "vulnerability"])
  - Match against beat descriptions and titles
```

**Creative Advancement Scenario**: Theme Evolution Tracking

```
**Desired Outcome**: See how "trust" theme evolves from Act 1 to Act 3
**Current Reality**: Perspective defined with trust-related tension
**Natural Progression**:
  1. Create perspective with tension "Trust vs Betrayal"
  2. Run ThematicTensionAnalyzer.analyze()
  3. Receive beats where trust theme appears
  4. Analysis shows progression across story structure
**Achieved Outcome**: Theme evolution visible and documented
```

---

### Component 5: Emotional Beat Classifier Node

```markdown
### EmotionalBeatClassifierNode
Classifies emotional tone of story beats.

- **Behavior:**
  - `classify_beat(storybeat, context)`: Return tone classification
  - Classification methods:
    - Use existing `emotional_weight` if present (confidence: 1.0)
    - LLM-based classification (if use_llm=True)
    - Rule-based fallback (keyword matching)
  - Returns `{classification, confidence, method}`

- **Configuration:**
  - `use_llm: bool` - Enable LLM classification (default: True)
  - `model_name: str` - LLM to use (e.g., "gpt-4", "claude-3")
  - `custom_categories: List[str]` - Override default tones

- **Default Emotional Tones:**
  - Devastating, Hopeful, Tense, Joyful, Melancholic
  - Triumphant, Fearful, Peaceful, Conflicted, Resigned

- **Batch Processing:**
  - `classify_all_beats(ncp_data)`: Classify every beat in narrative
  - Returns list of classification results
```

**Creative Advancement Scenario**: Emotional Rhythm Analysis

```
**Desired Outcome**: Visualize emotional pacing of story
**Current Reality**: 20 beats loaded, emotional_weight not set
**Natural Progression**:
  1. Call classify_all_beats(ncp_data)
  2. Each beat receives classification + confidence
  3. Map results: [Tense, Hopeful, Devastating, ...]
  4. Reveal pacing pattern (tension-release-tension)
**Achieved Outcome**: Emotional structure made visible
```

---

## 4. Use Case Scenarios

### Use Case 1: Multi-Source Loading (Production Workflow)

```python
# Load from various sources uniformly
loader = NCPLoaderNode(validate=True)

# From file (development)
local_ncp = loader.load_from_file("./narratives/tech_thriller.json")

# From API (production)
remote_ncp = loader.load_from_url("https://api.stories.com/ncp/123")

# From memory (testing)
test_ncp = loader.load_from_dict({"title": "Test", "players": [], ...})
```

### Use Case 2: Complex Query Patterns (Fantasy Epic)

```python
traversal = NarrativeTraversalNode(mode=TraversalMode.PLAYER_JOURNEY)

# Follow the hero's journey
elara_beats = traversal.traverse_player_journey(ncp_data, "elara_1")

# Find beats where vengeance theme appears
vengeance_beats = traversal.find_thematic_beats(
    ncp_data, 
    "perspective_justice", 
    search_terms=["vengeance", "revenge", "retribution"]
)

# Discover multi-character scenes
ensemble_beats = [b for b in ncp_data.storybeats if len(b.related_players) > 2]
```

### Use Case 3: Character Arc Comparison (Coming of Age)

```python
generator = CharacterArcGenerator()

# Generate arcs for three character types
protagonist_arc = generator.generate(ncp_data, "maya_1")  # Main character
deuteragonist_arc = generator.generate(ncp_data, "derek_1")  # Supporting
mentor_arc = generator.generate(ncp_data, "grandma_rosa_1")  # Guide

# Each returns structured markdown for comparison
```

### Use Case 4: Deep Theme Analysis (Sci-Fi Ethics)

```python
analyzer = ThematicTensionAnalyzer()

# Analyze primary philosophical tension
humanity_tech = analyzer.analyze(ncp_data, "perspective_consciousness")

# Analyze secondary theme
creator_creation = analyzer.analyze(ncp_data, "perspective_autonomy")

# Results show which beats explore which themes
```

### Use Case 5: Batch Emotional Classification (Thriller Screenplay)

```python
classifier = EmotionalBeatClassifierNode(
    use_llm=True,
    model_name="gpt-4"
)

# Classify all 20 beats in screenplay
results = classifier.classify_all_beats(ncp_data)

# Map emotional rhythm
rhythm = [r["classification"] for r in results]
# → ["Tense", "Devastating", "Hopeful", "Tense", "Triumphant", ...]
```

---

## 5. LangGraph Integration Patterns

### State Flow Pattern

```
┌─────────────────┐
│  Initial State  │
│  - ncp_data: None
│  - error: None   
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  NCPLoaderNode  │
│  load_from_*()  │
└────────┬────────┘
         │
         ▼
┌─────────────────┐
│  State Updated  │
│  - ncp_data: NCPData
│  - metadata: {}  
└────────┬────────┘
         │
    ┌────┴────┐
    │ Route   │
    └────┬────┘
    ▼    ▼    ▼
┌───┐  ┌───┐  ┌───┐
│Arc│  │Thm│  │Emo│
└─┬─┘  └─┬─┘  └─┬─┘
  │      │      │
  └──────┼──────┘
         ▼
┌─────────────────┐
│  Final State    │
│  - analysis: str│
│  - metadata: {} │
└─────────────────┘
```

### Conditional Routing

```python
def route_by_analysis_type(state: NCPState) -> str:
    """Route to appropriate analyzer based on request."""
    analysis_type = state["metadata"].get("analysis_type")
    
    if analysis_type == "character":
        return "character_arc"
    elif analysis_type == "theme":
        return "thematic_analysis"
    elif analysis_type == "emotional":
        return "emotional_classification"
    else:
        return "traversal"
```

---

## 6. Quality Criteria

### ✅ Creating Focus
- Emphasizes what users create: arc summaries, thematic analyses, emotional maps
- Not focused on "fixing" narrative issues

### ✅ Structural Dynamics
- NCP schema provides natural organization
- Traversal patterns reveal inherent narrative structure
- State flows through typed transformations

### ✅ Advancing Patterns
- Each component builds on previous (Loader → Traversal → Analysis)
- Results enable further creation (summaries → comparisons → insights)

### ✅ Desired Outcomes
- Clear deliverables: markdown summaries, beat lists, classifications
- Measurable: confidence scores, beat counts, coverage metrics

---

## 7. Anti-Patterns Avoided

- ❌ No "problem-fixing" language (e.g., "This solves the issue of...")
- ❌ No forced connections (each component has clear purpose)
- ❌ No oscillating patterns (data flows forward, not back-and-forth)
- ❌ No over-specification of implementation details

---

## 8. Dependencies

| Dependency       | Purpose                      |
| ---------------- | ---------------------------- |
| `langgraph`      | State graph execution        |
| `pydantic`       | Schema validation            |
| `langchain-core` | LLM integration (optional)   |
| `redis`          | State persistence (optional) |

---

## 9. Component 6: Unified State Bridge (NEW)

### Implementation Reference
**File**: `narrative_intelligence/schemas/unified_state_bridge.py` (737 lines)

```markdown
### UnifiedStateBridge
The shared contract enabling all six systems to communicate.

- **Behavior:**
  - Provides typed dataclasses for cross-system state
  - JSON serialization for Redis compatibility
  - Factory functions for common operations
  - Helper methods for state manipulation

- **Factory Functions:**
  - `create_new_narrative_state(story_id, session_id)`: Initialize fresh state
  - `create_beat_from_webhook(event_id, content, analysis, sequence)`: Beat from GitHub event
  - `get_default_characters()`: Mia, Ava8, Miette archetypes
  - `get_default_themes()`: Integration, Collaboration, Coherence threads

- **State Methods:**
  - `add_beat(beat)`: Add beat and update position
  - `add_routing_decision(decision)`: Record routing choice
  - `update_character_arc(char_id, impact, description)`: Track arc progress
  - `update_theme_strength(theme_id, delta)`: Adjust theme visibility
  - `get_last_n_beats(n)`: Context for generation
  - `calculate_coherence()`: Compute overall narrative coherence
  - `should_create_new_episode()`: Episode boundary detection
```

**Creative Advancement Scenario**: Cross-System State Flow

```
**Desired Outcome**: State flows through LangGraph → Flowise → Langflow seamlessly
**Current Reality**: Different systems use different state formats
**Natural Progression**:
  1. LangGraph creates UnifiedNarrativeState
  2. State serialized to JSON, stored in Redis via RedisKeys
  3. Flowise retrieves state, adds routing decisions
  4. Langflow retrieves state, processes through three universes
  5. State returned to LangGraph for beat generation
**Achieved Outcome**: Single contract enables multi-system orchestration
```

---

## 10. Component 7: Three-Universe Processor (NEW)

```markdown
### ThreeUniverseProcessor
LangGraph graph that processes events through all three universe lenses.

- **Behavior:**
  - `process(event, context)`: Analyze from all 3 perspectives in parallel
  - Returns `ThreeUniverseAnalysis` with:
    - Engineer perspective (technical analysis)
    - Ceremony perspective (relational analysis)
    - Story Engine perspective (narrative analysis)
    - Lead universe determination
    - Coherence score

- **Node Sequence:**
  1. `interpret_engineer`: Technical intent classification
  2. `interpret_ceremony`: Relational/K'é analysis
  3. `interpret_story_engine`: Narrative function detection
  4. `synthesize`: Combine perspectives, determine lead
  5. `calculate_coherence`: Score alignment

- **Lead Universe Logic:**
  - CEREMONY leads if: new contributor, sacred pause needed, relational obligation
  - ENGINEER leads if: technical precision critical, schema validation required
  - STORY_ENGINE leads if: narrative coherence primary, character arc in focus

- **Integration:**
  - Uses `UnifiedNarrativeState` from state bridge
  - Outputs to Langfuse via three-universe events
  - Informs routing decisions in Flowise/Langflow
```

**Creative Advancement Scenario**: GitHub Webhook Processing

```
**Desired Outcome**: Issue #110 interpreted through all three lenses
**Current Reality**: Raw webhook payload arrives
**Natural Progression**:
  1. Engineer: "FEATURE_REQUEST, confidence 0.8"
  2. Ceremony: "CO_CREATION from new contributor, needs K'é acknowledgment"
  3. Story Engine: "INCITING_INCIDENT, new thread entering narrative"
  4. Synthesis: Lead=CEREMONY (relationship first), coherence=0.88
  5. Result: Welcome message before technical analysis
**Achieved Outcome**: Response honors all three perspectives
```

---

## 11. Storytelling Package Integration

The `storytelling` package (`/src/storytelling`) is a primary consumer of this toolkit.

### Consumer Components

| Storytelling Component     | Uses From This Toolkit                               |
| -------------------------- | ---------------------------------------------------- |
| `NCPAwareStoryGenerator`   | `StoryBeat`, `NCPState`, `Player`, `Perspective`     |
| `CharacterArcTracker`      | Pattern from `CharacterState`, arc_position tracking |
| `EmotionalBeatEnricher`    | Beat analysis and classification patterns            |
| `AnalyticalFeedbackLoop`   | Gap identification, routing to enrichment            |
| `NarrativeAwareStoryGraph` | LangGraph orchestration patterns                     |

### Type Alignment

StoryBeat in storytelling should include `universe_analysis` field:

```python
# Storytelling consumer pattern
@dataclass
class StoryBeat:
    beat_id: str
    beat_index: int
    raw_text: str
    # ... existing fields ...
    universe_analysis: Optional[ThreeUniverseAnalysis]  # From unified_state_bridge
```

### Event Emission

Storytelling emits events consumed by the tracing layer:

| Event                        | Emitted By             | Received By       |
| ---------------------------- | ---------------------- | ----------------- |
| `BEAT_GENERATED`             | NCPAwareStoryGenerator | narrative-tracing |
| `EMOTIONAL_QUALITY_ASSESSED` | EmotionalBeatEnricher  | narrative-tracing |
| `CHARACTER_ARC_UPDATED`      | CharacterArcTracker    | narrative-tracing |
| `GAP_IDENTIFIED`             | AnalyticalFeedbackLoop | narrative-tracing |

**Coordination**: See `/src/storytelling/rispecs/COORDINATION_FROM_NARINTEL_INSTANCE.md`

---

## 12. Extension Points

### Adding New Traversal Modes
```python
class CustomTraversalMode(Enum):
    RELATIONSHIP_MAP = "relationship_map"  # Character interactions
    PACING_ANALYSIS = "pacing_analysis"    # Beat timing
```

### Adding New Emotional Categories
```python
classifier = EmotionalBeatClassifierNode(
    custom_categories=["Uncanny", "Sublime", "Grotesque"]
)
```

### Creating New Analysis Graphs
Follow the pattern:
1. Create state schema extending NCPState
2. Define node functions operating on that state
3. Wire nodes into StateGraph
4. Export as composable component

---

*Generated following RISE Framework v1.2 - Specification is implementation-agnostic*
