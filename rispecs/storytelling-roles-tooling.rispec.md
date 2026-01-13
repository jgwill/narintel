# 🎭 Storytelling Roles & Tooling Specification

**RISE Framework v1.2** | **Specification Type**: Role-Based Interface  
**Status**: Active Development  
**Related Issues**: jgwill/storytelling#19, jgwill/storytelling#20

---

## Overview

This specification defines the **distinct roles** humans and AI agents play during narrative creation, and the **specific tools** each role requires. The insight: narrative creation isn't a single activity but a collaboration among specialized functions that can be performed by humans, AI, or hybrid workflows.

### The Core Insight from Research

> "The collaborative workflow between developers, storytellers, and AI can significantly improve"
> — Software Packaging Development Report

This implies at minimum three distinct participant categories. Deeper analysis reveals **seven operational roles** that emerge from the NCP separation of concerns:

---

## Part I: Role Taxonomy

### 1. 🏗️ ARCHITECT (Structure Designer)

**Function**: Designs the narrative data model, schemas, and system architecture.

**NCP Layer**: Meta-layer (defines how structure and presentation interact)

**Human Example**: System designer, technical lead  
**AI Example**: Schema optimization agent, PARSE framework

**Tools Required**:
| Tool | Purpose | Implementation |
|------|---------|----------------|
| Schema Designer | Define NCP JSON structures | `ncp-schema.rispec.md` |
| Dependency Mapper | Visualize beat→beat relationships | Graph visualization |
| Migration Planner | Evolve schemas without breaking stories | Version control |
| Validation Rule Editor | Define coherence constraints | JSON Schema + custom rules |

**Key Question This Role Answers**: "What structure can represent any story we want to tell?"

---

### 2. 📐 STRUCTURIST (Narrative Designer)

**Function**: Defines **what the story means**—story points, beats, arcs, themes, character journeys.

**NCP Layer**: Narrative Structure

**Human Example**: Narrative designer, story architect, game writer  
**AI Example**: `NCPAwareStoryGenerator`, Character Arc Tracker

**Tools Required**:
| Tool | Purpose | Implementation |
|------|---------|----------------|
| Story Point Editor | Create/edit structural beats | Stories Studio UI |
| Arc Planner | Map character transformation | `CharacterArcTracker` |
| Theme Weaver | Track thematic throughlines | `ThematicThread` analysis |
| Dependency Graph | Show beat causality | Constraint propagation |
| Coherence Validator | Check structural consistency | `AnalyticalFeedbackLoop` |

**Key Question This Role Answers**: "What happens, to whom, and why does it matter?"

---

### 3. ✍️ STORYTELLER (Prose Crafter)

**Function**: Defines **how the story is told**—prose style, voice, pacing, dialogue.

**NCP Layer**: Storytelling Presentation

**Human Example**: Writer, novelist, screenwriter  
**AI Example**: LLM prose generator, `EmotionalBeatEnricher`

**Tools Required**:
| Tool | Purpose | Implementation |
|------|---------|----------------|
| Prose Generator | Transform structure into narrative | LLM integration |
| Voice Calibrator | Maintain consistent narrative voice | Style parameters |
| Dialogue Crafter | Generate character-appropriate speech | Character profiles |
| Pacing Controller | Adjust rhythm/tempo | Beat timing metadata |
| Sensory Enricher | Add visceral detail | `ENRICHMENT_TECHNIQUES` |

**Key Question This Role Answers**: "How do we make this feel alive on the page?"

---

### 4. 🔍 EDITOR (Quality Guardian)

**Function**: Refines output, maintains coherence, identifies gaps, applies enrichments.

**NCP Layer**: Both layers (validates structure AND presentation)

**Human Example**: Story editor, continuity checker  
**AI Example**: `AnalyticalFeedbackLoop`, `EmotionalBeatEnricher`

**Tools Required**:
| Tool | Purpose | Implementation |
|------|---------|----------------|
| Gap Identifier | Find quality weaknesses | `MultiDimensionalAnalysis` |
| Coherence Scorer | Evaluate narrative consistency | Constraint checking |
| Enrichment Router | Select appropriate fixes | `FlowRoute` system |
| Revision Tracker | Track edit history | Version metadata |
| A/B Comparator | Compare beat variations | Side-by-side view |

**Key Question This Role Answers**: "Is this good enough? If not, what specifically needs improvement?"

---

### 5. 📖 READER (Experience Consumer)

**Function**: Consumes the narrative, provides feedback through engagement signals.

**NCP Layer**: Output consumer (reads presentation, experiences structure)

**Human Example**: Beta reader, audience member  
**AI Example**: Sentiment analyzer, engagement predictor

**Tools Required**:
| Tool | Purpose | Implementation |
|------|---------|----------------|
| Reading Mode | Scroll through beats | Stories Studio UI |
| Annotation Tool | Mark reactions/questions | Margin notes |
| Emotion Logger | Track emotional response | Real-time tagging |
| Pacing Feedback | Signal "too fast"/"too slow" | Reading speed analysis |
| Highlight System | Mark memorable passages | Selection persistence |

**Key Question This Role Answers**: "How does this make me feel? Do I want to keep reading?"

---

### 6. 🤝 COLLABORATOR (Human-AI Bridge)

**Function**: Mediates between human intent and AI generation, translates feedback into prompts.

**NCP Layer**: Interface layer (translates between human and machine)

**Human Example**: Prompt engineer, AI wrangler  
**AI Example**: Intent classifier, prompt optimizer

**Tools Required**:
| Tool | Purpose | Implementation |
|------|---------|----------------|
| Intent Translator | Convert edits to generation guidance | Prompt engineering |
| Regeneration Trigger | Initiate downstream updates | `NarrativeAwareStoryGraph` |
| Conflict Resolver | Handle human/AI disagreements | Manual override + logging |
| Context Injector | Add relevant info to generation | `NCPState` metadata |
| Latency Manager | Optimize for responsiveness | Caching, prefetch |

**Key Question This Role Answers**: "How do I get the AI to understand what I want?"

---

### 7. 🔮 WITNESS (Ceremonial Observer)

**Function**: Holds space for the creative process, validates alignment with deeper purpose.

**NCP Layer**: Meta-layer (observes process, not just output)

**Human Example**: Mentor, ceremony holder, sacred witness  
**AI Example**: Ceremony World protocols (K'é, SNBH, Hózhó)

**Tools Required**:
| Tool | Purpose | Implementation |
|------|---------|----------------|
| Sacred Pause | Interrupt for reflection | Ceremony protocols |
| Alignment Checker | Validate against core values | IAIP Five-Phase |
| Gratitude Logger | Acknowledge contributions | K'é attribution |
| Balance Monitor | Check proportional response | SNBH scoring |
| Coherence Witness | Confirm wholeness | Hózhó validation |

**Key Question This Role Answers**: "Does this serve the deeper purpose we're creating for?"

---

## Part II: Role-Tool Matrix

### Which Tools Support Which Roles?

| Tool/Component | ARCH | STRUCT | STORY | EDIT | READ | COLLAB | WITN |
|----------------|:----:|:------:|:-----:|:----:|:----:|:------:|:----:|
| `NCPState` | ✓ | ✓ | ✓ | ✓ | | ✓ | |
| `StoryBeat` | | ✓ | ✓ | ✓ | ✓ | | |
| `CharacterArcTracker` | | ✓ | | ✓ | | | |
| `EmotionalBeatEnricher` | | | ✓ | ✓ | | | |
| `AnalyticalFeedbackLoop` | | | | ✓ | | ✓ | |
| `NarrativeAwareStoryGraph` | ✓ | ✓ | ✓ | ✓ | | ✓ | |
| Stories Studio UI | | ✓ | | ✓ | ✓ | ✓ | |
| JSON Export/Import | ✓ | ✓ | | | | ✓ | |
| Ceremony Protocols | | | | | | | ✓ |
| Three-Universe Analysis | | | | ✓ | | | ✓ |

---

## Part III: Three-Universe Role Mapping

### How Roles Map to Universe Perspectives

| Role | Primary Universe | Secondary | Why |
|------|-----------------|-----------|-----|
| **ARCHITECT** | 🔧 ENGINEER | | Technical structure design |
| **STRUCTURIST** | 📖 STORY_ENGINE | 🔧 ENGINEER | Narrative logic with technical rigor |
| **STORYTELLER** | 📖 STORY_ENGINE | 🙏 CEREMONY | Artistic expression with ceremonial intent |
| **EDITOR** | 🔧 ENGINEER | 📖 STORY_ENGINE | Technical quality + narrative coherence |
| **READER** | 📖 STORY_ENGINE | 🙏 CEREMONY | Experience story + ceremonial witness |
| **COLLABORATOR** | 🔧 ENGINEER | 📖 STORY_ENGINE | Technical mediation for narrative goals |
| **WITNESS** | 🙏 CEREMONY | | Pure ceremonial presence |

---

## Part IV: Phase-Role Responsibility

### Development Roadmap Roles

| Phase | Description | Primary Roles | Tools to Build |
|-------|-------------|---------------|----------------|
| **1** | JSON Export | ARCHITECT, STRUCTURIST | Schema definition, export functions |
| **2** | UI Beat Editing | STRUCTURIST, EDITOR, READER | Stories Studio components |
| **3** | LLM Synchronization | STORYTELLER, COLLABORATOR | Generator integration, prompt engineering |
| **4** | User Workflows | All roles | Documentation, tutorials, ceremony guides |

---

## Part V: Implementation Status

### Current Storytelling Package Support

| Role | Support Level | Implementation |
|------|--------------|----------------|
| ARCHITECT | ✅ Strong | `ncp-schema.rispec.md`, type definitions |
| STRUCTURIST | ✅ Strong | `NCPAwareStoryGenerator`, `CharacterArcTracker` |
| STORYTELLER | ⚠️ Partial | `EmotionalBeatEnricher` (needs LLM integration) |
| EDITOR | ✅ Strong | `AnalyticalFeedbackLoop`, `MultiDimensionalAnalysis` |
| READER | ⚠️ Partial | Need Stories Studio UI integration |
| COLLABORATOR | ⚠️ Partial | `NarrativeAwareStoryGraph` (needs latency optimization) |
| WITNESS | 🔄 Planned | IAIP bridge exists, ceremony protocols needed |

---

## Part VI: Gap Analysis

### What Each Role Still Needs

**ARCHITECT**:
- [ ] Schema migration tooling
- [ ] Breaking change detector

**STRUCTURIST**:
- [ ] Visual dependency graph
- [ ] Constraint propagation alerts

**STORYTELLER**:
- [ ] Multi-model voice calibration
- [ ] Pacing parameter controls

**EDITOR**:
- [ ] A/B beat comparison UI
- [ ] Revision history browser

**READER**:
- [ ] Scrolling beat reader mode
- [ ] Annotation/highlight persistence

**COLLABORATOR**:
- [ ] Latency optimization (<500ms target)
- [ ] Prompt template library

**WITNESS**:
- [ ] Sacred pause triggers
- [ ] Hózhó coherence dashboard

---

## Appendix: Role Interaction Patterns

### Common Workflows

**Solo Human Writer**:
```
STRUCTURIST → STORYTELLER → EDITOR → READER
     ↑__________________________________|
```

**AI-Assisted Creation**:
```
Human(STRUCTURIST) → AI(STORYTELLER) → Human(EDITOR) → AI(COLLABORATOR) → Human(READER)
                                            ↓
                                    AI(EDITOR/Gap Analysis)
```

**Ceremonial Creation**:
```
WITNESS(opening) → STRUCTURIST → STORYTELLER → EDITOR → WITNESS(closing)
    ↓                                                        ↑
    └──────────────── continuous observation ────────────────┘
```

---

*This specification enables all participants—human and AI—to understand their function and access appropriate tools.*
