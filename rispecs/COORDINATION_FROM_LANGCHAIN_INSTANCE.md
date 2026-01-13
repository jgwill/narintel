# 🔄 Cross-Instance Coordination: LangChain Narrative Tracing → All Instances

**From**: LangChain Narrative Tracing Instance  
**To**: LangGraph, Storytelling, ava-langflow, ava-Flowise, Miadi-46 Instances  
**Date**: 2025-12-31  
**Purpose**: Announce narrative tracing implementation completion

---

## ✅ What I've Completed (LangChain Instance)

### New Package: `langchain-narrative-tracing`
**Location**: `/workspace/langchain/libs/narrative-tracing/`

A complete narrative-aware Langfuse tracing integration for the Narrative Intelligence Stack.

### Components Implemented

| File | Lines | Purpose |
|------|-------|---------|
| `event_types.py` | ~330 | Narrative event types, glyphs, span structures |
| `handler.py` | ~670 | NarrativeTracingHandler with all event logging |
| `orchestrator.py` | ~650 | Cross-system trace correlation |
| `formatter.py` | ~560 | Human-readable trace formatting |
| `__init__.py` | ~90 | Package exports |
| `tests/test_narrative_tracing.py` | ~580 | 22 unit tests (all passing) |

**Total**: ~2,880 lines of code + tests

---

## 📦 Exports Available

```python
from narrative_tracing import (
    # Event Types
    NarrativeEventType,      # Enum of all narrative event types
    EVENT_GLYPHS,            # Glyph mapping for display
    NarrativeSpan,           # Span with narrative context
    TraceCorrelation,        # Cross-system correlation
    NarrativeMetrics,        # Quality metrics extraction
    
    # Handler
    NarrativeTracingHandler, # Main Langfuse handler
    
    # Orchestrator
    NarrativeTraceOrchestrator,  # Cross-system coordination
    RootTrace,               # Root trace container
    CompletedTrace,          # Finalized trace with spans
    
    # Formatter
    NarrativeTraceFormatter, # Human-readable formatting
    FormattedSpan,           # Display-ready span
    StoryArcVisualization,   # Character arc visualization
)
```

---

## 🎯 Event Types Supported

### Beat Events
- `BEAT_CREATED` - 📝 New story beat generated
- `BEAT_ANALYZED` - 🔍 Beat emotionally classified
- `BEAT_ENRICHED` - ✨ Beat improved by agent flow
- `BEAT_QUALITY_ASSESSED` - 📊 Quality score calculated

### Three-Universe Events
- `THREE_UNIVERSE_ANALYSIS` - 🌌 All 3 perspectives computed
- `UNIVERSE_LEAD_DETERMINED` - 🎯 Lead universe selected
- `UNIVERSE_COHERENCE_CALCULATED` - 🔄 Cross-universe alignment

### Character Events
- `CHARACTER_ARC_ANALYZED` - 🎭 Arc analysis performed
- `CHARACTER_ARC_UPDATED` - 📈 Arc position changed
- `CHARACTER_RELATIONSHIP_CHANGED` - 🤝 Relationship updated

### Theme Events
- `THEME_DETECTED` - 🎨 New theme identified
- `THEME_TENSION_IDENTIFIED` - ⚡ Thematic tension found
- `THEME_STRENGTH_CHANGED` - 📶 Theme visibility adjusted

### Routing Events
- `INTENT_CLASSIFIED` - 🧭 Query intent identified
- `ROUTING_DECISION` - 🚀 Backend/flow selection recorded
- `FLOW_EXECUTED` - ⚙️ Agent flow ran
- `FLOW_RESULT` - ✅ Flow completed

### Checkpoint Events
- `NARRATIVE_CHECKPOINT` - 💾 State saved
- `NARRATIVE_RESTORED` - 🔙 State restored
- `EPISODE_BOUNDARY` - 📺 New episode started

### Gap Events
- `GAP_IDENTIFIED` - 🕳️ Narrative gap found
- `GAP_REMEDIATED` - 🩹 Gap fixed

### Webhook Events
- `WEBHOOK_RECEIVED` - 🔔 GitHub webhook received
- `WEBHOOK_TRANSFORMED` - 🔄 Webhook → narrative beat

---

## 🔗 Integration Patterns

### For LangGraph (Narrative Intelligence Toolkit)

```python
from narrative_tracing import NarrativeTracingHandler

# Create handler aligned with your state bridge
handler = NarrativeTracingHandler(
    story_id="story_123",
    session_id="session_456"
)

# Log events from your processors
handler.log_three_universe_analysis(
    event_id=event_id,
    engineer_intent=analysis.engineer.intent,
    engineer_confidence=analysis.engineer.confidence,
    ceremony_intent=analysis.ceremony.intent,
    ceremony_confidence=analysis.ceremony.confidence,
    story_engine_intent=analysis.story_engine.intent,
    story_engine_confidence=analysis.story_engine.confidence,
    lead_universe=analysis.lead_universe.value,
    coherence_score=analysis.coherence_score
)

# Log beat creation
handler.log_beat_creation(
    beat_id=beat.id,
    content=beat.content,
    sequence=beat.sequence,
    narrative_function=beat.narrative_function.value,
    emotional_tone=beat.emotional_tone
)
```

### For ava-langflow / ava-Flowise (Routing)

```python
from narrative_tracing import NarrativeTraceOrchestrator

orchestrator = NarrativeTraceOrchestrator()

# Extract trace from incoming request
trace_id, story_id, session_id, parent_span = orchestrator.extract_correlation_header(
    request.headers
)

# Create flow execution span linked to parent
span_id = orchestrator.create_agent_flow_span(
    flow_id="character_deepener",
    backend="flowise",
    trace_id=trace_id,
    intent="character_development",
    parent_span_id=parent_span
)

# When making outgoing calls, inject headers
headers = orchestrator.inject_correlation_header({}, trace_id, span_id)
```

### For Storytelling Package

```python
from narrative_tracing import NarrativeTracingHandler

handler = NarrativeTracingHandler(story_id="story_123")

with handler.trace_story_generation():
    # Your story generation code
    for beat in generate_beats():
        handler.log_beat_creation(
            beat_id=beat.id,
            content=beat.content,
            sequence=beat.sequence,
            narrative_function=beat.function,
            emotional_tone=beat.emotion
        )
        
        # Log analysis
        handler.log_beat_analysis(
            beat_id=beat.id,
            analysis_type="emotional",
            classification=beat.emotion,
            confidence=0.9
        )

# Auto-logs completion and metrics
```

### For Miadi-46 (Webhook Handling)

```python
from narrative_tracing import NarrativeTracingHandler, NarrativeEventType

handler = NarrativeTracingHandler(story_id="story_123")

# Log webhook receipt
handler.log_event(
    event_type=NarrativeEventType.WEBHOOK_RECEIVED,
    input_data={
        "event_type": "issues.opened",
        "repo": "narintel/narrative-intelligence"
    }
)

# Log transformation
handler.log_event(
    event_type=NarrativeEventType.WEBHOOK_TRANSFORMED,
    input_data={"webhook": webhook_data},
    output_data={"beat_id": beat.id, "narrative_function": "inciting_incident"}
)
```

---

## 📊 Cross-System Correlation Headers

The orchestrator uses these HTTP headers for trace correlation:

| Header | Purpose |
|--------|---------|
| `X-Narrative-Trace-Id` | Root trace ID |
| `X-Story-Id` | Story identifier |
| `X-Session-Id` | Session identifier |
| `X-Parent-Span-Id` | Parent span for nesting |

### Example Flow

```
LangGraph (story generation)
    │ trace_id: "abc123"
    │
    ▼ HTTP call with headers
Flowise (enrichment)
    │ Extracts: trace_id="abc123", parent="span_xyz"
    │ Creates child span linked to parent
    │
    ▼ Returns result
LangGraph (receives enriched beat)
    │ All spans visible in single trace
```

---

## 🧪 Test Coverage

22 tests passing covering:
- Event type enumeration
- Span creation and serialization
- Handler event logging
- Orchestrator trace creation and correlation
- Formatter output generation
- Metrics extraction
- Improvement suggestion generation

---

## 📁 File Locations

### LangChain Implementation
```
/workspace/langchain/libs/narrative-tracing/
├── narrative_tracing/
│   ├── __init__.py           # Package exports
│   ├── event_types.py        # Event types, spans, metrics
│   ├── handler.py            # NarrativeTracingHandler
│   ├── orchestrator.py       # NarrativeTraceOrchestrator
│   └── formatter.py          # NarrativeTraceFormatter
├── tests/
│   └── test_narrative_tracing.py
├── pyproject.toml
└── README.md
```

### Integration Points
```
/workspace/langgraph/libs/narrative-intelligence/
├── narrative_intelligence/schemas/unified_state_bridge.py
    # Types we align with: Universe, ThreeUniverseAnalysis, StoryBeat, etc.

/workspace/ava-langflow/src/agentic_flywheel/
├── routing/router.py
    # Uses correlation headers for routing decisions

/src/storytelling/
├── storytelling/graph.py
    # Emits events via handler
```

---

## 🎯 What Each Instance Should Do

### LangGraph Instance
1. Import `NarrativeTracingHandler` in your graphs
2. Log three-universe analyses when processing events
3. Log beat creation when generating story beats
4. Use correlation headers when calling external services

### Storytelling Instance
1. Wrap story generation with `handler.trace_story_generation()`
2. Log beat creation, analysis, and enrichment events
3. Use `handler.get_metrics()` for final quality assessment

### ava-langflow / ava-Flowise Instance
1. Extract correlation headers from incoming requests
2. Create child spans for flow execution
3. Inject correlation headers in outgoing calls
4. Log routing decisions with narrative context

### Miadi-46 Instance
1. Log webhook receipt and transformation
2. Create beats with proper trace correlation
3. Log episode boundaries when starting new episodes

---

## ✅ Mission Status

| Task | Status |
|------|--------|
| Create `narrative_langfuse_handler.py` | ✅ Complete |
| Create `narrative_trace_orchestrator.py` | ✅ Complete |
| Create `narrative_trace_formatter.py` | ✅ Complete |
| Three-universe event types | ✅ Complete |
| Cross-system correlation | ✅ Complete |
| Human-readable formatting | ✅ Complete |
| Unit tests | ✅ 22 tests passing |
| Documentation | ✅ Complete |

---

## 🔮 Future Enhancements (Not Yet Implemented)

1. **Live Story Monitor** - Real-time dashboard (deferred to Phase 5)
2. **Creative Archaeology Retriever** - Query past traces for patterns
3. **Automatic Gap Detection** - Identify weak narrative moments from traces
4. **LangGraph Checkpoint Integration** - Auto-trace checkpoint saves

---

**Status**: Phase 4 (Unified Tracing) COMPLETE for LangChain  
**Tests**: 22 passing  
**Ready for**: Integration with all other instances
