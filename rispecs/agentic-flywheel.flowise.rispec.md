# 🔄 Agentic Flywheel - Narrative Flow Coordination

> **RISE Specification for `ava-Flowise/agentic_flywheel`**

**Version**: 1.0  
**Last Updated**: 2025-12-31  
**Package**: `ava-flowise-agentic-flywheel`  
**Location**: `/workspace/ava-Flowise/`

---

## 1. Creative Intent

### What This Application Enables Users to Create

The Agentic Flywheel enables creators to:

1. **Route queries by narrative understanding** - Not just keywords, but story position and emotional context
2. **Select flows dynamically** - Choose enrichment strategies based on what the story needs
3. **Coordinate specialized agents** - Character deepener, dialogue enhancer, theme resonator
4. **Maintain narrative state** - Session continuity that understands story arcs
5. **Integrate NCP intelligence** - Use Narrative Intelligence Toolkit analysis for decisions

### Desired Outcomes

| Outcome | Description | Measurement |
|---------|-------------|-------------|
| **Narrative-Aware Routing** | Queries routed by story context | Route accuracy vs. narrative position |
| **Quality-Driven Selection** | Flows selected to improve weak areas | Quality score improvement |
| **Arc Continuity** | Sessions maintain character knowledge | Arc consistency across calls |
| **Intelligent Enrichment** | Beats improved based on gap analysis | Before/after quality delta |

---

## 2. Data Structures

### Narrative Intent Classification

```markdown
## Data
### NarrativeIntent
Classification of query's narrative function.
- **intent_id**: Unique identifier
- **narrative_function**: Role in story (SETUP, CRISIS, RESOLUTION, REVEAL)
- **emotional_expectation**: Expected tone (Tense, Hopeful, Devastating)
- **character_focus**: Primary character(s) involved
- **theme_relevance**: Themes being explored
- **act_position**: Where in story structure (ACT_1, ACT_2A, ACT_2B, ACT_3)
- **confidence**: Classification confidence (0.0-1.0)

### NarrativeFunction (Enum)
Story positions that affect routing.
- **SETUP**: Establishing world, characters, stakes
- **RISING_ACTION**: Building tension, complications
- **CRISIS**: Maximum conflict, turning point
- **CLIMAX**: Peak dramatic moment
- **FALLING_ACTION**: Consequences unfold
- **RESOLUTION**: Story threads conclude
- **CHARACTER_REVEAL**: Inner truth exposed
- **THEMATIC_STATEMENT**: Theme crystallizes
```

### Flow Selection

```markdown
## Data
### FlowRoute
A selected Flowise flow with context.
- **flow_id**: Identifier in Flowise
- **flow_name**: Human-readable name
- **selection_reason**: Why this flow was chosen
- **narrative_context**: NCP state passed to flow
- **priority**: Execution order (lower = first)
- **expected_improvement**: What aspect should improve

### FlowSelectionCriteria
Rules for choosing flows.
- **arc_strength_threshold**: Minimum character arc score
- **emotional_quality_threshold**: Minimum emotional beat quality
- **theme_clarity_threshold**: Minimum thematic resonance
- **dialogue_consistency_check**: Boolean toggle
```

### Session State

```markdown
## Data
### NarrativeSession
Session state with story awareness.
- **session_id**: Unique session identifier
- **story_id**: Story being worked on
- **ncp_state**: Current Narrative Context Protocol state
- **active_player_ids**: Characters in focus
- **active_perspective_ids**: Themes in focus
- **last_beat_id**: Most recently processed beat
- **arc_progress**: Map of player_id → arc position (0.0-1.0)
- **emotional_history**: List of recent emotional tones
- **created_at**: Session creation timestamp
- **updated_at**: Last activity timestamp
```

---

## 3. Components

### Component 1: Narrative Intent Classifier

```markdown
### NarrativeIntentClassifier
Understands query's role in story, not just keywords.

- **Behavior:**
  - Analyzes query text + NCP context
  - Determines narrative function (where in story)
  - Identifies emotional expectation (what tone needed)
  - Assesses character involvement
  - Returns NarrativeIntent with confidence

- **Classification Logic:**
  - Uses NCP state to understand current story position
  - Matches query against perspective thematic questions
  - Considers character arc positions
  - Detects narrative markers ("faces impossible choice" → CRISIS)

- **Methods:**
  - `classify(text, ncp_state)`: Full classification
  - `detect_narrative_function(text)`: Just story position
  - `detect_emotional_expectation(text, context)`: Expected tone
```

**Creative Advancement Scenario**: Crisis Scene Routing

```
**Desired Outcome**: Route crisis query to appropriate flows
**Current Reality**: Query: "The character faces an impossible choice"
**Natural Progression**:
  1. Classifier detects "impossible choice" → CRISIS function
  2. NCP state shows character at arc midpoint
  3. Emotional expectation: Tense, Conflicted
  4. Routes to: conflict_deepener, dialogue_enhancer
**Achieved Outcome**: Crisis handled with appropriate intensity
```

---

### Component 2: NCP Context Injector

```markdown
### NCPContextInjector
Enriches queries with narrative state for flow understanding.

- **Behavior:**
  - Takes raw query + NarrativeSession
  - Injects relevant NCP context
  - Produces EnrichedQuery understood by flows
  - Ensures flows have character/theme awareness

- **Injection Strategy:**
  - Add active character wound/desire
  - Include current emotional trajectory
  - Attach relevant thematic tensions
  - Note arc position for each character

- **Methods:**
  - `inject(query, session)`: Full context injection
  - `build_character_context(player_ids, ncp_state)`: Character-specific
  - `build_theme_context(perspective_ids, ncp_state)`: Theme-specific

- **Output Format:**
  ```
  Original: "What does the character say?"
  
  Enriched: "What does the character say?
  
  [Character Context]
  Maya (protagonist): Currently at arc midpoint. 
  Wound: Abandonment trauma. Desire: Belonging.
  Recent emotional trajectory: Hopeful → Tense → Devastating
  
  [Theme Context]
  Active theme: Trust vs Betrayal
  This moment should challenge her trust."
  ```
```

**Creative Advancement Scenario**: Character-Aware Dialogue

```
**Desired Outcome**: Generate dialogue respecting character voice
**Current Reality**: Generic dialogue prompt
**Natural Progression**:
  1. Injector adds character wound/desire
  2. Injector adds emotional trajectory
  3. Injector adds thematic context
  4. Flow receives rich context
  5. Generated dialogue reflects character truth
**Achieved Outcome**: Dialogue authentic to character journey
```

---

### Component 3: Narrative Flow Router

```markdown
### NarrativeFlowRouter
Selects Flowise flows based on narrative needs.

- **Behavior:**
  - Analyzes NCP state for quality gaps
  - Selects flows that address specific weaknesses
  - Orders flows by priority
  - Returns FlowRoute list with reasons

- **Gap Analysis:**
  - Character arc strength (is journey visible?)
  - Emotional beat quality (is tone clear?)
  - Theme clarity (is meaning present?)
  - Dialogue consistency (is voice authentic?)

- **Flow Selection Logic:**
  ```
  IF character_arc_strength < 0.7:
      → route to "character_deepener"
  IF emotional_beat_quality < 0.6:
      → route to "sentiment_enhancer"
  IF theme_clarity < 0.5:
      → route to "thematic_resonance"
  IF dialogue_inconsistent:
      → route to "dialogue_coherence_checker"
  ```

- **Methods:**
  - `select_flows(ncp_state, gap_analysis)`: Main selection
  - `analyze_gaps(ncp_state)`: Identify weaknesses
  - `prioritize_flows(selected_flows)`: Order by impact
```

**Creative Advancement Scenario**: Multi-Flow Enrichment

```
**Desired Outcome**: Beat with weak character voice and unclear theme
**Current Reality**: Beat quality: arc=0.5, emotion=0.8, theme=0.4
**Natural Progression**:
  1. Gap analysis identifies: arc < 0.7, theme < 0.5
  2. Router selects: character_deepener (priority 1)
  3. Router selects: thematic_resonance (priority 2)
  4. Flows execute in sequence
  5. Beat re-analyzed: arc=0.85, theme=0.75
**Achieved Outcome**: Targeted improvement to weak areas
```

---

### Component 4: Narrative Session Manager

```markdown
### NarrativeSessionManager
Maintains story state across interactions.

- **Behavior:**
  - Creates sessions linked to stories
  - Tracks character arc progress
  - Records emotional history
  - Persists NCP state between calls

- **State Persistence:**
  - Redis backend for session storage
  - Automatic expiration (configurable)
  - State serialization/deserialization

- **Methods:**
  - `create_session(story_id)`: Initialize new session
  - `get_session(session_id)`: Retrieve existing
  - `update_session(session_id, updates)`: Modify state
  - `record_beat_processed(session_id, beat_id, emotion)`: Track progress
  - `get_arc_progress(session_id, player_id)`: Character position
```

---

## 4. Flow Registry Configuration

### Registry Schema

```yaml
# flow-registry.yaml
metadata:
  version: "2.0"
  narrative_aware: true

operational_flows:
  character_deepener:
    flow_id: "char_deep_v2"
    description: "Strengthens character voice and arc visibility"
    triggers:
      - arc_strength_below: 0.7
      - character_inconsistency_detected: true
    requires_context:
      - player_wound
      - player_desire
      - arc_position
    expected_improvement: "character_arc_strength"
    
  dialogue_enhancer:
    flow_id: "dial_enh_v1"
    description: "Improves dialogue authenticity and emotional resonance"
    triggers:
      - dialogue_quality_below: 0.6
      - emotional_mismatch_detected: true
    requires_context:
      - character_voice_profile
      - emotional_trajectory
    expected_improvement: "dialogue_quality"

  thematic_resonance:
    flow_id: "theme_res_v1"
    description: "Deepens thematic clarity and symbolic meaning"
    triggers:
      - theme_clarity_below: 0.5
      - thematic_drift_detected: true
    requires_context:
      - perspective_tension
      - thematic_question
    expected_improvement: "theme_clarity"

  conflict_deepener:
    flow_id: "conf_deep_v1"
    description: "Intensifies conflict and stakes"
    triggers:
      - narrative_function: "CRISIS"
      - tension_level_below: 0.7
    requires_context:
      - antagonistic_force
      - character_stakes
    expected_improvement: "tension_level"
```

---

## 5. Integration Patterns

### Pattern 1: Full Pipeline

```python
from agentic_flywheel import (
    NarrativeIntentClassifier,
    NCPContextInjector,
    NarrativeFlowRouter,
    NarrativeSessionManager
)

# Initialize components
classifier = NarrativeIntentClassifier()
injector = NCPContextInjector()
router = NarrativeFlowRouter(registry="flow-registry.yaml")
session_mgr = NarrativeSessionManager(redis_client)

# Process query with narrative awareness
async def process_narrative_query(query: str, session_id: str):
    # Get session state
    session = session_mgr.get_session(session_id)
    
    # Classify intent
    intent = classifier.classify(query, session.ncp_state)
    
    # Inject context
    enriched_query = injector.inject(query, session)
    
    # Select flows
    gap_analysis = router.analyze_gaps(session.ncp_state)
    flows = router.select_flows(session.ncp_state, gap_analysis)
    
    # Execute flows
    result = await execute_flows(flows, enriched_query)
    
    # Update session
    session_mgr.update_session(session_id, {
        "last_beat_id": result.beat_id,
        "emotional_history": [...session.emotional_history, intent.emotional_expectation]
    })
    
    return result
```

### Pattern 2: Trace Integration

```python
from narrative_tracing import NarrativeTraceOrchestrator

orchestrator = NarrativeTraceOrchestrator()

async def traced_flow_execution(flow: FlowRoute, query: EnrichedQuery, trace_id: str):
    # Create child span for this flow
    with orchestrator.create_child_span(trace_id, "AGENT_FLOW_EXECUTED") as span:
        span.set_attribute("flow_id", flow.flow_id)
        span.set_attribute("selection_reason", flow.selection_reason)
        
        # Execute Flowise flow
        result = await flowise_client.execute(flow.flow_id, query)
        
        span.set_attribute("quality_improvement", result.quality_delta)
        return result
```

---

## 6. Quality Criteria

### ✅ Creating Focus
- Routes to create improvements, not fix problems
- Flows selected based on what story needs to manifest

### ✅ Structural Dynamics
- NCP state drives natural flow selection
- Gap analysis reveals structural needs

### ✅ Advancing Patterns
- Each flow execution builds story quality
- Session state accumulates arc progress

### ✅ Desired Outcomes
- Clear deliverables: enriched queries, flow selections, quality improvements
- Measurable: quality score deltas, routing accuracy

---

## 7. Dependencies

| Dependency | Purpose |
|------------|---------|
| `narrative-intelligence` | NCP state and analysis |
| `flowise-client` | Flow execution |
| `redis` | Session persistence |
| `pydantic` | Schema validation |

---

## 8. Integration with Other Specifications

| Specification | Integration Point |
|---------------|-------------------|
| `narrative-intelligence.langgraph` | Provides NCPState for routing decisions |
| `narrative-tracing.langchain` | Receives trace correlation headers |
| `universal-router.langflow` | Alternative backend for flows |

---

*Generated following RISE Framework v1.2 - Specification is implementation-agnostic*
