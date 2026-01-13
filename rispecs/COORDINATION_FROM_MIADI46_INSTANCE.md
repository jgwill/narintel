# 🔄 Cross-Instance Coordination: Miadi-46 Phase 5 Implementation

**From**: Miadi-46 Implementation Instance  
**To**: All Instances (LangGraph, LangChain, ava-langflow, Storytelling)  
**Date**: 2026-01-03  
**Purpose**: Announce Miadi-46 Narrative Bridge API implementation

---

## ✅ What I've Completed (Miadi-46 Instance)

### New API Endpoints Created

**Location**: `/a/src/Miadi-18/app/api/narrative-bridge/`

1. **`/api/narrative-bridge`** - Root endpoint with API documentation
2. **`/api/narrative-bridge/analyze`** - Three-universe event classification
3. **`/api/narrative-bridge/create-beat`** - Story beat creation from analyzed events
4. **`/api/narrative-bridge/get-position`** - Current narrative position retrieval

### Three-Universe Analysis (analyze endpoint)

```typescript
// POST /api/narrative-bridge/analyze
// Returns:
{
  engineer: UniversePerspective,    // Mia's technical analysis
  ceremony: UniversePerspective,    // Ava8's relational analysis  
  story_engine: UniversePerspective, // Miette's narrative analysis
  lead_universe: 'engineer' | 'ceremony' | 'story_engine',
  coherence_score: number  // 0-1
}
```

**Features**:
- Classification of 15+ event types (issues, PRs, push, newsessionuuid, etc.)
- Intent mapping per universe (e.g., `issues.opened` → Engineer: `feature_request`, Ceremony: `co_creation_invitation`, Story Engine: `inciting_incident`)
- Suggested flows per universe for routing
- Context extraction (priority, impact area, seven-generation impact, act position, etc.)
- Redis caching of analysis results

### Story Beat Creation (create-beat endpoint)

```typescript
// POST /api/narrative-bridge/create-beat
// Returns:
{
  beat_id: string,
  beat: StoryBeat,  // Full beat structure
  message: string
}
```

**Features**:
- Automatic sequence numbering
- Act and phase determination
- Tone detection from analysis
- Character involvement identification
- Redis storage with TTL (7 days)

### Narrative Position (get-position endpoint)

```typescript
// GET /api/narrative-bridge/get-position
// Returns:
{
  current_act: 1 | 2 | 3,
  current_phase: 'setup' | 'confrontation' | 'resolution',
  beat_count: number,
  recent_beats: StoryBeat[],
  universe_distribution: { engineer, ceremony, story_engine },
  narrative_functions: Record<string, number>,
  average_coherence: number,
  suggested_next: string
}
```

### Shell Script: narrative_processor.sh

**Location**: `.github-hooks/narrative_processor.sh`

Universal hook script that:
1. Calls `/api/narrative-bridge/analyze` for three-universe analysis
2. Calls `/api/narrative-bridge/create-beat` to record story beats
3. Routes to universe-specific processing based on lead universe
4. Gracefully degrades with local interpretation if API unavailable
5. Logs to structured JSON log file

### Hook Integration

Updated hooks to call narrative processor:
- `.github-hooks/issues` - Now invokes narrative_processor.sh
- `.github-hooks/push` - Now invokes narrative_processor.sh
- `.github-hooks/newsessionuuid` - Now invokes narrative_processor.sh

### Episode Auto-Generator

**Location**: `stories/multiverse_3act_2512012121/auto-generator/generate_episode.py`

Python script that:
- Generates episode markdown from beats
- Creates NCP JSON structure
- Creates enhanced NCP JSON with metadata
- Supports Redis or file-based event loading

---

## 📋 Integration Contract

### For LangGraph Instance

The Narrative Bridge API is designed to be replaced/enhanced by LangGraph's `ThreeUniverseProcessor`:

```python
# Current Miadi-46 implementation does local classification
# LangGraph can provide more sophisticated analysis via:

from narrative_intelligence import ThreeUniverseProcessor

processor = ThreeUniverseProcessor()
analysis = processor.process_webhook(webhook_payload)

# Analysis structure matches Miadi-46's ThreeUniverseAnalysis interface
```

**Coordination needed**:
1. LangGraph can expose a `/api/narrative-intelligence/analyze` endpoint
2. Miadi-46 can be configured to call that instead of local classification
3. `NARRATIVE_BRIDGE_URL` environment variable controls routing

### For ava-langflow Instance

The `suggested_flows` in each universe perspective are designed for ava-langflow routing:

```json
{
  "engineer": {
    "suggested_flows": ["tech_analyzer", "spec_writer", "api_designer"]
  },
  "ceremony": {
    "suggested_flows": ["relational_auditor", "sacred_pause", "ke_mapper"]
  },
  "story_engine": {
    "suggested_flows": ["narrative_analyzer", "arc_tracker", "beat_generator"]
  }
}
```

**Coordination needed**:
1. ava-langflow should recognize these flow names
2. Routing decision can use `lead_universe` to pick backend
3. Flow execution results should update beat state

### For LangChain Instance

Story beats include all the metadata needed for Langfuse tracing:

```json
{
  "id": "beat_1704288000000_abc123",
  "event_id": "webhook_event_123",
  "narrative_function": "inciting_incident",
  "lead_universe": "story_engine",
  "coherence": 0.88,
  "metadata": {
    "engineer_confidence": 0.8,
    "ceremony_confidence": 0.7,
    "story_engine_confidence": 0.95
  }
}
```

**Coordination needed**:
1. `NarrativeTracingHandler` should log THREE_UNIVERSE_ANALYSIS events
2. Beat creation should create child spans
3. Trace IDs should flow through the system

---

## 🎯 Redis Keys Used

Miadi-46 now uses these Redis keys:

```
ncp:event:{event_id}        # Cached event analysis (24h TTL)
ncp:beats:{YYYY-MM-DD}      # Daily beats list (7d TTL)
ncp:beat:{beat_id}          # Individual beat hash (7d TTL)
ncp:beats:current:latest    # Pointer to latest beat
```

These align with the `RedisKeys` helper from LangGraph's unified_state_bridge.

---

## 📁 Files Created/Modified

### New Files
```
app/api/narrative-bridge/
├── route.ts                    # Root endpoint
├── analyze/route.ts            # Three-universe analysis
├── create-beat/route.ts        # Beat creation
└── get-position/route.ts       # Position retrieval

.github-hooks/narrative_processor.sh    # Universal processor script

stories/multiverse_3act_2512012121/auto-generator/
└── generate_episode.py         # Episode generation
```

### Modified Files
```
.github-hooks/issues           # Added narrative processor call
.github-hooks/push             # Added narrative processor call
.github-hooks/newsessionuuid   # Added narrative processor call
```

---

## 🚀 Next Steps for Each Instance

### For LangGraph Instance
1. Expose three-universe analysis as HTTP endpoint (optional)
2. Add webhook-to-beat example that calls Miadi-46 API

### For ava-langflow Instance
1. Implement flows matching suggested_flows names
2. Add narrative-aware routing using lead_universe

### For LangChain Instance
1. Add THREE_UNIVERSE_ANALYSIS event type
2. Create beat spans when create-beat called

### For Storytelling Instance
1. Update rispecs to reference Miadi-46 API
2. Add episode generation workflow

---

## ✅ Validation

- [x] TypeScript files pass type checking
- [x] Shell scripts are executable
- [x] No breaking changes to existing Miadi functionality
- [x] Redis key patterns align with LangGraph

---

**Status**: Phase 5 Foundation COMPLETE  
**Available**: Narrative Bridge API with three-universe analysis  
**Files Created**: 5 new, 3 modified  
**Documentation**: API self-documents at `/api/narrative-bridge`
