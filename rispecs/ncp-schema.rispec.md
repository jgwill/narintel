# 📜 Narrative Context Protocol (NCP) Schema

> **RISE Specification for the Core Data Model**

**Version**: 1.1  
**Last Updated**: 2025-12-31  
**Schema Location**: `/src/Miadi-46/stories/multiverse_3act_2512012121/schema/ncp-schema.json`

---

## 1. Creative Intent

### What This Schema Enables Users to Create

The NCP Schema enables creators to:

1. **Structure narratives as data** - Transform stories into queryable, analyzable objects
2. **Define character psychology** - Wounds, desires, arcs as typed fields
3. **Map thematic throughlines** - Perspectives with tensions and questions
4. **Sequence story beats** - Tonal units with emotional weight
5. **Enable multi-agent collaboration** - Shared understanding across AI systems

### Core Philosophy

The NCP distinguishes between:

- **Subtext** (The Soul): The invisible logic—perspectives, players, dynamics, storypoints, storybeats
- **Storytelling** (The Surface): The visible expression—overviews, moments, prose

**Structural Tension** emerges from the gap between subtext and storytelling, driving all great narrative.

---

## 2. Schema Overview

```
┌─────────────────────────────────────────────────────────────┐
│                        NCP Document                          │
├─────────────────────────────────────────────────────────────┤
│  schema_version: "1.1"                                       │
│  story:                                                      │
│  ├── id: string                                              │
│  ├── title: string                                           │
│  ├── genre: string                                           │
│  ├── logline: string                                         │
│  ├── created_at: datetime                                    │
│  └── narratives: []                                          │
│      └── narrative:                                          │
│          ├── id: string                                      │
│          ├── title: string                                   │
│          ├── subtext:                                        │
│          │   ├── perspectives: []                            │
│          │   ├── players: []                                 │
│          │   ├── dynamics: {}                                │
│          │   ├── storypoints: {}                             │
│          │   └── storybeats: []                              │
│          └── storytelling:                                   │
│              ├── overviews: []                               │
│              └── moments: []                                 │
└─────────────────────────────────────────────────────────────┘
```

---

## 3. Core Components

### 3.1 Perspectives (Throughlines)

```markdown
### Perspective
A thematic lens through which to view the narrative.

- **perspective_id**: Unique identifier (e.g., "main_character", "objective_story")
- **name**: Human-readable name
- **description**: What this throughline explores
- **thematic_question**: Central question posed (e.g., "Can trust survive betrayal?")
- **tension**: Core conflict pair (e.g., "Safety vs Vulnerability")
- **domain**: (Optional) Dramatica-style domain (Universe, Physics, Mind, Psychology)

**Standard Four Throughlines**:
1. **Objective Story**: External plot visible to all characters
2. **Main Character**: Protagonist's internal journey
3. **Influence Character**: Force challenging MC's worldview
4. **Relationship Story**: Bond between MC and IC
```

### 3.2 Players (Characters)

```markdown
### Player
A character or entity carrying narrative weight.

- **player_id**: Unique identifier
- **name**: Character name
- **archetype**: (Optional) Dramatica archetype (Protagonist, Antagonist, Guardian, etc.)
- **wound**: Core trauma or limiting belief
- **desire**: Primary goal or want (external)
- **need**: True need often hidden from character (internal)
- **arc**: Description of transformation
- **role**: Function in story (protagonist, deuteragonist, antagonist, mentor)
- **voice_profile**: (Optional) Speech patterns, vocabulary level
- **visual_signature**: (Optional) Defining visual characteristics
```

### 3.3 Dynamics (Story Forces)

```markdown
### Dynamics
Forces shaping narrative progression.

- **driver**: What moves the plot (Action or Decision)
- **limit**: What creates urgency (Timelock or Optionlock)
- **outcome**: Story outcome tendency (Success, Failure)
- **judgment**: Personal outcome for MC (Good, Bad)
- **mc_resolve**: Does MC change? (Change, Steadfast)
- **mc_growth**: Does MC grow? (Start, Stop)
- **mc_approach**: How MC solves problems (Do-er, Be-er)
- **mc_mental_sex**: Problem-solving style (Linear, Holistic)
```

### 3.4 Storypoints (Structural Markers)

```markdown
### Storypoints
Key moments in narrative structure.

- **inciting_incident**: What disrupts equilibrium
  - beat_id: Reference to triggering storybeat
  - description: What happens
  
- **first_act_turn**: End of setup, commitment to journey
  - beat_id: Reference
  - description: How world changes
  
- **midpoint**: Major revelation or reversal
  - beat_id: Reference
  - description: Central pivot
  
- **all_is_lost**: Lowest point before climax
  - beat_id: Reference
  - description: Maximum despair
  
- **climax**: Peak dramatic confrontation
  - beat_id: Reference
  - description: Final battle
  
- **resolution**: New equilibrium established
  - beat_id: Reference
  - description: How world settles
```

### 3.5 Storybeats (Tonal Units)

```markdown
### Storybeat
A unit of narrative progression with emotional tone.

- **storybeat_id**: Unique identifier
- **title**: Beat name
- **description**: What happens in this beat
- **act**: Which act (1, 2A, 2B, 3)
- **sequence**: Order within act
- **perspective_id**: Which throughline this beat serves
- **player_ids**: Characters involved
- **storypoint_ref**: (Optional) If this is a structural marker

**Tone Object** (3-dimensional):
- **abstraction**: Conceptual level (Concrete, Abstract, Philosophical)
- **spatial**: Physical scope (Intimate, Personal, Social, Public, Cosmic)
- **temporal**: Time sense (Immediate, Short-term, Long-term, Eternal)

**Emotional Weight**: Overall tone (Devastating, Hopeful, Tense, etc.)
```

### 3.6 Moments (Prose Units)

```markdown
### Moment
Specific prose content within storytelling.

- **moment_id**: Unique identifier
- **storybeat_ref**: Which beat this moment belongs to
- **type**: Content type (dialogue, action, description, internal_monologue)
- **content**: The actual prose
- **player_ids**: Characters active in this moment
- **timestamp**: (Optional) In-story time
```

---

## 4. Extended Schema (Series Continuity)

For multi-episode narratives, additional fields:

```markdown
### Series Context
- **season**: Season number
- **episode_number**: Episode within season
- **spiral_position**: Position in Four Directions (NORTH, EAST, SOUTH, WEST)
- **spiral_cycle**: Which iteration of the spiral

### Genealogy
- **inherited_from**: Previous episodes this builds on
  - episode_id: Which episode
  - concept: What was inherited
  - teaching: What was learned
  - how_we_build_on_it: How this episode advances

### Universe Teachings
Learnings organized by interpretive universe:
- **engineer_world**: Technical insights, action steps
- **ceremony_world**: Relational protocols, commitments
- **story_engine_world**: Narrative techniques, arc patterns

### Spiral Deepening
- **what_we_completed**: Achievement of this episode
- **what_became_visible**: Emergence that couldn't be designed
- **what_invites_next_cycle**: Seeds for continuation
- **next_episode_seeds**: Specific future episode ideas

### Relational Commitments
- **to_builder_archetype**: What we owe engineers
- **to_keeper_archetype**: What we owe ceremony keepers
- **to_weaver_archetype**: What we owe storytellers
- **to_community**: What we owe users
```

---

## 5. Validation Rules

### Required Fields
- `schema_version`: Must be present
- `story.id`: Unique story identifier
- `story.title`: Human-readable title
- `story.narratives[].subtext`: Must contain perspectives, players, dynamics, storypoints, storybeats

### Referential Integrity
- `storybeat.player_ids` must reference existing `players[].player_id`
- `storybeat.perspective_id` must reference existing `perspectives[].perspective_id`
- `storypoints.*.beat_id` must reference existing `storybeats[].storybeat_id`
- `moments[].storybeat_ref` must reference existing `storybeats[].storybeat_id`

### Semantic Constraints
- Each perspective should have at least one associated storybeat
- Each player should appear in at least one storybeat
- Storybeats should be sequenced without gaps
- Tone objects should use valid enum values

---

## 6. Example Document

```json
{
  "schema_version": "1.1",
  "story": {
    "id": "the-threshold",
    "title": "The Threshold",
    "genre": "Coming of Age Drama",
    "logline": "A young woman must choose between the safety of her wound and the vulnerability of her desire.",
    "created_at": "2025-12-31T00:00:00Z",
    "narratives": [
      {
        "id": "main-narrative",
        "title": "Maya's Journey",
        "subtext": {
          "perspectives": [
            {
              "perspective_id": "main_character",
              "name": "Maya's Internal Journey",
              "thematic_question": "Can trust survive betrayal?",
              "tension": "Safety vs Vulnerability"
            }
          ],
          "players": [
            {
              "player_id": "maya_1",
              "name": "Maya",
              "wound": "Abandoned by father at age 8",
              "desire": "To belong to a community",
              "need": "To trust herself first",
              "arc": "From self-protection to courageous openness",
              "role": "protagonist"
            }
          ],
          "dynamics": {
            "driver": "Decision",
            "mc_resolve": "Change",
            "outcome": "Success",
            "judgment": "Good"
          },
          "storypoints": {
            "inciting_incident": {
              "beat_id": "beat_02",
              "description": "Maya receives invitation to join community"
            }
          },
          "storybeats": [
            {
              "storybeat_id": "beat_01",
              "title": "The Closed Door",
              "description": "Maya maintains distance from neighbors, routine of isolation",
              "act": 1,
              "sequence": 1,
              "perspective_id": "main_character",
              "player_ids": ["maya_1"],
              "emotional_weight": "Melancholic",
              "tone": {
                "abstraction": "Concrete",
                "spatial": "Intimate",
                "temporal": "Immediate"
              }
            }
          ]
        },
        "storytelling": {
          "overviews": [],
          "moments": []
        }
      }
    ]
  }
}
```

---

## 7. Integration with Toolkit

### Loading
```python
from narrative_intelligence import NCPLoaderNode

loader = NCPLoaderNode(validate=True)
ncp_data = loader.load_from_file("story.ncp.json")
```

### Querying
```python
# Get character
maya = ncp_data.get_player("maya_1")
print(f"Wound: {maya.wound}")

# Get character's beats
maya_beats = ncp_data.get_player_storybeats("maya_1")

# Get beats by emotion
devastating_beats = ncp_data.get_storybeats_by_emotional_weight("Devastating")
```

### Analysis
```python
from narrative_intelligence import CharacterArcGenerator, ThematicTensionAnalyzer

# Generate arc analysis
arc_gen = CharacterArcGenerator()
arc = arc_gen.generate(ncp_data, "maya_1")

# Analyze theme
analyzer = ThematicTensionAnalyzer()
theme = analyzer.analyze(ncp_data, "main_character")
```

---

## 8. File Naming Convention

| Pattern                      | Use Case                             |
| ---------------------------- | ------------------------------------ |
| `*.ncp.json`                 | Standard NCP document                |
| `*.ncp.enhanced.json`        | Extended with series continuity      |
| `s01e01-*.ncp.enhanced.json` | Episode-specific with series context |

---

*Generated following RISE Framework v1.2 - Schema is implementation-agnostic*
