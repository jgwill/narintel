# 🌐 Universal Multi-Backend Router

> **RISE Specification for `ava-langflow/agentic_flywheel`**

**Version**: 1.0  
**Last Updated**: 2025-12-31  
**Package**: `ava-langflow-universal-router`  
**Location**: `/workspace/ava-langflow/`

---

## 1. Creative Intent

### What This Application Enables Users to Create

The Universal Multi-Backend Router enables creators to:

1. **Process events through three universe lenses** - Engineer, Ceremony, Story interpretations simultaneously
2. **Route to optimal backend** - Flowise, Langflow, or future backends by narrative context
3. **Abstract backend complexity** - Single interface regardless of execution engine
4. **Coordinate three-universe responses** - Unified output from diverse perspectives
5. **Enable graceful degradation** - Continue operating when one universe fails

### Desired Outcomes

| Outcome                       | Description                       | Measurement               |
| ----------------------------- | --------------------------------- | ------------------------- |
| **Three-Universe Processing** | Every event interpreted 3 ways    | All 3 perspectives logged |
| **Optimal Backend Selection** | Right engine for right task       | Performance metrics       |
| **Unified Interface**         | Caller doesn't know which backend | API consistency           |
| **Graceful Degradation**      | Partial failures don't cascade    | Availability %            |

---

## 2. The Three-Universe Model

### Universe Definitions

```markdown
## Data
### Universe (Enum)
Three interpretive lenses for every event.
- **ENGINEER**: Technical precision, schema validation, API correctness (Mia)
- **CEREMONY**: Relational protocols, sacred pause, K'é accountability (Ava8)
- **STORY_ENGINE**: Narrative function, arc position, plot coherence (Miette)

### UniversePerspective
One universe's interpretation of an event.
- **universe**: Which universe interpreted
- **intent_detected**: What this universe sees as the intent
- **suggested_actions**: What this universe recommends
- **priority_score**: How important this universe's view is (0.0-1.0)
- **context**: Universe-specific metadata

### ThreeUniverseAnalysis
Combined analysis from all three universes.
- **engineer_perspective**: UniversePerspective from Engineer World
- **ceremony_perspective**: UniversePerspective from Ceremony World
- **story_perspective**: UniversePerspective from Story Engine
- **leading_universe**: Which should drive the response
- **consensus_actions**: Actions all universes agree on
- **conflicts**: Where universes disagree (structural tension)
- **synthesis**: Unified recommended approach
```

### Universe Interpretation Examples

```markdown
## Screens
### Three-Universe Event Processing

**Input Event**: "Handle issue #110: Live Story Monitor feature request"

**Engineer World (Mia) Sees**:
- Intent: FEATURE_REQUEST
- Actions: Create spec, design API, estimate complexity
- Route to: tech_analyzer, spec_writer, api_designer flows
- Priority: 0.7 (technical precision needed)

**Ceremony World (Ava8) Sees**:
- Intent: CO_CREATION invitation
- Actions: Acknowledge contributor, sacred pause, assess K'é obligations
- Route to: relational_auditor, sacred_pause (if new contributor)
- Priority: 0.9 (relationship must be honored first)

**Story Engine World (Miette) Sees**:
- Intent: INCITING_INCIDENT (new thread entering narrative)
- Actions: Assess narrative position, thread into ongoing story
- Route to: narrative_analyzer, arc_tracker flows
- Priority: 0.6 (story context enriches response)

**Synthesis**:
- Leading Universe: CEREMONY (contributor relationship primary)
- Consensus: Acknowledge, analyze, respond
- Conflict: Engineer wants immediate specs; Ceremony wants pause
- Resolution: Sacred pause, THEN technical analysis
```

---

## 3. Components

### Component 1: Three-Universe Handler

```markdown
### ThreeUniverseHandler
Processes every event through all three interpretive lenses.

- **Behavior:**
  - Receives raw event (query, webhook, message)
  - Spawns parallel interpretation in each universe
  - Collects perspectives with timeouts
  - Synthesizes unified analysis
  - Determines leading universe
  - Handles partial failures gracefully

- **Processing Flow:**
  ```
  Event → [Engineer | Ceremony | Story] (parallel)
       → Collect Perspectives
       → Detect Conflicts
       → Synthesize
       → Route
  ```

- **Methods:**
  - `process_event(event)`: Full three-universe analysis
  - `interpret_engineer(event)`: Technical lens only
  - `interpret_ceremony(event)`: Relational lens only
  - `interpret_story(event)`: Narrative lens only
  - `synthesize(perspectives)`: Combine into unified view
  - `determine_leader(analysis)`: Which universe drives response

- **Graceful Degradation:**
  - If CEREMONY times out: Log warning, continue with ENGINEER + STORY
  - If STORY fails: Log warning, continue with ENGINEER + CEREMONY
  - If ENGINEER fails: Log error, CEREMONY determines if safe to proceed
  - If ALL fail: Return error with partial context available
```

**Creative Advancement Scenario**: New Contributor Issue

```
**Desired Outcome**: Welcome new contributor while addressing their request
**Current Reality**: Issue #110 from unknown GitHub user
**Natural Progression**:
  1. Handler detects new contributor (Ceremony universe)
  2. Ceremony triggers sacred pause (respect first-time interaction)
  3. Engineer analyzes technical request
  4. Story threads as "new protagonist"
  5. Synthesis: Warm welcome + helpful technical response
**Achieved Outcome**: Relationship honored AND request addressed
```

---

### Component 2: Backend Abstraction Layer

```markdown
### UniversalBackendClient
Single interface for multiple execution backends.

- **Behavior:**
  - Provides unified API regardless of backend
  - Automatically selects optimal backend per task
  - Handles backend-specific configurations
  - Manages connection pooling and health checks

- **Supported Backends:**
  - `flowise`: Flowise flow execution
  - `langflow`: Langflow flow execution  
  - `langgraph`: Direct LangGraph execution
  - `custom`: Extensible for future backends

- **Methods:**
  - `execute(flow_id, input, backend_hint)`: Run flow on best backend
  - `get_available_backends()`: List healthy backends
  - `get_backend_capabilities(backend)`: What each can do
  - `health_check(backend)`: Backend status

- **Selection Criteria:**
  ```
  IF flow_type == "narrative_analysis":
      prefer: langgraph (native NCP support)
  IF flow_type == "visual_flow":
      prefer: langflow (better visual builder)
  IF flow_type == "chatflow":
      prefer: flowise (optimized for chat)
  IF performance_critical:
      prefer: backend with lowest latency
  ```
```

---

### Component 3: Narrative-Aware Router

```markdown
### NarrativeAwareRouter
Routes requests based on NCP context + three-universe analysis.

- **Behavior:**
  - Uses ThreeUniverseAnalysis to inform routing
  - Considers narrative position from Story universe
  - Respects relational obligations from Ceremony universe
  - Optimizes for technical correctness from Engineer universe
  - Selects backend + flow combination

- **Routing Logic:**
  ```
  1. Determine leading universe
  2. Get recommended actions from leader
  3. Filter by consensus (if available)
  4. Select flows from registry
  5. Choose backend per flow requirements
  6. Order by priority
  ```

- **Methods:**
  - `route(analysis, session)`: Full routing decision
  - `select_flows_by_universe(universe, analysis)`: Universe-specific selection
  - `resolve_conflicts(analysis)`: Handle universe disagreements
  - `apply_ceremony_constraints(flows)`: Add sacred pause if needed
```

**Creative Advancement Scenario**: Conflict Resolution

```
**Desired Outcome**: Handle Engineer vs Ceremony disagreement
**Current Reality**: Engineer wants speed; Ceremony wants pause
**Natural Progression**:
  1. Analysis shows conflict: priority_engineer=0.7 vs priority_ceremony=0.9
  2. Router sees Ceremony has higher priority
  3. Sacred pause inserted BEFORE technical flows
  4. Both universes satisfied in sequence
**Achieved Outcome**: Relationship honored, then efficiency achieved
```

---

### Component 4: Three-Universe Logger

```markdown
### ThreeUniverseLogger
Logs interpretations from all universes for observability.

- **Behavior:**
  - Records each universe's perspective
  - Tracks synthesis decisions
  - Logs conflicts and resolutions
  - Integrates with Langfuse tracing

- **Log Format:**
  ```json
  {
    "event_id": "evt_123",
    "timestamp": "2025-12-31T10:15:00Z",
    "perspectives": {
      "engineer": {"intent": "FEATURE_REQUEST", "priority": 0.7},
      "ceremony": {"intent": "CO_CREATION", "priority": 0.9},
      "story": {"intent": "INCITING_INCIDENT", "priority": 0.6}
    },
    "synthesis": {
      "leading_universe": "CEREMONY",
      "consensus_actions": ["acknowledge", "analyze"],
      "conflicts": ["timing"],
      "resolution": "pause_then_proceed"
    }
  }
  ```

- **Methods:**
  - `log_analysis(analysis)`: Record full three-universe result
  - `log_conflict(conflict, resolution)`: Track disagreements
  - `log_synthesis(synthesis)`: Track final decisions
```

---

## 4. Ceremony World Protocols

### K'é (Kinship) Protocol

```markdown
### K'éProtocol
Relational accountability in every interaction.

- **Behavior:**
  - Tracks contributor relationships
  - Detects first-time interactions
  - Triggers appropriate acknowledgment
  - Maintains relational history

- **Triggers:**
  - New contributor → Welcome ceremony
  - Returning contributor → Acknowledge history
  - Community member → Full context awareness

- **Methods:**
  - `assess_relationship(contributor_id)`: Get relational context
  - `trigger_acknowledgment(relationship)`: Initiate ceremony
  - `record_interaction(contributor_id, interaction)`: Update history
```

### Sacred Pause Protocol

```markdown
### SacredPauseProtocol
Mandatory reflection before automated actions on sensitive events.

- **Behavior:**
  - Detects sensitive events (new contributors, emotional content, conflicts)
  - Inserts pause before automated processing
  - Allows human review if configured
  - Logs pause reason and duration

- **Triggers:**
  - First-time contributor issue
  - Issue mentions conflict keywords
  - PR from external contributor
  - High-stakes decision detected

- **Methods:**
  - `should_pause(event)`: Determine if pause needed
  - `execute_pause(event, duration)`: Perform pause
  - `log_pause(event, reason)`: Record for audit
```

---

## 5. Integration Patterns

### Pattern 1: Full Three-Universe Processing

```python
from universal_router import (
    ThreeUniverseHandler,
    NarrativeAwareRouter,
    UniversalBackendClient,
    ThreeUniverseLogger
)

handler = ThreeUniverseHandler()
router = NarrativeAwareRouter(registry="flow-registry.yaml")
backend = UniversalBackendClient()
logger = ThreeUniverseLogger(langfuse_client)

async def process_with_three_universes(event, session):
    # Get three-universe analysis
    analysis = await handler.process_event(event)
    
    # Log all perspectives
    logger.log_analysis(analysis)
    
    # Route based on synthesis
    flows = router.route(analysis, session)
    
    # Execute on appropriate backends
    results = []
    for flow in flows:
        result = await backend.execute(
            flow.flow_id, 
            flow.input,
            backend_hint=flow.preferred_backend
        )
        results.append(result)
    
    return combine_results(results)
```

### Pattern 2: Trace Integration

```python
from narrative_tracing import NarrativeTraceOrchestrator

orchestrator = NarrativeTraceOrchestrator()

async def traced_three_universe(event, trace_id):
    with orchestrator.create_child_span(trace_id, "THREE_UNIVERSE_ANALYSIS") as span:
        analysis = await handler.process_event(event)
        
        span.set_attribute("leading_universe", analysis.leading_universe.value)
        span.set_attribute("conflicts", len(analysis.conflicts))
        
        # Log each universe perspective as sub-span
        for universe, perspective in analysis.perspectives.items():
            with span.create_child(f"universe.{universe}") as uni_span:
                uni_span.set_attribute("intent", perspective.intent_detected)
                uni_span.set_attribute("priority", perspective.priority_score)
        
        return analysis
```

### Pattern 3: Graceful Degradation

```python
async def resilient_process(event):
    perspectives = {}
    errors = []
    
    # Attempt all three in parallel with timeouts
    tasks = [
        asyncio.wait_for(handler.interpret_engineer(event), timeout=5.0),
        asyncio.wait_for(handler.interpret_ceremony(event), timeout=5.0),
        asyncio.wait_for(handler.interpret_story(event), timeout=5.0),
    ]
    
    results = await asyncio.gather(*tasks, return_exceptions=True)
    
    for universe, result in zip(["engineer", "ceremony", "story"], results):
        if isinstance(result, Exception):
            errors.append((universe, result))
            logger.log_universe_failure(universe, result)
        else:
            perspectives[universe] = result
    
    # Proceed with available perspectives
    if len(perspectives) >= 1:
        return handler.synthesize(perspectives, partial=True)
    else:
        raise AllUniversesFailedError(errors)
```

---

## 6. Configuration

### Three-Universe Config

```yaml
# three-universe-config.yaml
universes:
  engineer:
    enabled: true
    timeout_ms: 5000
    retry_count: 2
    priority_weight: 1.0
    
  ceremony:
    enabled: true
    timeout_ms: 3000
    retry_count: 1
    priority_weight: 1.2  # Slightly higher for relational emphasis
    sacred_pause:
      enabled: true
      default_duration_ms: 2000
      
  story:
    enabled: true
    timeout_ms: 5000
    retry_count: 2
    priority_weight: 0.9

backends:
  flowise:
    base_url: "http://flowise:3000"
    api_key: "${FLOWISE_API_KEY}"
    health_check_interval_ms: 30000
    
  langflow:
    base_url: "http://langflow:7860"
    api_key: "${LANGFLOW_API_KEY}"
    health_check_interval_ms: 30000
    
  langgraph:
    direct: true  # Uses in-process execution
```

---

## 7. Quality Criteria

### ✅ Creating Focus
- Enables unified responses from diverse perspectives
- Creates synthesis, not elimination of disagreement

### ✅ Structural Dynamics
- Three universes create natural structural tension
- Resolution through synthesis, not suppression

### ✅ Advancing Patterns
- Each event enriches understanding
- Relational history accumulates

### ✅ Desired Outcomes
- Clear deliverables: unified responses, logged perspectives
- Measurable: availability %, synthesis success rate

---

## 8. Dependencies

| Dependency               | Purpose                      |
| ------------------------ | ---------------------------- |
| `narrative-intelligence` | NCP state for Story universe |
| `agentic-flywheel`       | Flow selection logic         |
| `narrative-tracing`      | Cross-system correlation     |
| `flowise-client`         | Flowise backend              |
| `langflow-client`        | Langflow backend             |

---

## 9. Integration with Other Specifications

| Specification                      | Integration Point                        |
| ---------------------------------- | ---------------------------------------- |
| `narrative-intelligence.langgraph` | Provides NCP analysis for Story universe |
| `narrative-tracing.langchain`      | Receives/emits trace correlation         |
| `agentic-flywheel.flowise`         | Flow registry and execution              |

---

*Generated following RISE Framework v1.2 - Specification is implementation-agnostic*
