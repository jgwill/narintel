# 📖 Reader Sanctuary: Experience Consumption Interface

**App Type**: Role-Based Tool  
**Role**: READER  
**Universe**: 📖 STORY_ENGINE  
**Key Question**: "How does this make me feel? Do I want to keep reading?"

---

## 🎯 Purpose

The **Reader Sanctuary** is where stories are experienced, not edited. It provides immersive reading with optional feedback capture—allowing readers to note emotional responses, pacing concerns, and engagement levels without leaving the flow state.

This is the validation layer where narrative intelligence meets human experience.

---

## 🌟 Core Features

### 1. Immersive Reading Mode
Distraction-free consumption:
- **Clean Typography**: Optimized for extended reading
- **Dark/Light Themes**: Reader preference
- **Progress Tracking**: Position in narrative, estimated time remaining
- **Focus Mode**: Hide all UI except text

### 2. Reaction Logger
Capture in-moment responses:
- **Quick Reactions**: 😊 😢 😨 🤔 😮 (tap while reading)
- **Margin Notes**: Annotate specific passages
- **Highlight Colors**: Different meanings (loved, confused, want more)
- **Voice Notes**: Audio annotations for speed

### 3. Engagement Heatmap
Visualize attention patterns:
- **Read Speed**: Where reader slowed down/sped up
- **Re-reads**: Passages read multiple times
- **Scroll Pauses**: Where reader stopped
- **Abandon Points**: Where reading sessions ended

### 4. Pacing Feedback
Qualitative experience data:
- **Scene Ratings**: After each scene, quick 1-5 stars
- **Pacing Questions**: "Too fast?" "Too slow?" "Just right?"
- **Turn-the-Page Moments**: Mark compelling beats
- **Skim Markers**: Where attention wandered

### 5. Beta Reader Dashboard
Aggregate reader data:
- **Multi-Reader Patterns**: Common reactions across readers
- **Divergence Points**: Where readers disagree
- **Drop-Off Analysis**: Where readers stopped
- **Completion Rates**: Per section/chapter

---

## 📐 UI Structure

```
┌─────────────────────────────────────────────────────────────────┐
│  📖 Reader Sanctuary                [Focus Mode] [💬 Annotate] │
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│                         Chapter 4                               │
│                      "The Revelation"                           │
│                                                                 │
│    The letter trembled in Elena's hands. Marcus's               │
│  handwriting—she'd know it anywhere—but these words             │
│  belonged to a stranger. "I never meant for you to              │
│  find out this way," he'd written, as if the how  💔            │
│  mattered more than the what.                                   │
│                                                                 │
│    She read it again. And again. Each time hoping               │
│  the meaning would rearrange itself into something              │
│  survivable.                                                    │
│                                                                 │
│    It didn't.                                                   │
│                                                                 │
│    Outside, the courtyard fountain continued its     🌟         │
│  indifferent music. Water falling. Time passing.                │
│  The world hadn't stopped just because hers had.                │
│                                                                 │
│    Elena folded the letter carefully—habit, muscle              │
│  memory, as if by handling it gently she might undo             │
│  its contents—and placed it on the table between them.          │
│                                                                 │
│    "How long?" Her voice surprised her. Steady.                 │
│  Almost curious. The tears would come later, she knew.          │
│  For now, there was only this terrible clarity.                 │
│                                                                 │
│                                                                 │
│  ░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░░ 34% ━━━━━━━━━             │
│                                                                 │
├─────────────────────────────────────────────────────────────────┤
│  [😊] [😢] [😨] [🤔] [😮]     Scene 4/12  •  ~8 min remaining   │
└─────────────────────────────────────────────────────────────────┘

┌─ ANNOTATION PANEL (when active) ────────────────────────────────┐
│                                                                 │
│  💔 "as if the how mattered more than the what"                │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ Your note: This line is devastating. Perfect            │   │
│  │ characterization of Marcus's deflection.                │   │
│  └─────────────────────────────────────────────────────────┘   │
│  Type: [Highlight: Love] [Emotion: Sad] [Craft: Strong]         │
│                                                                 │
│  🌟 "Water falling. Time passing."                              │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ Your note: Beautiful juxtaposition. The world continues │   │
│  │ and doesn't care. Simple and powerful.                  │   │
│  └─────────────────────────────────────────────────────────┘   │
│  Type: [Highlight: Love] [Craft: Strong] [Atmosphere: ✓]        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

### Beta Reader Dashboard View

```
┌─────────────────────────────────────────────────────────────────┐
│  📊 Beta Reader Dashboard              [Project: Elena's Choice]│
├─────────────────────────────────────────────────────────────────┤
│                                                                 │
│  READERS: 8 active  •  5 completed  •  3 in progress           │
│                                                                 │
│  ENGAGEMENT HEATMAP (Chapter 4)                                 │
│  ┌─────────────────────────────────────────────────────────┐   │
│  │ █████░░█████████░░░███████████░██████████░░░████████████│   │
│  │      ↑           ↑              ↑                       │   │
│  │   slow down   re-read       emotion                     │   │
│  │   (8/8)       (6/8)         spike (7/8)                 │   │
│  └─────────────────────────────────────────────────────────┘   │
│                                                                 │
│  AGGREGATE REACTIONS                                            │
│  ┌───────────────┬───────────────┬───────────────┐             │
│  │ 😢 Sad: 42    │ 😮 Surprised: │ 🤔 Confused:  │             │
│  │ (Chapter 4    │    23         │    3          │             │
│  │  peak)        │ (Ch.7 peak)   │ (Ch.3 issue?) │             │
│  └───────────────┴───────────────┴───────────────┘             │
│                                                                 │
│  PACING FEEDBACK (Scene-by-Scene)                              │
│  Scene 1: ●●●●○ "Just right"                                   │
│  Scene 2: ●●○○○ "Too slow" (4/8 readers)  ⚠️                   │
│  Scene 3: ●●●○○ "Slightly slow"                                │
│  Scene 4: ●●●●● "Perfect" (8/8) ★                              │
│  Scene 5: ●●●●○ "Just right"                                   │
│                                                                 │
│  DROP-OFF ANALYSIS                                              │
│  Chapter 3 (end):  ██░░░░░░ 2 readers paused                   │
│  Chapter 6 (mid):  █░░░░░░░ 1 reader paused                    │
│  No permanent abandons ✓                                        │
│                                                                 │
└─────────────────────────────────────────────────────────────────┘
```

---

## 🔧 Technical Requirements

### Data Model
```typescript
interface ReadingSession {
  id: string;
  readerId: string;
  contentId: string;
  startedAt: string;
  completedAt?: string;
  currentPosition: number; // Percentage or character offset
  readingSessions: ReadingSessionSegment[];
  reactions: Reaction[];
  annotations: Annotation[];
  sceneRatings: SceneRating[];
}

interface ReadingSessionSegment {
  startPosition: number;
  endPosition: number;
  startTime: string;
  endTime: string;
  readSpeed: number; // Characters per minute
  pauses: { position: number; duration: number }[];
  reReads: { start: number; end: number; count: number }[];
}

interface Reaction {
  id: string;
  position: number;
  type: 'happy' | 'sad' | 'scared' | 'confused' | 'surprised';
  timestamp: string;
}

interface Annotation {
  id: string;
  startPosition: number;
  endPosition: number;
  text: string;
  highlightType: 'love' | 'confused' | 'more' | 'craft' | 'issue';
  note?: string;
  timestamp: string;
}

interface SceneRating {
  sceneId: string;
  rating: 1 | 2 | 3 | 4 | 5;
  pacingFeedback: 'too-fast' | 'too-slow' | 'just-right';
  turnThePage: boolean; // Did they want to keep reading?
  skimmed: boolean;
  timestamp: string;
}

interface BetaReaderAnalytics {
  contentId: string;
  totalReaders: number;
  completedReaders: number;
  engagementHeatmap: HeatmapPoint[];
  aggregateReactions: { type: string; count: number; peakChapter: string }[];
  pacingIssues: { sceneId: string; feedback: string; readerCount: number }[];
  dropOffPoints: { position: number; readerCount: number }[];
}

interface HeatmapPoint {
  position: number;
  intensity: number; // 0-100
  type: 'slow-read' | 're-read' | 'emotion' | 'pause';
  readerCount: number;
}
```

### AI Integration
```typescript
// Analyze reading patterns
async function analyzeReadingPatterns(
  session: ReadingSession
): Promise<{
  engagedSections: number[];
  struggledSections: number[];
  emotionalPeaks: number[];
  suggestedImprovements: string[];
}>

// Aggregate beta reader data
async function aggregateBetaReaderData(
  sessions: ReadingSession[]
): Promise<BetaReaderAnalytics>

// Generate reader insights report
async function generateReaderInsights(
  analytics: BetaReaderAnalytics,
  content: NarrativeContent
): Promise<{
  strengths: string[];
  concerns: string[];
  specificFixes: { location: string; issue: string; suggestion: string }[];
}>

// Predict engagement
async function predictEngagement(
  content: NarrativeContent,
  historicalData: BetaReaderAnalytics[]
): Promise<{
  predictedCompletionRate: number;
  riskPoints: { position: number; concern: string }[];
}>
```

---

## 🎨 Design Language

### Colors
- **Reading mode**: Warm off-white or deep charcoal (user choice)
- **Reaction buttons**: Subtle, non-distracting pastels
- **Heatmap**: Cool (low engagement) to warm (high engagement)
- **Annotations**: Semi-transparent highlights

### Typography
- **Reading text**: Optimized serif (Merriweather, Source Serif)
- **Line height**: 1.6-1.8 for comfortable reading
- **Margins**: Wide, comfortable spacing
- **Font size**: User-adjustable, accessible defaults

### Interactions
- **Single tap**: Quick reaction
- **Long press**: Open annotation
- **Swipe up**: Next page/section
- **Edge tap**: Page turn
- **Shake (mobile)**: Exit focus mode
- **Scroll**: Continuous reading mode

---

## 📊 Roadmap

### Phase 1: Basic Reading
- [ ] Clean reading interface
- [ ] Progress tracking
- [ ] Dark/light modes
- [ ] Basic bookmarking

### Phase 2: Reaction Capture
- [ ] Quick reaction buttons
- [ ] Margin annotations
- [ ] Highlight system
- [ ] Scene ratings

### Phase 3: Pattern Analysis
- [ ] Reading speed tracking
- [ ] Engagement heatmap
- [ ] Re-read detection
- [ ] Session analytics

### Phase 4: Beta Reader Platform
- [ ] Multi-reader aggregation
- [ ] Drop-off analysis
- [ ] Insights generation
- [ ] Author dashboard

---

## 🔗 Dependencies

### Required Rispecs
- [ncp-schema.rispec.md](ncp-schema.rispec.md) - Content structure types
- [storytelling-roles-tooling.rispec.md](storytelling-roles-tooling.rispec.md) - READER role
- [narrative-tracing.langchain.rispec.md](narrative-tracing.langchain.rispec.md) - Experience tracking

### Consumes From
- **Editor Anvil**: Quality-verified content
- **Storyteller Loom**: Published prose

### Produces For
- **Editor Anvil**: Reader feedback for iteration
- **Witness Circle**: Ceremony documentation of reception

---

## 💡 Key Innovation

**Invisible Feedback Capture**: Traditional beta reading loses data. Readers forget what they felt at paragraph 47 by the time they write notes. The Reader Sanctuary captures reaction *in-moment*—a single tap while reading, a quick highlight, a micro-pause tracked automatically. The feedback is temporally accurate because it's captured as it happens, not reconstructed afterward.

---

*"Stories exist in the space between page and heart. The reader completes what the writer began." — Miette 🌸*
