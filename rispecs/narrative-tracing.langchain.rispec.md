# 📊 Narrative Tracing Integration

> **RISE Specification for `langchain/integrations/narrative_tracing`**

**Version**: 1.0  
**Last Updated**: 2025-12-31  
**Package**: `langchain-narrative-tracing`  
**Location**: `/workspace/langchain/integrations/`

---

## 1. Creative Intent

### What This Application Enables Users to Create

The Narrative Tracing Integration enables creators to:

1. **Trace the entire story creation journey** - From initial beat generation through analysis to enrichment
2. **Understand creative decisions** - See why each narrative choice was made
3. **Correlate across systems** - Link LangGraph analysis → Flowise flows → final output
4. **Visualize narrative operations** - Story-aware span naming, not generic LLM calls
5. **Learn from creative archaeology** - Mine past traces for patterns and improvements

### Desired Outcomes

| Outcome | Description | Measurement |
|---------|-------------|-------------|
| **Full Visibility** | Every narrative operation traced | 100% operation coverage |
| **Semantic Clarity** | Spans named by narrative function | Human-readable trace trees |
| **Cross-Stack Correlation** | Trace IDs flow through all systems | Single root → all children |
| **Creative Learning** | Past traces inform future generation | Retrievable by story_id |

---

## 2. Data Structures

### Trace Event Types

```markdown
## Data
### NarrativeEventType
Categories of traceable narrative operations.
- **BEAT_CREATED**: New story beat generated
- **BEAT_ANALYZED**: Beat classified emotionally
- **BEAT_ENRICHED**: Beat improved by agent flow
- **CHARACTER_ARC**: Character arc analysis performed
- **CHARACTER_ARC_UPDATED**: Character arc position changed
- **THEME_TENSION**: Thematic tension identified
- **THEME_STRENGTH_CHANGED**: Theme visibility adjusted
- **NARRATIVE_CHECKPOINT**: Story state saved
- **AGENT_FLOW_EXECUTED**: Flowise/Langflow flow ran
- **AGENT_ROUTE_DECISION**: Intent → flow routing
- **ROUTING_DECISION**: Backend/flow selection recorded
- **INTENT_CLASSIFIED**: Query intent identified
- **THREE_UNIVERSE_ANALYSIS**: All 3 perspectives computed (NEW)
- **UNIVERSE_LEAD_DETERMINED**: Lead universe selected (NEW)
- **COHERENCE_CALCULATED**: Cross-universe alignment scored (NEW)

### NarrativeSpan
A traced operation with narrative context.
- **span_id**: Unique span identifier
- **trace_id**: Parent trace identifier
- **event_type**: NarrativeEventType
- **story_id**: Story being operated on
- **beat_id**: (Optional) Specific beat involved
- **player_ids**: (Optional) Characters involved
- **emotional_tone**: (Optional) Detected emotion
- **theme_keywords**: (Optional) Theme tags
- **input_data**: What went into the operation
- **output_data**: What came out
- **duration_ms**: Operation time
- **metadata**: Additional context

### TraceCorrelation
Links traces across system boundaries.
- **root_trace_id**: Original trace from generation
- **child_trace_ids**: Traces from downstream systems
- **story_id**: Story being traced
- **correlation_path**: System hop sequence
```

### Handler Configuration

```markdown
## Data
### NarrativeTracingConfig
Configuration for narrative-aware tracing.
- **langfuse_public_key**: Langfuse authentication
- **langfuse_secret_key**: Langfuse secret
- **langfuse_host**: (Optional) Custom Langfuse host
- **project_name**: Project identifier
- **enable_semantic_naming**: Use narrative-aware span names
- **correlation_header**: Header name for cross-system IDs
- **batch_size**: Traces per batch upload
- **flush_interval_ms**: Max time between uploads
```

---

## 3. Components

### Component 1: Narrative Tracing Handler

```markdown
### NarrativeTracingHandler
Langfuse callback handler with narrative awareness.

- **Behavior:**
  - Extends `LangfuseCallbackHandler` with narrative event types
  - Auto-detects narrative operations from function names
  - Creates semantic span names (e.g., "📖 character_arc:protagonist_1")
  - Attaches NCP metadata to spans
  - Supports custom event logging

- **Integration Points:**
  - Hooks into LangChain callback system
  - Receives events from LangGraph executions
  - Correlates with external system traces

- **Semantic Naming Pattern:**
  ```
  Generic: "llm.run" 
  Narrative: "📖 beat.classify:storybeat_12 (Tense→Hopeful)"
  ```

- **Event Logging Methods:**
  - `log_beat_creation(beat, source)`: Track beat generation
  - `log_beat_analysis(beat, classification)`: Track emotional classification
  - `log_beat_enrichment(beat, enrichment_type)`: Track agent improvements
  - `log_character_arc(player_id, arc_summary)`: Track arc analysis
  - `log_theme_tension(perspective_id, analysis)`: Track thematic analysis
```

**Creative Advancement Scenario**: Complete Story Trace

```
**Desired Outcome**: See full journey of story from conception to completion
**Current Reality**: Story generated through multiple systems
**Natural Progression**:
  1. Story generation creates root trace with story_id
  2. Each beat creation is a child span
  3. Analysis operations inherit trace_id
  4. Flowise enrichment flows continue the trace
  5. Final trace shows complete creative journey
**Achieved Outcome**: End-to-end visibility of story creation
```

---

### Component 2: Multi-Stack Trace Orchestrator

```markdown
### NarrativeTraceOrchestrator
Correlates traces across LangGraph → Flowise → LangChain boundaries.

- **Behavior:**
  - Creates unique trace IDs that flow through entire stack
  - Maintains trace context across HTTP boundaries
  - Links parent-child relationships across systems
  - Provides trace reconstruction for complete view

- **Correlation Methods:**
  - `create_story_generation_root(story_id)`: Start new trace
  - `create_child_span(parent_trace_id, event_type)`: Extend trace
  - `inject_correlation_header(request)`: Add trace ID to outgoing calls
  - `extract_correlation_header(request)`: Read trace ID from incoming calls
  - `reconstruct_full_trace(root_trace_id)`: Gather all related spans

- **Cross-System Flow:**
  ```
  LangGraph (beat generation)
       │ trace_id: "abc123"
       ▼
  HTTP call with X-Narrative-Trace-Id: abc123
       │
       ▼
  Flowise (enrichment flow)
       │ parent_trace_id: "abc123"
       │ span_id: "def456"
       ▼
  Response with enriched beat
       │
       ▼
  LangGraph (state update)
       │ correlates "def456" as child of "abc123"
  ```
```

**Creative Advancement Scenario**: Debug Enrichment Failure

```
**Desired Outcome**: Understand why beat enrichment produced poor result
**Current Reality**: Enriched beat doesn't match expected quality
**Natural Progression**:
  1. Find trace by story_id and beat_id
  2. Reconstruct full trace including Flowise spans
  3. See input to enrichment flow
  4. See LLM prompts and responses
  5. Identify where quality degraded
**Achieved Outcome**: Root cause visible in trace tree
```

---

### Component 3: Narrative Trace Formatter

```markdown
### NarrativeTraceFormatter
Formats traces for human understanding.

- **Behavior:**
  - Transforms generic spans into narrative-aware displays
  - Groups operations by story structure (acts, beats, characters)
  - Highlights emotional tone changes
  - Shows character involvement per operation

- **Display Methods:**
  - `format_for_display(trace)`: Human-readable summary
  - `format_as_timeline(trace)`: Chronological beat sequence
  - `format_as_arc_graph(trace)`: Character-centric view
  - `export_as_markdown(trace)`: Documentation-ready format

- **Output Format:**
  ```
  📖 Story Generation: "The Threshold"
  ├── 🎭 Beat Created: "The Awakening" (Hopeful)
  │   └── Characters: [Maya, Derek]
  ├── 🎭 Beat Created: "The Challenge" (Tense)
  │   └── Characters: [Maya]
  ├── 🔍 Beat Analyzed: emotional=Devastating, confidence=0.92
  ├── ✨ Beat Enriched via character_deepener flow
  │   └── Input: weak character voice
  │   └── Output: strengthened dialogue
  └── 💾 Checkpoint: act_1_complete
  ```
```

---

### Component 4: Creative Archaeology Retriever

```markdown
### CreativeArchaeologyRetriever
Mine past traces for patterns and insights.

- **Behavior:**
  - Query traces by story_id, player_id, theme, emotion
  - Identify common enrichment patterns
  - Find successful generation sequences
  - Detect quality degradation patterns

- **Query Methods:**
  - `find_traces_by_story(story_id)`: All traces for a story
  - `find_traces_by_emotion(emotional_tone)`: Beats with specific tone
  - `find_enrichment_patterns(success_threshold)`: What enrichments work
  - `find_quality_regressions()`: Where quality dropped

- **Analytics:**
  - Average enrichment success rate
  - Most common emotional transitions
  - Character involvement correlations
  - Theme → beat type mappings
```

---

## 4. Integration Patterns

### Pattern 1: LangGraph Node Tracing

```python
from narrative_tracing import NarrativeTracingHandler

handler = NarrativeTracingHandler(config)

# Automatic tracing of LangGraph execution
with handler.trace_story_generation(story_id="story_123"):
    result = character_arc_generator.generate(ncp_data, "protagonist_1")
    # Spans created automatically:
    # - gather_character_beats
    # - generate_arc_summary
    # - llm_call (with narrative context)
```

### Pattern 2: Cross-System Correlation

```python
from narrative_tracing import NarrativeTraceOrchestrator

orchestrator = NarrativeTraceOrchestrator()

# In LangGraph (origin)
root_trace = orchestrator.create_story_generation_root("story_123")

# When calling Flowise
headers = orchestrator.inject_correlation_header({})
response = flowise_client.call(flow_id, input_data, headers=headers)

# In Flowise (receiver)
parent_trace_id = orchestrator.extract_correlation_header(request)
with orchestrator.create_child_span(parent_trace_id, "AGENT_FLOW_EXECUTED"):
    # Flow execution traced as child
    pass
```

### Pattern 3: Narrative-Aware Callbacks

```python
from langchain_core.callbacks import CallbackManager
from narrative_tracing import NarrativeTracingHandler

handler = NarrativeTracingHandler(config)

# Attach to LangChain operations
callback_manager = CallbackManager([handler])

# Now all LLM calls include narrative context
llm.invoke(prompt, config={"callbacks": callback_manager})
```

---

## 5. Trace Event Specifications

### Beat Created Event

```json
{
  "event_type": "BEAT_CREATED",
  "story_id": "story_123",
  "beat_id": "storybeat_7",
  "timestamp": "2025-12-31T10:15:00Z",
  "metadata": {
    "title": "The Revelation",
    "emotional_weight": "Devastating",
    "related_players": ["maya_1", "derek_1"],
    "generation_source": "story_generator_v2",
    "prompt_template": "indigenous_spiral_of_memory"
  }
}
```

### Beat Analyzed Event

```json
{
  "event_type": "BEAT_ANALYZED",
  "story_id": "story_123",
  "beat_id": "storybeat_7",
  "timestamp": "2025-12-31T10:15:30Z",
  "metadata": {
    "analysis_type": "emotional_classification",
    "classification": "Devastating",
    "confidence": 0.94,
    "method": "llm_gpt4",
    "previous_classification": null
  }
}
```

### Agent Flow Executed Event

```json
{
  "event_type": "AGENT_FLOW_EXECUTED",
  "story_id": "story_123",
  "beat_id": "storybeat_7",
  "timestamp": "2025-12-31T10:16:00Z",
  "metadata": {
    "flow_id": "character_deepener",
    "backend": "flowise",
    "input_quality_score": 0.65,
    "output_quality_score": 0.88,
    "enrichment_applied": "dialogue_strengthening"
  }
}
```

### Three-Universe Analysis Event (NEW)

```json
{
  "event_type": "THREE_UNIVERSE_ANALYSIS",
  "event_id": "evt_456",
  "story_id": "story_123",
  "timestamp": "2025-12-31T10:15:00Z",
  "metadata": {
    "engineer": {
      "universe": "engineer",
      "intent": "feature_request",
      "confidence": 0.8,
      "suggested_flows": ["spec_writer", "api_designer"]
    },
    "ceremony": {
      "universe": "ceremony",
      "intent": "co_creation",
      "confidence": 0.7,
      "suggested_flows": ["sacred_pause", "relational_auditor"]
    },
    "story_engine": {
      "universe": "story_engine",
      "intent": "inciting_incident",
      "confidence": 0.95,
      "suggested_flows": ["narrative_analyzer", "arc_tracker"]
    },
    "lead_universe": "story_engine",
    "coherence_score": 0.88
  }
}
```

### Routing Decision Event (NEW)

```json
{
  "event_type": "ROUTING_DECISION",
  "decision_id": "route_789",
  "story_id": "story_123",
  "session_id": "session_456",
  "timestamp": "2025-12-31T10:16:30Z",
  "metadata": {
    "backend": "flowise",
    "flow": "character_deepener",
    "method": "narrative",
    "score": 0.92,
    "success": true,
    "latency_ms": 1250,
    "narrative_position": {
      "act": 2,
      "phase": "confrontation",
      "beat_count": 7
    }
  }
}
```

---

## 6. Redis Key Integration

Use `RedisKeys` from `narrative_intelligence.schemas.unified_state_bridge` for consistent key naming:

```python
from narrative_intelligence.schemas import RedisKeys

# In tracing code
state_key = RedisKeys.state(session_id)     # → "ncp:state:{session_id}"
beats_key = RedisKeys.beats(session_id)     # → "ncp:beats:{session_id}"
routing_key = RedisKeys.routing_history(session_id)  # → "ncp:routing:{session_id}"
```

---

## 7. Quality Criteria

### ✅ Creating Focus
- Enables understanding and learning from creative process
- Traces reveal what was created, not what was fixed

### ✅ Structural Dynamics
- Parent-child relationships show natural flow
- Cross-system correlation reveals structural connections

### ✅ Advancing Patterns
- Each trace builds knowledge for future generation
- Creative archaeology enables continuous improvement

### ✅ Desired Outcomes
- Clear deliverables: trace trees, formatted summaries, analytics
- Measurable: coverage %, correlation success rate

---

## 7. Dependencies

| Dependency | Purpose |
|------------|---------|
| `langfuse` | Trace storage and UI |
| `langchain-core` | Callback integration |
| `pydantic` | Schema validation |

---

## 8. Integration with Other Specifications

| Specification | Integration Point |
|---------------|-------------------|
| `narrative-intelligence.langgraph` | Traces NCP analysis operations |
| `agentic-flywheel.flowise` | Receives correlation headers |
| `universal-router.langflow` | Receives correlation headers |

---

## 9. Storytelling Package Integration

The `storytelling` package (`/src/storytelling`) is a primary **event emitter** for this tracing layer.

### Event Sources from Storytelling

| Storytelling Component | Events Emitted |
|------------------------|----------------|
| `NCPAwareStoryGenerator` | `BEAT_CREATED`, `NARRATIVE_CHECKPOINT` |
| `EmotionalBeatEnricher` | `BEAT_ANALYZED`, `BEAT_ENRICHED` |
| `CharacterArcTracker` | `CHARACTER_ARC`, `CHARACTER_ARC_UPDATED` |
| `AnalyticalFeedbackLoop` | `GAP_IDENTIFIED`, `GAP_REMEDIATED` |
| `NarrativeAwareStoryGraph` | `AGENT_FLOW_EXECUTED`, workflow spans |

### Integration Pattern

```python
# In storytelling/narrative_intelligence_integration.py
from narrative_tracing import NarrativeTracingHandler

class NCPAwareStoryGenerator:
    def __init__(self, llm_provider, tracer: NarrativeTracingHandler):
        self.tracer = tracer
    
    def generate_beat_with_ncp(self, ...):
        beat = self._generate(...)
        self.tracer.log_beat_creation(beat, source="ncp_generator")
        return beat
```

### Session Logging Integration

Storytelling's `Logger` and `SessionManager` can integrate with this tracing layer:

```python
# Optional Langfuse enhancement to existing Logger
class EnhancedLogger(Logger):
    def __init__(self, tracer: NarrativeTracingHandler):
        super().__init__()
        self.tracer = tracer
    
    def log_llm_interaction(self, prompt, response, node_name):
        super().log_llm_interaction(prompt, response, node_name)
        # Also emit to Langfuse
        self.tracer.log_event(
            event_type="LLM_GENERATION",
            input_data={"prompt": prompt, "node": node_name},
            output_data={"response": response}
        )
```

**Coordination**: See `/src/storytelling/rispecs/COORDINATION_FROM_NARINTEL_INSTANCE.md`

---

*Generated following RISE Framework v1.2 - Specification is implementation-agnostic*
