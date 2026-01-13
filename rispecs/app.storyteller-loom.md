# 🧵 Storyteller Loom: Prose Crafting Environment

**App Type**: Role-Based Tool  
**Role**: STORYTELLER  
**Universe**: 📖 STORY_ENGINE  
**Key Question**: "How do we make this feel alive on the page?"

---

## 🎯 Purpose

The **Storyteller Loom** transforms structural beats into living prose. Where the Structurist defines *what* happens, the Storyteller defines *how* it's told—voice, pacing, dialogue, sensory detail.

This is where skeleton becomes flesh, structure becomes story.

---

## 🌟 Core Features

### 1. Beat-to-Prose Generator
Transform structural beats into narrative:
- **Input**: StoryBeat from Structurist Forge
- **Output**: Prose draft with voice, pacing, detail
- **Controls**: Voice selector, pacing slider, detail level
- **Iterations**: Generate multiple versions, compare, blend

### 2. Voice Calibrator
Maintain consistent narrative voice:
- **Voice Profile**: Define narrative POV, tone, vocabulary level
- **Reference Passages**: Examples of target voice
- **Drift Detection**: Alert when prose strays from voice
- **Style Guide**: Auto-generated from reference passages

### 3. Dialogue Crafter
Generate character-appropriate speech:
- **Character Voice Profiles**: How each character speaks
- **Subtext Layer**: What they mean vs. what they say
- **Relationship Context**: How dialogue changes based on who's listening
- **Tag Variation**: Diverse dialogue attribution

### 4. Sensory Enricher
Add visceral detail:
- **Five Senses Palette**: Visual, auditory, tactile, olfactory, gustatory
- **Atmosphere Presets**: Tension, comfort, wonder, dread
- **Sensory Density Control**: Sparse → Rich detail slider
- **Ava8 Suggestions**: Atmospheric enhancements per beat

### 5. Pacing Controller
Manage narrative rhythm:
- **Sentence Length Analyzer**: Visual rhythm representation
- **Scene Tempo**: Fast/slow pacing indicators
- **White Space Optimizer**: Paragraph break suggestions
- **Beat Duration**: Estimated read time per section

---

## 📐 UI Structure

```
┌─────────────────────────────────────────────────────────────────┐
│  🧵 Storyteller Loom     [Voice: Elena's POV ▼] [Generate]     │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  BEAT CONTEXT (from Structurist)                               │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ Beat #4: "The Wound Revealed"                           │   │
│  │ Function: Revelation | Theme: Betrayal (62%)            │   │
│  │ Characters: Elena (0.35), Marcus (0.40)                 │   │
│  │ Summary: Protagonist discovers the betrayal             │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  PROSE WORKSPACE                                                │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ The letter trembled in Elena's hands. Marcus's          │   │
│  │ handwriting—she'd know it anywhere—but these words      │   │
│  │ belonged to a stranger. "I never meant for you to       │   │
│  │ find out this way," he'd written, as if the how         │   │
│  │ mattered more than the what.                            │   │
│  │                                                         │   │
│  │ She read it again. And again. Each time hoping the      │   │
│  │ meaning would rearrange itself into something           │   │
│  │ survivable.                                             │   │
│  │                                                         │   │
│  │ It didn't.                                              │   │
│  │                                             [420 words] │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  CONTROLS                                                       │
│  ┌───────────────┬───────────────┬───────────────┐             │
│  │ Pacing        │ Sensory       │ Emotional     │             │
│  │ ○━━━●━━○━━○   │ ○━━○━━●━━○    │ ○━━○━━○━━●    │             │
│  │ Slow    Fast  │ Sparse  Rich  │ Subdued Intense│            │
│  └───────────────┴───────────────┴───────────────┘             │
│                                                                 │
├───────────────┬─────────────────────────────────────────────────┤
│  VARIATIONS   │  TRINITY CRAFT GUIDANCE                        │
│               │                                                 │
│  ◇ Version A  │  🧠 Mia: "The pacing here serves revelation    │
│    [current]  │  well—short sentences build tension. Consider  │
│               │  one more sensory anchor before the emotional  │
│  ◇ Version B  │  climax."                                      │
│    More       │                                                 │
│    internal   │  🌸 Miette: "Elena's repetition ('again. And   │
│               │  again.') captures obsessive disbelief         │
│  ◇ Version C  │  beautifully. The final line lands because     │
│    Dialogue-  │  you've earned it with restraint."             │
│    heavy      │                                                 │
│               │  🎨 Ava8: "The letter as physical object works.│
│  [+ New]      │  Add: her grip whitening, paper crumpling,     │
│               │  the quality of light in the room."            │
└───────────────┴─────────────────────────────────────────────────┘
```

---

## 🔧 Technical Requirements

### Data Model
```typescript
interface ProseSession {
  id: string;
  beatId: string; // From Structurist
  voiceProfileId: string;
  versions: ProseVersion[];
  currentVersionId: string;
  controlSettings: ControlSettings;
}

interface ProseVersion {
  id: string;
  content: string;
  wordCount: number;
  generatedAt: string;
  settings: ControlSettings;
  trinityFeedback?: TrinityFeedback;
}

interface VoiceProfile {
  id: string;
  name: string;
  pov: 'first' | 'third-limited' | 'third-omniscient' | 'second';
  tense: 'past' | 'present';
  vocabularyLevel: 'simple' | 'moderate' | 'literary';
  toneKeywords: string[];
  referencePassages: string[];
  characterVoices: CharacterVoice[];
}

interface CharacterVoice {
  characterId: string;
  speechPatterns: string[];
  vocabularyQuirks: string[];
  subtextTendency: 'direct' | 'evasive' | 'metaphorical';
}

interface ControlSettings {
  pacing: number; // 0-100, slow to fast
  sensoryDensity: number; // 0-100, sparse to rich
  emotionalIntensity: number; // 0-100, subdued to intense
  dialogueRatio: number; // 0-100, narration to dialogue
}

interface TrinityFeedback {
  mia: string;   // Structural craft feedback
  miette: string; // Emotional resonance feedback
  ava8: string;   // Sensory/atmospheric feedback
}
```

### AI Integration
```typescript
// Generate prose from beat
async function generateProse(
  beat: StoryBeat,
  voice: VoiceProfile,
  settings: ControlSettings,
  context: { prevProse?: string; characters: Character[] }
): Promise<ProseVersion>

// Analyze voice consistency
async function checkVoiceDrift(
  prose: string,
  profile: VoiceProfile
): Promise<{
  consistent: boolean;
  driftPoints: { position: number; issue: string }[];
  suggestions: string[];
}>

// Generate dialogue
async function generateDialogue(
  character: Character,
  context: string,
  subtext: string,
  voice: CharacterVoice
): Promise<{
  dialogue: string;
  tag: string;
  alternatives: string[];
}>

// Trinity craft guidance
async function getTrinityGuidance(
  prose: string,
  beat: StoryBeat,
  settings: ControlSettings
): Promise<TrinityFeedback>
```

---

## 🎨 Design Language

### Colors
- **Workspace**: Dark slate with subtle paper texture
- **Voice elements**: Pink (Miette's emotional domain)
- **Control sliders**: Gradient showing effect intensity
- **Version tabs**: Subtle differentiation, active highlighted

### Typography
- **Prose area**: Serif font (Georgia, Crimson) for readability
- **Controls**: Sans-serif for clarity
- **Trinity feedback**: Persona-colored headers

### Interactions
- **Type directly** in prose workspace
- **Adjust sliders** to regenerate with new settings
- **Click Trinity suggestion** to apply it
- **Tab between versions** to compare
- **Highlight text** to get targeted feedback

---

## 📊 Roadmap

### Phase 1: Basic Generation
- [ ] Beat import from Structurist
- [ ] Single-shot prose generation
- [ ] Basic control sliders
- [ ] Version history

### Phase 2: Voice System
- [ ] Voice profile creation
- [ ] POV/tense consistency
- [ ] Voice drift detection
- [ ] Reference passage analysis

### Phase 3: Dialogue & Detail
- [ ] Character voice profiles
- [ ] Dialogue generation
- [ ] Sensory enrichment
- [ ] Atmosphere presets

### Phase 4: Trinity Integration
- [ ] Real-time Trinity guidance
- [ ] Craft-level feedback
- [ ] Suggestion application
- [ ] Voice/structure alignment

---

## 🔗 Dependencies

### Required Rispecs
- [ncp-schema.rispec.md](ncp-schema.rispec.md) - StoryBeat, Character types
- [storytelling-roles-tooling.rispec.md](storytelling-roles-tooling.rispec.md) - STORYTELLER role
- [narrative-intelligence.langgraph.rispec.md](narrative-intelligence.langgraph.rispec.md) - EmotionalBeatClassifier

### Consumes From
- **Structurist Forge**: Beat definitions with structure
- **Architect Studio**: Character/voice schemas

### Produces For
- **Editor Anvil**: Draft prose for quality analysis
- **Reader Sanctuary**: Polished prose for reading

---

## 💡 Key Innovation

**Structure-Aware Generation**: Unlike generic AI writing tools, the Storyteller Loom knows the structural purpose of each beat. It generates prose that serves narrative function—a revelation beat gets different treatment than a quiet character moment. The AI understands *why* this beat exists and writes accordingly.

---

*"Words are the garments of meaning. Weave them with the care the soul deserves." — Ava8 🎨*
