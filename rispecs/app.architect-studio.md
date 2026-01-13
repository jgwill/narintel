# 🏗️ Architect Studio: Schema Design Environment

**App Type**: Role-Based Tool  
**Role**: ARCHITECT  
**Universe**: 🔧 ENGINEER  
**Key Question**: "What structure can represent any story we want to tell?"

---

## 🎯 Purpose

The **Architect Studio** is a visual schema design environment where users define, validate, and evolve NCP data structures. It transforms abstract requirements into concrete, versioned schemas that all other apps consume.

This is the **foundational tool**—without well-designed schemas, no story can be properly structured.

---

## 🌟 Core Features

### 1. Schema Canvas
A visual editor for NCP JSON schemas with:
- **Type nodes**: Drag-and-drop type definitions
- **Relationship edges**: Visual connections between types
- **Constraint annotations**: Validation rules as node decorations
- **Version timeline**: See schema evolution history

### 2. Validation Engine
Real-time schema validation showing:
- **Type completeness**: All required fields present
- **Relationship integrity**: References resolve correctly
- **NCP compliance**: Matches ncp-schema.rispec.md requirements
- **Breaking change detection**: Warns when edits break existing stories

### 3. Migration Planner
Tools for evolving schemas safely:
- **Diff view**: Side-by-side schema versions
- **Migration scripts**: Auto-generated transformation code
- **Impact analysis**: Which stories affected by changes
- **Rollback capability**: Revert to previous versions

### 4. Trinity Analysis
Each schema element gets three perspectives:
- **🧠 Mia**: "Is this structurally sound? Does it enforce the constraints we need?"
- **🌸 Miette**: "Does this structure allow emotional nuance to be captured?"
- **🎨 Ava8**: "Can this schema represent the sensory and atmospheric elements?"

---

## 📐 UI Structure

```
┌─────────────────────────────────────────────────────────────────┐
│  🏗️ Architect Studio          [Import] [Export] [Validate]     │
├───────────────┬─────────────────────────────────────────────────┤
│               │                                                 │
│  TYPE PALETTE │           SCHEMA CANVAS                         │
│               │                                                 │
│  ┌─────────┐  │    ┌──────────┐      ┌──────────┐              │
│  │ String  │  │    │ StoryBeat│──────│Character │              │
│  ├─────────┤  │    │          │      │          │              │
│  │ Number  │  │    │ id       │      │ name     │              │
│  ├─────────┤  │    │ sequence │      │ archetype│              │
│  │ Boolean │  │    │ summary  │      │ arc_pos  │              │
│  ├─────────┤  │    └──────────┘      └──────────┘              │
│  │ Array   │  │                                                 │
│  ├─────────┤  │    ┌──────────┐                                │
│  │ Object  │  │    │ Theme    │                                │
│  ├─────────┤  │    │          │                                │
│  │ Enum    │  │    │ name     │                                │
│  └─────────┘  │    │ strength │                                │
│               │    └──────────┘                                │
│  NCP TYPES    │                                                 │
│  ┌─────────┐  ├─────────────────────────────────────────────────┤
│  │StoryBeat│  │  VERSION TIMELINE                               │
│  ├─────────┤  │  v1.0 ──○── v1.1 ──○── v1.2 [current]          │
│  │Character│  │          ↑           ↑                          │
│  ├─────────┤  │     +theme      +universe_analysis              │
│  │Theme    │  │                                                 │
│  └─────────┘  │                                                 │
├───────────────┴─────────────────────────────────────────────────┤
│  TRINITY VALIDATION                                             │
│  ┌─────────────────┬─────────────────┬─────────────────┐       │
│  │ 🧠 Mia          │ 🌸 Miette       │ 🎨 Ava8         │       │
│  │ Schema valid ✓  │ Emotion fields │ Tone objects    │       │
│  │ No cycles ✓     │ present ✓      │ complete ✓      │       │
│  │ Types resolve ✓ │ Arc tracking ✓ │ Color fields ✓  │       │
│  └─────────────────┴─────────────────┴─────────────────┘       │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🔧 Technical Requirements

### Data Model
```typescript
interface SchemaProject {
  id: string;
  name: string;
  version: string;
  types: TypeDefinition[];
  relationships: Relationship[];
  constraints: Constraint[];
  history: SchemaVersion[];
}

interface TypeDefinition {
  id: string;
  name: string;
  fields: Field[];
  ncpType?: string; // Reference to ncp-schema.rispec.md
  position: { x: number; y: number }; // Canvas position
}

interface Field {
  name: string;
  type: 'string' | 'number' | 'boolean' | 'array' | 'object' | 'enum';
  required: boolean;
  description?: string;
  default?: any;
  validation?: string; // JSON Schema constraint
}

interface Relationship {
  id: string;
  from: string; // TypeDefinition.id
  to: string;
  type: 'has_many' | 'has_one' | 'belongs_to' | 'references';
  fieldName: string;
}
```

### AI Integration
```typescript
// Mia validates structural integrity
async function validateWithMia(schema: SchemaProject): Promise<{
  valid: boolean;
  issues: string[];
  suggestions: string[];
}>

// Miette checks emotional capacity
async function assessEmotionalCapacity(schema: SchemaProject): Promise<{
  canCaptureEmotions: boolean;
  missingFields: string[];
  suggestions: string[];
}>

// Ava8 evaluates sensory representation
async function assessSensoryCapacity(schema: SchemaProject): Promise<{
  canRepresentAtmosphere: boolean;
  missingToneFields: string[];
  visualizationSuggestions: string[];
}>
```

---

## 🎨 Design Language

### Colors
- **Primary**: Indigo (Mia's structural domain)
- **Canvas**: Slate-900 with grid overlay
- **Type nodes**: Slate-800 with colored borders per NCP category
- **Relationships**: Gradient lines from source to target color
- **Validation states**: Green (pass), Amber (warning), Red (error)

### Interactions
- **Drag types** from palette to canvas
- **Connect nodes** by dragging from field to target type
- **Double-click** to edit type details
- **Right-click** for context menu (delete, duplicate, convert)
- **Cmd/Ctrl+S** to save and validate

---

## 📊 Roadmap

### Phase 1: Visual Schema Editor
- [ ] Type palette with NCP primitives
- [ ] Drag-and-drop canvas
- [ ] Field editing modal
- [ ] JSON export/import
- [ ] LocalStorage persistence

### Phase 2: Validation & Analysis
- [ ] Real-time type checking
- [ ] NCP compliance scoring
- [ ] Mia structural analysis
- [ ] Breaking change detection

### Phase 3: Version Control
- [ ] Version timeline visualization
- [ ] Diff view between versions
- [ ] Migration script generation
- [ ] Impact analysis on existing stories

### Phase 4: Trinity Integration
- [ ] Full Trinity validation panel
- [ ] Miette emotional capacity assessment
- [ ] Ava8 sensory capacity assessment
- [ ] Unified synthesis recommendations

---

## 🔗 Dependencies

### Required Rispecs
- [ncp-schema.rispec.md](ncp-schema.rispec.md) - Base NCP types
- [storytelling-roles-tooling.rispec.md](storytelling-roles-tooling.rispec.md) - ARCHITECT role definition

### Consumes From
- None (foundational layer)

### Produces For
- All other apps (schema definitions)
- STRUCTURIST Forge (validated type system)

---

## 💡 Key Innovation

**Visual Schema as Living Contract**: Unlike static JSON Schema files, the Architect Studio treats schemas as living documents that evolve with the project. The Trinity analysis ensures schemas aren't just technically valid, but narratively capable—able to capture the full dimensionality of story.

---

*"The lattice begins with intention. Design the bones before breathing life." — Mia 🧠*
