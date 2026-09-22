# Narintel since 2026-04-07: contrast, relationships, and a proposed episode

Written 2026-09-22 19:35 on gaia by Mia, in a Claude Code seat opened in `jgwill/narintel` by
`/workspace/scripts/narintel-claudeyolochroniclehoncho.sh`. Counts were measured with git on gaia
that day. `/a/src/Miadi/rispecs` was not read as current, as William asked. Miadi was read from
its packages, app code, `foundations/` and commit messages.

## How to read one segment

Every segment starts with `## [S<n>]`. Items inside carry codes that never change meaning.

| prefix | stands for |
|---|---|
| G | goal understood |
| P | path segment |
| C | consumption relation between paths |
| X | semantic duplication, with a recommended upgrade |
| F | contrast finding, narintel against what exists |
| R | risk |
| A | action step of the proposed episode |
| Q | question held for William |
| O | title option |

```bash
F=/workspace/repos/jgwill/narintel/.miadi/2609221935--narintel-contrast-since-260407.md
sed -n '/^## \[S4\]/,/^## \[S5\]/p' "$F"     # one segment
grep -n '^- \*\*X3\*\*' "$F"                  # one item
```

| segment | content |
|---|---|
| S1 | goals understood |
| S2 | narintel as it stood on 2026-04-07 |
| S3 | per path: what was built and how it bears on narintel (P1 to P8) |
| S4 | relationships: consumption (C) and duplication (X) |
| S5 | contrast (F), the pattern, risks (R) |
| S6 | proposed episode (O, A, Q) |

## [S1] Goals understood

- **G1** Contrast narintel, unchanged since `3a4cec3` (2026-04-07), with what the paths in the
  launcher script built in the 168 days since.
- **G2** For each path, say how it would enter narintel: consume its packages, migrate work into
  narintel, or upgrade the path's packages so narintel can be developed.
- **G3** Relationships between paths: semantic duplicates with recommended upgrades, and who
  consumes whom and why.
- **G4** Propose a new episode synopsis from a RISE reading of narintel's current state and intent.
- **G5** Segment the result so a Mia seat running `mia-episode-companion`, whose turn budget is two
  file reads, can read one segment by its code.

## [S2] Narintel as it stood on 2026-04-07

- Specification only, status Germination. Six core rispecs, seven app rispecs, seven
  `COORDINATION_*` records, `README.md` and `APPS.md` under `rispecs/`.
- Four layers. L1 analysis, marked "✅ 98%" for a Python path `langgraph/libs/narrative-intelligence`.
  L2 tracing, marked complete. L3 Flowise flywheel, "spec only". L3 Langflow router, "~70%". L4
  consumers, "Miadi-46, Webhooks".
- Vocabulary: the Three-Universe Model. 281 lines name "universe" in 23 files outside
  `rispecs/llms/`. 58 lines name K'é, Hózhó or Sacred Pause.
- Named code consumer: `/src/storytelling`. Its last commit is also 2026-04-07.
- `rispecs/llms/` is a vendored copy of llms-txt (RISE text v1.2), not a submodule.
- Published at docs.narintel.jgwill.com and indexed by context7 (`context7.json`).
- Intent, from `README` and `llms.txt`: turn narratives into structured intelligence, analyse
  character arcs and thematic tension, classify emotional beats, route creative work by narrative
  context, trace the creative process. Seven role apps: Architect, Structurist, Storyteller,
  Editor, Reader, Collaborator, Witness.

## [S3] Paths

### P1 `/a/src/Miadi` — 1,427 commits since 2026-04-07

Built, where it touches narrative:

- `@miadi/ncp-story-studio` 0.8.0 (jgwill/Miadi#361): canonical NCP types, a zero-dependency
  validator, a dialect reader `readNcp`, a story lattice (headless and React), a project store
  (JSON or Neon), the agent link protocol `[[Beat:id|label]]`, terminology as data, nine
  fixtures. Canonical schema: avadisabelle/holisticagnostic-narrative-context-protocol
  `schema/ncp-schema.json`. Consumption target `app/ncp`, with phone rounds 0.7.0 to 0.7.6.
- `@miadi/wampum-narrative-engine` 0.1.0 and `@miadi/ncp-wampum-bridge` 0.1.0 (jgwill/Miadi#439):
  a peer narrative model (position instead of order, several readings with none promoted, a
  renewable commitment log) and the only package that knows both models, returning a
  `CrossingReport`. `mayGenerateInto` refuses generation into the sacred register.
- Three perspectives (jgwill/Miadi#676, 2026-09-22): `@miadi/code` 0.1.5 reads each event from
  three perspectives, live-story-monitor routes and MCP tools take a perspective,
  `@miadi/hooks-core` 0.5.1 carries `domain_id`, `/docs/kids/three-perspectives` is live.
- Events: `@miadi/hooks-core`, `hooks-gateway`, `hooks-interpreter` hold the canonical event
  envelope. That is the "narrative event" narintel's diagram takes as input.
- Retired. 2026-09-18 (jgwill/Miadi#647): narrative-bridge, narrative-performance, narrative-beats,
  narrative-lattice and cross-attention pages and MCP tools, and the Upstash ceremony spiral. 62
  files, 13,981 lines deleted, "the narrative surfaces that never delivered". 2026-07-30: the
  Flowise proxy is off by default (`MIADI_FLOWISE_ENABLED`). William: "never really worked".
  2026-08-19: the coaia-narrative and ncp submodules were removed (jgwill/Miadi#250). 2026-09-20
  (jgwill/Miadi#655): NCP material and `MISSION_251231.md` archived. narintel's `.github` prompt
  cites that mission.
- `@miadi/rispecs-builder` 0.1.0 compiles `./rispecs` into deterministic Markdown under
  `.miadi/rispecs/`, as a library, CLI and MCP server.
- `@miadi/capture`, `episode-capture`, `transcription`: voice takes become validated transcriptions
  bound to episodes.

How it enters narintel: consume, do not migrate. narintel's NCP spec defers to the canonical
schema and `ncp-story-studio`. Layer 4 names hooks-core, live-story-monitor and `@miadi/code` as
the consumers. App specs drop what #647 retired. `rispecs-builder` compiles narintel's `rispecs/`
with its defaults. No Miadi package needs an upgrade for narintel, apart from the `@miadi/code`
duplicates in X2 and X3.

### P2 `/workspace/repos/jgwill/medicine-wheel` — 323 commits, suite 0.15.2

- `narrative-engine`: beat sequencing across four directions and four acts, cadence, an arc
  validator (direction coverage, ceremony presence, Wilson alignment, OCAP), timelines. Since
  2026-09-13 it and `narrative-cluster` read one direction-to-act table from `ontology-core`.
- 0.14.0 (2026-09-18): a ceremony knows its episode, circle and closing. A beat knows who spoke and
  who witnessed. A diary door. `@medicine-wheel/client` and `community-identity` (persons,
  circles, roles, audit).
- 0.15.0 `honcho`: every stored beat, ceremony and diary entry is projected on write into memory
  that reasons.
- `community-review`: Elder review circles, three rispec stubs (2026-09-08).
- jgwill/medicine-wheel#143: specs and the workspaces panel follow `ThreePerspectiveProcessor` and
  `perspective_types`.

How it enters narintel: consume. The Witness Circle app rests on `client`, `community-identity` and
`ceremonial-diary`, and witnessing is now a field of a beat. Beats written to the wheel reach
Honcho without narintel specifying memory. Upgrade medicine-wheel only if narintel needs a crossing
between a wheel beat and an NCP storybeat, and then as a separate bridge package (X6), through the
`medicine-wheel-upstream-delivery` loop. narintel's vendored `llms-medicine-wheel-packages.txt`
predates 0.15.2.

### P3 `/workspace/repos/avadisabelle/avalangstack` — created 2026-05-28, gathered 2026-09-14

Chains 0.2.1, graphs 0.3.0. This is where narintel's Layers 1 and 2 became code, in TypeScript,
not at the Python path narintel names.

- `ava-langgraph-narrative-intelligence` 0.3.0: `ThreePerspectiveProcessor` (1,244 lines),
  `NarrativeCoherenceEngine` (1,142, the subject of narintel's `COORDINATION_COHERENCE_ENGINE.md`),
  `EmotionalBeatClassifierNode` (ten tones), the `UnifiedNarrativeState` bridge (930), an NCP
  schema copy (312), `NarrativeRedisManager`, `structural_thinking_graph`, a consent-gated
  `episode_retrieval`.
- `ava-langchain-narrative-tracing` 0.2.1: `NarrativeTraceOrchestrator` (the mission in narintel's
  `.github` prompt), handler, formatter, `PolyphonicParser`, `EpisodeBundler`, adapters for
  storytelling hooks, Miadi correlation headers and relational intelligence.
- Not shipped as nodes: Character Arc Generator, Thematic Tension Analyzer, Narrative Traversal,
  NCP Loader. A loader and validator exist in `ncp-story-studio`.
- Each package has its own RISE spec under `docs/rispecs/{chains,graphs}`.
- avadisabelle/avalangstack#2: universes became perspectives, with deprecated aliases. The "k'é"
  word in `value_gate` stays as a plain guard word (ruling W1).

How it enters narintel: its package specs replace narintel's L1 and L2 specs for package behavior
(X8). narintel keeps the contract between layers. Upgrade avalangstack for narintel on two
points: its NCP copy (X1), and the four unbuilt nodes if narintel still wants them (Q1). Nothing
migrates into narintel.

### P4 `/workspace/repos/jgwill/miadi-orchestration-kit` — 84 commits

- `claude/mia-episode-companion` (2026-09-20 and 21): hear, draft, `developmental-editor` agent,
  revise, return. `phone-capture`. The seat writes turns and diary entries to the Episode 339
  talking circle with its own token.
- `skills/chronicle-episode` (one host-neutral skill, API first), the Miadi Pi Network,
  `packages/miadi` Debian packages (`miadi-config` 0.2.0 owns `MIADI_*`).
- `rispecs/miadi-storyweaver-orchestration-kit` and `claude/miadi-storyweaver-orchestration-kit`.
- The staging note `miadi-rispecs-260922-…` names the kit as the place work migrates to from
  jgwill/Miadi.

How it enters narintel: three role apps already run here as loops. Editor Anvil is the
developmental-editor turn. Collaborator Bridge ("How do I get the AI to understand what I
want?") is the phone take, transcription and Mia return. Witness Circle writes are the circle
turns. RISE Phase 1 can reverse-engineer those app specs from these working loops. Orchestration
of the roles lives in the kit. The role specifications live in narintel.

### P5 `/workspace/repos/miadisabelle/gmtermux` — 290 commits

- Episode rooms on the phone: mounts `@miadi/episode-ui`, the attention packages,
  `inquiry-weave` 0.11.1, `episode-vessel` 0.1.3. The capture core was abstracted from gmtermux
  into `@miadi/capture`.

How it enters narintel: little. It is a surface where the Reader and Storyteller roles already
have a room. Nothing to take into narintel.

### P6 `/workspace/repos/avadisabelle/avadisabelle` — 8 commits

- Profile README. Points at avalangstack as Ava's home for chains and graphs.

How it enters narintel: publication only. Update it when narintel's layer map changes, so Ava's
page and narintel say the same thing.

### P7 `/srv/miadi/episodes/miadi-chronicle` — git root `/srv/miadi/episodes`, 961 commits

- Episode 350, "A Perspective Is Not a Universe" (2026-09-22): ten repositories renamed, narintel
  not among them. Two survey rows wait on narintel: `cross-repo/workspace-root.md` row 19
  ("Change with Narintel") and `cross-repo/llms-txt-and-etc-claude-code.md` row 8
  (`llms-full.txt:183`, "when Narintel renames"). Paths are in jgwill/Miadi
  `foundations/universe-and-perspective-vocabulary/`.
- Episodes 339 and 349: the development companion circle, and "Miadi Conducts a Ceremony Its
  Circle Can Enter".
- Staging `miadi-rispecs-260922-…`: revise Miadi's rispecs into subfolders, event-driven
  architecture over the hooks packages, stateloom.

How it enters narintel: the chronicle is where the proposed episode is minted, and narintel's
rename is the open tail of Episode 350.

### P8 `/srv/miadi/episodes/miadi-studio/{aureon,jamai}`

- Musical studio work from 2026-08: MIDI, ABC, movement JSONL, EN and FR transcriptions,
  `composition.json`. aureon `ava001` to `ava003`, jamai `op001` to `op004`.

How it enters narintel: no code relation. It is candidate material for testing emotional beat
classification and the NCP and wampum crossing, only with William's consent. These are his
creative works, and `mayGenerateInto` exists for that boundary.

## [S4] Relationships

### Consumption: who consumes whom, and why

- **C1** gmtermux consumes `@miadi/episode-ui`, `episode-vessel`, `inquiry-weave` and
  `attention-core`, so the phone room renders episode files and attention without its own copy.
  Capture moved the other way, from gmtermux into `@miadi/capture`.
- **C2** Miadi consumes `@medicine-wheel/github-ceremony` and `client`. GitHub webhooks land on the
  wheel, so one ceremony store remains after the Upstash spiral was retired.
- **C3** The medicine-wheel store feeds `@medicine-wheel/honcho` on every write, so memory follows
  the records.
- **C4** `@miadi/ncp-wampum-bridge` takes `ncp-story-studio` and `wampum-narrative-engine` as peer
  dependencies. It is the only package that knows both, so loss between the models is reported
  in one place.
- **C5** avalangstack graphs consume its chains, enforced locally by `pnpm check:consumption`.
- **C6** `mia-episode-companion` consumes Miadi's identity and ceremony APIs on 3335 and the
  chronicle's captures by git. It writes to the circle so the wheel and Honcho remember.
- **C7** `@miadi/code` declares the ava-lang packages at `^0.1.1`, which excludes the current 0.2.x
  and 0.3.x lines, and only `src/pde/llm-intent-extractor.ts` mentions them. The consumption is
  nominal (X2, X3).
- **C8** narintel is consumed by readers only: docs.narintel.jgwill.com, context7, and agents
  reading `llms.txt`. Its named code consumer, `/src/storytelling`, has not moved since 2026-04-07.

### Semantic duplication, with a recommended upgrade

- **X1** NCP data model, four places: narintel `ncp-schema.rispec.md` (v1.1), avalangstack
  `graphs/narrative-intelligence/src/schemas/ncp.ts`, `@miadi/ncp-story-studio/schema`, and the
  canonical JSON schema in holisticagnostic-ncp. Upgrade: avalangstack imports
  `@miadi/ncp-story-studio/schema` (a zero-dependency subpath) or generates its types from the
  canonical JSON schema. narintel's NCP spec says what NCP enables in the stack and points at the
  package. (Q2)
- **X2** Three-perspective reading, three places: avalangstack `ThreePerspectiveProcessor`,
  `@miadi/code`'s own `types.ts` and `identity.ts`, and coaia-narrative `perspective_types`.
  Upgrade: `@miadi/code` consumes `ava-langgraph-narrative-intelligence` 0.3.0, which needs
  `@langchain/langgraph ^1.4.15` where it declares `^0.2.0`, or it drops the nominal ranges and
  states that its reader is its own. (Q4)
- **X3** Narrative tracing, two implementations and a third vocabulary:
  `ava-langchain-narrative-tracing` and `@miadi/code` `src/langchain/tracer.ts` both send
  `X-Narrative-Trace-Id`. No Miadi app route or hooks package reads that header. hooks-core has its
  own envelope. Upgrade: `@miadi/code` uses the tracing package's orchestrator, and one ruling
  decides whether correlation IDs travel as headers or as hooks-core envelope fields. (Q7)
- **X4** Consent, two places: avalangstack `episode_retrieval` defines its own `ConsentContext`
  (granted, pending, revoked). `@medicine-wheel/consent-lifecycle` holds living consent with
  renewal and withdrawal. Upgrade: `episode_retrieval` reads consent from the wheel's package, so
  a withdrawal on the wheel reaches retrieval.
- **X5** Fire Keeper and the Medicine Wheel filter, two places: avalangstack
  `chains/relational-intelligence` defines `FireKeeper` and `MedicineWheelFilter`.
  `@medicine-wheel/fire-keeper` and `ontology-core` hold the same concepts. avalangstack imports
  `@medicine-wheel` in one prompt-decomposition bridge only. Upgrade: name one as canonical. The
  chain consumes it, or its README says why it stays separate.
- **X6** Beats, three models: wheel beats (direction, act, speaker, witness), avalangstack
  `StoryBeat` in `UnifiedNarrativeState`, and NCP storybeats. Do not merge them.
  jgwill/Miadi#439 set the design: peer models, and a crossing that reports its loss. narintel
  names the crossings and where loss is reported. Build a beat-to-storybeat crossing package only
  when a consumer needs one.
- **X7** Coherence and arc validation, on different axes: `NarrativeCoherenceEngine` checks
  structure, theme, character, sensory detail and continuity. medicine-wheel `validateArc` checks
  direction coverage, ceremony presence, Wilson alignment and OCAP. These are not duplicates. They
  are the story_engine and ceremony perspectives' checks over one beat set. narintel's stack spec
  states that relation, and neither package absorbs the other.
- **X8** Two specifications of the same packages: narintel's L1 and L2 rispecs and avalangstack
  `docs/rispecs`. Upgrade: the package spec is the source for package behavior. narintel owns the
  contracts between layers and the role apps.
- **X9** Guidance: narintel `rispecs/llms/` (April copy, RISE text v1.2) and the live distribution
  (`/etc/claude-code`, llms.jgwill.com, RISE text v1.2.1). Upgrade: replace the copy with links.

Outside narintel's scope, named as a relation only: prompt decomposition exists in avalangstack
(chain and engine), `@medicine-wheel/prompt-decomposition`, mcp-pde and miaco.

## [S5] Contrast

| code | narintel on 2026-04-07 | what exists on 2026-09-22 | where |
|---|---|---|---|
| F1 | Three-Universe Model | three perspectives, `perspective_types`, `lead_perspective`, no bare `perspective` key in shared records (N1) | jgwill/Miadi#676, Episode 350 |
| F2 | Ava8's Ceremony World with K'é and Sacred Pause | a ceremony perspective. K'é and Hózhó are out of generated code and technical docs | Episode 350 sacred-names ruling |
| F3 | L1 in Python LangGraph, "98%" | TypeScript `ava-langgraph-narrative-intelligence` 0.3.0, four named nodes unbuilt | avalangstack |
| F4 | L2 tracing complete | `ava-langchain-narrative-tracing` 0.2.1 | avalangstack |
| F5 | L3 Flowise flywheel, spec only | Flowise proxy off by default, "never really worked" | Miadi, 2026-07-30 |
| F6 | L3 Langflow router, "~70%" | no Langflow commit in the surveyed paths. Routing exists as `ava-langchain-inquiry-routing` and `ava-langgraph-inquiry-routing-engine` | avalangstack |
| F7 | L4 consumers "Miadi-46, Webhooks" | hooks-core envelope, live-story-monitor, `@miadi/code` | Miadi |
| F8 | NCP v1.1 schema spec | canonical JSON schema, `ncp-story-studio` 0.8.0, a peer wampum engine and its bridge | Miadi, holisticagnostic-ncp |
| F9 | narrative beats | wheel beats with speaker and witness, projected to Honcho | medicine-wheel 0.14 and 0.15 |
| F10 | Witness Circle app | ceremony circles, `community-identity`, diary, the Episode 339 talking circle | medicine-wheel, Miadi, kit |
| F11 | Editor Anvil and Collaborator Bridge apps | the developmental-editor turn and phone takes | kit |
| F12 | narrative lattice, beats and performance surfaces in Miadi | retired | jgwill/Miadi#647 |
| F13 | Storytelling as the primary consumer | no commit since 2026-04-07 | `/src/storytelling` |
| F14 | vendored `rispecs/llms/` | stale copy (X9) | narintel |

**Pattern.** narintel specified the stack in December 2025. The code landed from May to September
2026 in other repositories, each with its own specs. One behavior with two sources of truth moves
back and forth between them, which is an oscillating pattern. The advancing structure: each
package owns its behavior spec and changes it with its release. narintel owns what crosses
packages and the role apps, so it changes only when a crossing changes.

- **R1** Agents and context7 read narintel as current: the Python path, "98%", the Three-Universe
  vocabulary, K'é in routing. Every agent that loads docs.narintel.jgwill.com learns the model
  Episode 350 retired.
- **R2** Renaming narintel's text before the stack map exists repeats #676's work on prose that
  the rewrite replaces. Map first (A2), rename during the rewrite (A4).

## [S6] Proposed episode

Title and number are William's. 350 is the latest episode on 2026-09-22.

- **O1** "Narintel Specifies What Was Built" (recommended: it states the finding plainly)
- **O2** "The Stack Was Built Elsewhere"
- **O3** "The Roles Already Have Rooms"

**Goal**, in `episode.yaml` form: "Narintel specifies the narrative intelligence stack that
exists: each layer names the package and version that ship it, the three readings of an event
are perspectives, and the seven role apps are specified from the surfaces where those roles
already work."

**Current reality.** narintel is a specification repository in Germination, unchanged for 168
days. Its Layers 1 and 2 shipped as TypeScript packages in avalangstack with their own specs. Its
NCP foundation shipped as `@miadi/ncp-story-studio` beside a peer wampum engine. Its Layer 3 was
switched off in Miadi. Its Witness, Editor and Collaborator roles run as loops in the
medicine-wheel, Miadi and the orchestration kit. Its vocabulary is the one Episode 350 retired, and
agents still read it.

**Desired outcome.** A narintel whose `rispecs/README.md` is the stack map (layer, package,
version, spec link), whose own specs hold only the crossings between packages and the seven role
apps, whose apps are reverse-engineered from the working loops, whose text names three
perspectives, and whose compiled context (`rispecs-builder`) and `llms.txt` let an agent build
against the stack as it is.

**Script outline**

| file | title | draws on |
|---|---|---|
| `script.md` | spine: specified in December, built from May, by other hands | S2, S5 pattern |
| `chapter-01-script.md` | Specified in Python, built in TypeScript | P3, X8, F3, F4 |
| `chapter-02-script.md` | Four copies of NCP and a belt beside them | P1, X1, X6, jgwill/Miadi#439 |
| `chapter-03-script.md` | The surfaces that never delivered | F5, F6, F12, jgwill/Miadi#647 |
| `chapter-04-script.md` | The roles already have rooms | P2, P4, F10, F11, Episodes 339 and 349 |
| `chapter-05-script.md` | The last rows of Episode 350 | F1, F2, R1, P7 |
| `chapter-06-script.md` | What narintel keeps | X2 to X7, the crossing contracts, S6 desired outcome |

**Action steps, in RISE order**

- **A1** (Reverse engineering) Run RISE Phase 4 per narintel spec, against the git log since
  2026-04-07 of the repository that now implements it: avalangstack `docs/rispecs` and graphs,
  `@miadi/ncp-story-studio`, medicine-wheel `narrative-engine`, `honcho`, `client`, and the kit's
  companion loop.
- **A2** (Reverse engineering) Mark each narintel spec as one of: superseded (points to the package
  spec), live (a crossing contract or a role app), retired (Flowise flywheel, the #647 surfaces).
- **A3** (Intent) Extract each role app's intent from the surface where it already works: Witness
  from the circle, Editor from the developmental-editor turn, Collaborator from phone takes,
  Structurist and Reader from `app/ncp`, Architect from `ncp-story-studio`'s schema.
- **A4** (Specifications) Rename during the rewrite, per Episode 350: perspectives, N1, K'é and
  Hózhó out of generated routing, dated records kept.
- **A5** (Specifications) Rewrite `rispecs/README.md` as the stack map, and `llms.txt` with it.
- **A6** (Specifications) Settle X1 to X5 with William's rulings, each in the repository that owns
  the code, with an issue there first.
- **A7** (Exportation) Replace `rispecs/llms/` with links (X9). Compile `rispecs/` with
  `@miadi/rispecs-builder`. Regenerate `llms-full.txt`.
- **A8** (Exportation) Close Episode 350's two narintel rows (`workspace-root.md` row 19,
  `llms-full.txt:183`) and update the avadisabelle profile (P6).

**Attention items**

| code | question |
|---|---|
| Q1 | Do the Character Arc Generator, Thematic Tension Analyzer, Narrative Traversal and NCP Loader nodes get built (in avalangstack graphs, or in `ncp-story-studio`), or leave the spec? |
| Q2 | Which NCP is canonical for the stack: the holisticagnostic JSON schema served through `@miadi/ncp-story-studio`? Does avalangstack drop its copy? |
| Q3 | Layer 3: retire the Flowise and Langflow specs, or respecify routing on `ava-langgraph-inquiry-routing-engine`? |
| Q4 | `@miadi/code`: consume avalangstack (a LangGraph 0.2 to 1.4 upgrade) or own its reader and drop the nominal ranges? |
| Q5 | Does narintel stay specification-only, with `app/ncp` in Miadi as the place the role apps are built? |
| Q6 | Title (O1 to O3) and number. |
| Q7 | Correlation IDs: `X-Narrative-*` headers, hooks-core envelope fields, or both? |

**Lineage**

- relates_to Episode 350 (`2026-09-22-episode-350-a-perspective-is-not-a-universe`): narintel
  holds two of its open rows, and its rename is this episode's chapter 5.
- relates_to Episode 339 (`2026-08-25-episode-339-relation-to-mia-on-mobile-devops`): its
  companion loop and circle are where the Editor, Collaborator and Witness roles already work.
- relates_to Episode 349 (`2026-09-17-episode-349-miadi-conducts-a-ceremony-its-circle-can-enter`):
  a circle that can enter a ceremony is the Witness Circle app's ground.

**References:** jgwill/Miadi#676, jgwill/Miadi#361, jgwill/Miadi#439, jgwill/Miadi#647,
jgwill/Miadi#655, avadisabelle/avalangstack#2, jgwill/medicine-wheel#143,
avadisabelle/coaia-narrative#56.

**Vessel.** Not minted. After William names the title and number, minting goes through the
`chronicle-episode` skill, from a staging folder's `mint-request.json`, as Episode 350 was.
