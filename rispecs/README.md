# 📘 Narintel RISE Specifications

> **Narrative Intelligence Stack** - A unified ecosystem for NCP-driven story analysis, agent coordination, and creative advancement.

**Version**: 1.0  
**Last Updated**: 2025-12-31  
**Framework**: RISE (Reverse-engineer → Intent-extract → Specify → Export)  
**Attribution**: Based on RISE Framework v1.2 by Guillaume D.Isabelle

---

## 🙏 Foundational Credits

This stack evolved from the **Indigenous-AI Collaborative Platform (IAIP)** rispecs:

| IAIP Origin                                     | Contribution to NarIntel                                                     |
| ----------------------------------------------- | ---------------------------------------------------------------------------- |
| `four-directions.spec.md`                       | Three-Universe Model (East/South/West/North → Engineer/Ceremony/StoryEngine) |
| `ceremonial-technology.spec.md`                 | Five-Phase methodology, Sacred Pause, K'é Protocol                           |
| `relational-science.spec.md`                    | Relational accountability, concentric values model                           |
| `iaip-holistic-reasoning-mcp.spec.md`           | MCP tool patterns, holistic inquiry cycles                                   |
| `continuous-companionship-architecture.spec.md` | Persistent context, session continuity                                       |

**See**: `/a/src/IAIP/rispecs/COORDINATION_TO_NARINTEL_CYCLE.md` for full lineage

---

## 🌟 Vision: What Users Create

This stack enables creators to:

1. **Transform narratives into structured intelligence** - Load, validate, and traverse stories as queryable data structures
2. **Analyze character arcs and thematic tensions** - Generate insights about narrative dynamics
3. **Classify emotional beats** - Understand the emotional landscape of stories
4. **Route creative workflows intelligently** - Agents that understand narrative context
5. **Trace the entire creative process** - Observability across all narrative operations

---

## 📁 Specification Index

### Foundation

| Specification                                | Description                                                     |
| -------------------------------------------- | --------------------------------------------------------------- |
| [ncp-schema.rispec.md](ncp-schema.rispec.md) | Narrative Context Protocol - Core data model for all components |

### Core Toolkit (LangGraph)

| Specification                                                                            | Package                                 | Description                                     | Status |
| ---------------------------------------------------------------------------------------- | --------------------------------------- | ----------------------------------------------- | ------ |
| [narrative-intelligence.langgraph.rispec.md](narrative-intelligence.langgraph.rispec.md) | `langgraph/libs/narrative-intelligence` | Core NCP analysis toolkit with nodes and graphs | ✅ 98% |

### Tracing Layer (LangChain)

| Specification                                                                  | Package                               | Description                          | Status |
| ------------------------------------------------------------------------------ | ------------------------------------- | ------------------------------------ | ------ |
| [narrative-tracing.langchain.rispec.md](narrative-tracing.langchain.rispec.md) | `langchain/libs/narrative-tracing`    | Narrative-aware Langfuse integration | ✅ Complete |

### Agent Coordination Layer

| Specification                                                              | Package        | Description                                      | Status |
| -------------------------------------------------------------------------- | -------------- | ------------------------------------------------ | ------ |
| [agentic-flywheel.flowise.rispec.md](agentic-flywheel.flowise.rispec.md)   | `ava-Flowise`  | Narrative intent classification and flow routing | 🔴 Spec Only |
| [universal-router.langflow.rispec.md](universal-router.langflow.rispec.md) | `ava-langflow` | Three-universe handler and backend abstraction   | 🟡 ~70% |

### Human-AI Collaboration

| Specification                                                                      | Package        | Description                                          | Status |
| ---------------------------------------------------------------------------------- | -------------- | ---------------------------------------------------- | ------ |
| [storytelling-roles-tooling.rispec.md](storytelling-roles-tooling.rispec.md)       | `storytelling` | Seven roles (Architect→Witness) and their tool needs | 🟡 ~75% |

---

## 🏗️ Structural Dynamics

### Three-Universe Model

Every narrative event flows through three interpretive lenses:

```
┌──────────────────────────────────────────────────────────┐
│                    NARRATIVE EVENT                        │
│         (Story beat, webhook, user query)                │
└────────────────────────┬─────────────────────────────────┘
                         │
         ┌───────────────┼───────────────┐
         ▼               ▼               ▼
┌─────────────────┐ ┌─────────────────┐ ┌─────────────────┐
│  ENGINEER WORLD │ │  CEREMONY WORLD │ │ STORY ENGINE    │
│     (Mia)       │ │     (Ava8)      │ │    (Miette)     │
├─────────────────┤ ├─────────────────┤ ├─────────────────┤
│ - Schema valid? │ │ - K'é honored?  │ │ - Arc coherent? │
│ - Types correct?│ │ - Sacred pause? │ │ - Theme threads?│
│ - API callable? │ │ - Relations ok? │ │ - Beat sequence?│
└─────────────────┘ └─────────────────┘ └─────────────────┘
         │               │               │
         └───────────────┼───────────────┘
                         ▼
              ┌─────────────────────┐
              │  UNIFIED RESPONSE   │
              └─────────────────────┘
```

### NCP Protocol Foundation

All specifications build upon the **Narrative Context Protocol (NCP)**:

- **Players**: Characters carrying narrative weight
- **Perspectives**: Throughlines (Objective, Main Character, Influence, Relationship)
- **Storybeats**: Tonal units with abstraction, spatial, and temporal dimensions
- **Storypoints**: Structural markers (Inciting Incident, Climax, Resolution)
- **Dynamics**: Forces shaping narrative progression

---

## 🔗 Integration Flow

```
┌─────────────────────────────────────────────────────────────────┐
│                     NARRATIVE INTELLIGENCE STACK                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                  │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │           Layer 4: CONSUMERS (Miadi-46, Webhooks)          │ │
│  └──────────────────────────┬─────────────────────────────────┘ │
│                             │                                    │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │   Layer 3: ROUTING (ava-langflow + ava-Flowise)            │ │
│  │   - Three-universe handlers                                 │ │
│  │   - Narrative intent classification                         │ │
│  │   - Dynamic flow selection                                  │ │
│  └──────────────────────────┬─────────────────────────────────┘ │
│                             │                                    │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │   Layer 2: TRACING (langchain)                              │ │
│  │   - Narrative-specific Langfuse events                      │ │
│  │   - Cross-stack correlation                                  │ │
│  │   - Creative archaeology traces                              │ │
│  └──────────────────────────┬─────────────────────────────────┘ │
│                             │                                    │
│  ┌────────────────────────────────────────────────────────────┐ │
│  │   Layer 1: ANALYSIS (langgraph/narrative-intelligence)      │ │
│  │   - NCP Loader + Validator                                  │ │
│  │   - Narrative Graph Traversal                               │ │
│  │   - Character Arc Generator                                 │ │
│  │   - Thematic Tension Analyzer                               │ │
│  │   - Emotional Beat Classifier                               │ │
│  └────────────────────────────────────────────────────────────┘ │
│                                                                  │
└─────────────────────────────────────────────────────────────────┘
```

---

## 📋 Cross-Specification Dependencies

| From Spec           | Depends On                         | Nature of Dependency                     |
| ------------------- | ---------------------------------- | ---------------------------------------- |
| `langchain` tracing | `langgraph` narrative-intelligence | Traces NCP analysis operations           |
| `flowise` flywheel  | `langgraph` narrative-intelligence | Uses NCP state for intent classification |
| `langflow` router   | `flowise` flywheel + `langgraph`   | Routes to backends using NCP context     |
| All specs           | NCP Schema                         | Core data model                          |

---

## 📦 Downstream Consumers

### Storytelling Package (`/src/storytelling`)

The `storytelling` package is a primary consumer of the Narrative Intelligence Stack. Its rispecs coordinate with ours:

| Storytelling Rispec                                   | Consumes From NarIntel                         |
| ----------------------------------------------------- | ---------------------------------------------- |
| `Narrative_Intelligence_Integration_Specification.md` | `StoryBeat`, `NCPState` from langgraph toolkit |
| `Character_Arc_Tracking_Specification.md`             | `CharacterState` patterns                      |
| `Emotional_Beat_Enrichment_Specification.md`          | Emits events to langchain tracing              |
| `Analytical_Feedback_Loop_Specification.md`           | Uses gap routing, emits analysis events        |
| `Narrative_Aware_Story_Graph_Specification.md`        | Orchestration patterns                         |
| `Logging_And_Traceability_Specification.md`           | Langfuse event taxonomy                        |
| `IAIP_Integration_Specification.md`                   | Ceremony World / K'é alignment                 |

**Coordination File**: See `/src/storytelling/rispecs/COORDINATION_FROM_NARINTEL_INSTANCE.md`

---

## 🎯 Creative Advancement Patterns

These specifications enable:

| Pattern                  | Description                                  | Enabled By               |
| ------------------------ | -------------------------------------------- | ------------------------ |
| **Arc Tracking**         | Character development monitored across beats | `narrative-intelligence` |
| **Theme Threading**      | Thematic tensions traced through story       | `narrative-intelligence` |
| **Emotional Mapping**    | Emotional landscape visualized               | `narrative-intelligence` |
| **Narrative Routing**    | Flow selection based on story position       | `flowise` + `langflow`   |
| **Creative Archaeology** | Full trace of creative decisions             | `langchain` tracing      |

---

## 📖 How to Use These Specifications

1. **For Implementation**: Each `.rispec.md` file is self-contained enough to re-implement the component from scratch
2. **For Review**: Understand desired outcomes and structural dynamics without reading code
3. **For Extension**: Add new capabilities by extending the specification first
4. **For Testing**: Creative Advancement Scenarios can be converted to integration tests

---

*Generated following RISE Framework v1.2 - Creative Orientation Over Reactive Approaches*