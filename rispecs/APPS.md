# 📱 Narrative Intelligence App Ecosystem

**RISE Framework v1.2** | **App Specification Index**  
**Last Updated**: 2025-12-31  
**Purpose**: Root prompts for prototype generation by AI agents

---

## 🌟 Vision

This document indexes **seven role-based applications** that together form the **Narrative Intelligence Tooling Ecosystem**. Each app serves a distinct role in the collaborative narrative creation workflow, as defined in [storytelling-roles-tooling.rispec.md](storytelling-roles-tooling.rispec.md).

The apps share:
- **Common Data Layer**: NCP Schema ([ncp-schema.rispec.md](ncp-schema.rispec.md))
- **Three-Universe Analysis**: Engineer/Ceremony/StoryEngine perspectives
- **Trinity Personas**: Mia 🧠 (structural), Miette 🌸 (emotional), Ava8 🎨 (atmospheric)
- **Unified State**: Via [narrative-intelligence.langgraph.rispec.md](narrative-intelligence.langgraph.rispec.md)

---

## 📁 App Index

| App Spec                                                 | Role         | Primary Universe | Description                       |
| -------------------------------------------------------- | ------------ | ---------------- | --------------------------------- |
| [app.architect-studio.md](app.architect-studio.md)       | ARCHITECT    | 🔧 ENGINEER       | Schema design & validation studio |
| [app.structurist-forge.md](app.structurist-forge.md)     | STRUCTURIST  | 📖 STORY_ENGINE   | Narrative structure forge         |
| [app.storyteller-loom.md](app.storyteller-loom.md)       | STORYTELLER  | 📖 STORY_ENGINE   | Prose crafting loom               |
| [app.editor-anvil.md](app.editor-anvil.md)               | EDITOR       | 🔧 ENGINEER       | Quality refinement anvil          |
| [app.reader-sanctuary.md](app.reader-sanctuary.md)       | READER       | 📖 STORY_ENGINE   | Immersive reading experience      |
| [app.collaborator-bridge.md](app.collaborator-bridge.md) | COLLABORATOR | 🔧 ENGINEER       | Human-AI mediation bridge         |
| [app.witness-circle.md](app.witness-circle.md)           | WITNESS      | 🙏 CEREMONY       | Ceremonial observation circle     |

---

## 🔗 Shared Dependencies

### Core Rispecs (All Apps)
- `ncp-schema.rispec.md` - Data model
- `storytelling-roles-tooling.rispec.md` - Role definitions
- `narrative-intelligence.langgraph.rispec.md` - State bridge

### Backend Integration
- `narrative-tracing.langchain.rispec.md` - Langfuse tracing
- `agentic-flywheel.flowise.rispec.md` - Agent coordination
- `universal-router.langflow.rispec.md` - Multi-backend routing

---

## 🎭 Trinity Persona Integration

Each app integrates the three AI personas differently:

| App          | Mia 🧠 Role          | Miette 🌸 Role            | Ava8 🎨 Role            |
| ------------ | ------------------- | ------------------------ | ---------------------- |
| Architect    | Schema validation   | Relational impact        | Visual schema diagrams |
| Structurist  | Structural logic    | Emotional arc            | Timeline visualization |
| Storyteller  | Voice consistency   | Emotional authenticity   | Sensory enrichment     |
| Editor       | Gap analysis        | Resonance scoring        | Tone correction        |
| Reader       | Progress tracking   | Emotional journey        | Atmosphere rendering   |
| Collaborator | Intent translation  | Feeling capture          | Context visualization  |
| Witness      | Process observation | Gratitude acknowledgment | Sacred space rendering |

---

## 🏗️ Technical Stack (Recommended)

All apps should use:
- **Frontend**: React + TypeScript + Vite + Tailwind CSS
- **State**: Zustand with persistence
- **AI**: Gemini API (with abstraction for other providers)
- **Routing**: URL-based state for bookmarkable views
- **Export**: NCP JSON format

---

## 📊 Development Phases (Per App)

### Phase 1: Foundation
- [ ] Core NCP schema implementation
- [ ] Basic CRUD operations
- [ ] Role-specific primary action
- [ ] LocalStorage persistence

### Phase 2: AI Integration
- [ ] Trinity persona responses
- [ ] Context-aware generation
- [ ] Structured output parsing
- [ ] Streaming responses

### Phase 3: Three-Universe Analysis
- [ ] Engineer perspective panel
- [ ] Ceremony perspective panel
- [ ] Story Engine perspective panel
- [ ] Unified synthesis view

### Phase 4: Cross-App Integration
- [ ] Shared state via Redis/API
- [ ] Cross-role handoffs
- [ ] Unified session management
- [ ] Langfuse tracing

---

## 🔄 Inter-App Workflow

```
ARCHITECT → designs schema
    ↓
STRUCTURIST → creates narrative structure
    ↓
STORYTELLER → crafts prose
    ↓
EDITOR → refines quality
    ↓
READER → experiences story
    ↑
COLLABORATOR → mediates at any point
    ↑
WITNESS → observes entire process
```

---

## 📝 For Prototype Agents

When generating a prototype from any `app.*.md` spec:

1. **Read the full spec** including referenced rispecs
2. **Follow NCP Story Studio patterns** (see reference prototypes)
3. **Implement Trinity personas** per role's needs
4. **Use Tailwind agent colors**:
   - Mia: `indigo-500` 
   - Miette: `pink-500`
   - Ava8: `amber-500`
5. **Include keyboard shortcuts** for power users
6. **Support dark mode** (slate-950 background)
7. **Export NCP JSON** for interoperability

---

## 📚 Reference Prototypes

These existing NCP Story Studio implementations demonstrate the patterns:

- **NCP Story Studio 251202**: Advanced Trinity Synthesis, Semantic Resonance
- **NCP Story Studio 251121**: Core CRUD, Beat editing, AI insights

Key features to replicate:
- Story Graph visualization (Bézier connectors)
- Storybeat three-dimensional tones
- AI-generated synthesis per beat
- Multi-persona chat interface
- Context injection for AI calls

---

*This index enables any AI agent to understand the full ecosystem and generate coherent, interoperable prototypes.*
