# Steal Ideas — Extracted from 5 Evaluated Sources

**Created:** July 13, 2026  
**Purpose:** Every concrete idea, technique, value, command, and rule worth taking from the 5 sources I evaluated. Hand this file to the agent when you need to reference or implement any of these.

---

## 1. Two-Stage Frame Sampling for Video Analysis

**Stolen from:** Source 1 — conradcaffier03 gist ("Give Claude Eyes")

The idea: sample the hook densely (it carries the most motion and decides retention), sample the body sparsely.

### The FFmpeg Commands

```bash
# HOOK: first 15 seconds at 15fps → tiled contact sheets (5 cols × 9 rows = 45 frames per sheet)
mkdir -p hook && ffmpeg -y -t 15 -i video.mp4 \
  -vf "fps=15,scale=200:-1,tile=5x9:margin=6:padding=4:color=white" -an hook/sheet_%02d.jpg

# BODY: 1 frame every 3.5 seconds across the whole video
mkdir -p body && ffmpeg -y -i video.mp4 -vf "fps=1/3.5,scale=360:-1" body/f_%02d.jpg

# AUDIO: extract for transcription
ffmpeg -y -i video.mp4 -ar 16000 -ac 1 audio.wav
```

### Why These Specific Values

| Parameter | Value | Why |
|-----------|-------|-----|
| Hook duration | 15 seconds | The hook decides viewer retention — most motion and cuts happen here |
| Hook FPS | 15 fps | Dense enough to catch fast cuts, text reveals, count-up animations |
| Hook tile layout | 5x9 | 45 frames per contact sheet = 3 seconds of video per sheet. Reduces total image count for context window |
| Hook scale | 200px wide | Small enough to fit many on a sheet, large enough to read on-screen text |
| Body FPS | 1 frame / 3.5s | Catches end-states of scenes without flooding context. Misses transitions (acceptable tradeoff) |
| Body scale | 360px wide | Larger than hook because each frame carries a full scene worth of info |
| Audio sample rate | 16000 Hz, mono | Whisper's expected input format |

### Frame Index Math
- Sheet k, cell i → frame number: `(k-1)*45 + i`
- Frame N in hook → timestamp: `t = N / 15` seconds
- Frame N in body → timestamp: `t = N * 3.5` seconds

### Limitations to Know
- A 60-minute video at 1 frame/3.5s = ~1,000 body frames → will blow past context limits
- Whisper mishears names ("Claude" → "plot") — always cross-check transcript against frames
- yt-dlp fails on some platforms (age-gated content, private videos, some Instagram posts)
- This gives the AI a flipbook of JPEGs, NOT video understanding — it can't track motion, transitions, or audio tone

### How to Use This in Your Pipeline
Adapt into an Antigravity IDE skill that:
1. Takes a YouTube/Instagram URL
2. Downloads with yt-dlp
3. Runs the two-stage FFmpeg extraction
4. Transcribes with Whisper (or feeds to ElevenLabs for comparison)
5. Feeds frames + transcript to the agent for competitor analysis, hook study, or QA of your own renders

---

## 2. Production Rules — Editorial Quality System

**Stolen from:** Source 3 — Bomx/super-video-maker-skill (SKILL.md, 51 operating rules)

These are hard-won production SOPs. Each rule exists because someone made the mistake it prevents.

### B-Roll Routing Table (Rule 22)

Choose b-roll by what the narration is DOING, not what's "cool to generate":

| Beat Purpose | First Choice | Second Choice | Last Resort |
|-------------|-------------|---------------|-------------|
| **News beat** ("here's what changed") | Real screenshot of the announcement (blog, product page) + Ken Burns | Editorial photo | Generated — only if no real visual exists |
| **Source proof** | Agent-operated browser footage or real screenshot of proof page | — | NEVER replace with generated b-roll |
| **Story/example** ("a founder doing X") | Real stock footage of a real person (Pexels/Pixabay) | Editorial photo + Ken Burns | Generated as last resort |
| **Concept/metaphor** | Typographic pull-quote card or single real object photo | — | NOT an abstract symbolic render |
| **Aggregate/momentum** ("everyone is talking") | Screenshot of Techmeme/Trends/HN + Ken Burns | Photo of newspaper headlines on a desk | NOT a "data constellation" |
| **Action step** | Real UI screenshot with drawn arrow/highlight | Real hand performing the step | NOT glowing icons in space |

### Layout Zone System (Rule 24)

Plan layout zones BEFORE composing — overlay collision is the #1 visual bug.

Default zone map for 1920x1080 with bottom-centered captions:

```
+------------------------------------------+
| [Disclosure badge]         [Avatar PiP]  |
|  50,50                      1378,50      |
|  (hook only, fades ~4.5s)   492x276      |
|                                          |
|              [CENTER]                    |
|     b-roll / browser proof / avatar      |
|                                          |
|                                          |
|          ---------------------           |
|          [BOTTOM BAND ~140px]            |
|          karaoke captions ONLY           |
+------------------------------------------+

OUTRO: disclosure footer bottom-center, action steps middle, PiP hidden
```

**Rule: If two elements share a zone, stagger their enable= time windows or redesign one.**

### Cut Cadence Rules

| Content Type | Max Hold Time | Why |
|-------------|---------------|-----|
| AI-generated static images | 2-4 seconds | Holding >3.5s advertises it's AI-generated |
| Real screenshots | 3-6 seconds | Real content earns more screen time |
| Long beats (>5s) | MUST split into 2-3 cuts | Different photos, different crops, or alternating textures |

### Visual Job Labels (Rule 32)

Every shot gets exactly ONE label:

| Job | What It Proves |
|-----|---------------|
| **Proof** | "This is real" |
| **Mechanism** | "This is how it works" |
| **Consequence** | "This is why it matters" |
| **Action** | "This is what to do" |
| **Transition** | "We are moving to the next idea" |

**If a shot has no job, it is filler — cut it.**
**If two consecutive shots have the same job + same source, the second must prove a different detail or be replaced.**

### Source Repetition Budget (Rule 33)

Per source website:
- **Max 1** establishing shot (hero/headline)
- **Max 2** additional crops (paragraph proof, feature section)
- Each appearance MUST answer a different question
- The same website as generic wallpaper = banned

### Beat-Locking Rule (Rule 14)

Always Whisper-transcribe the audio first (word-level timestamps), then pin EVERY visual change to the actual seconds the words appear. Never overlay visuals against assumed timing.

### Script Structure Template

```
Hook (5-6s)         -> Why the viewer should care, one breath
Disclosure (1 line) -> "Quick note, this is the digital avatar of <name>"
News beat           -> What changed
Story/example       -> Concrete situation making the change feel real
Source proof        -> Browser footage or screenshot showing the source
Action step         -> What the viewer should do next (3 numbered moves)
Spoken CTA (6-8s)   -> Avatar speaks follow CTA over outro recap card
```

**Never end with a silent card. Always have a spoken CTA tail.**

---

## 3. Remotion Animation Values

**Stolen from:** Source 5 — sabrina.dev ("5 Insane Claude Code Video Prompts")

Cross-check these against your remotion-craft-skill defaults. Test both, keep whichever renders better.

### Safe Zones (1080x1920 mobile)

| Zone | Value |
|------|-------|
| Top margin | 150px |
| Bottom margin | 170px |
| Side margins | 60px each |

### Typography Minimums

| Element | Minimum Size |
|---------|-------------|
| Headlines | 56px |
| Body text | 36px |
| Absolute minimum (anything) | 28px |

### Animation Defaults

| Parameter | Value | Use |
|-----------|-------|-----|
| Spring damping | spring({ damping: 200 }) | Standard entrance/exit |
| Stagger between elements | 8-12 frames | Sequential reveals |
| Transition fades | 12 frames via TransitionSeries | Between scenes |
| SVG drawing | stroke-dashoffset animation | Line drawing effects |

### Scene Structure Templates

**Product Demo (5 scenes):**
Hook -> Demo -> Proof -> CTA

**Explainer (5 scenes):**
Hook -> Problem -> Mechanism -> Evidence -> CTA

**Each prompt uses "STEP 1 - RESEARCH, STEP 2 - BUILD" with approval checkpoints between steps.**

---

## 4. Voiceover Humanization Rules

**Stolen from:** Source 3 — Bomx/super-video-maker-skill (SPOKEN_VO_HUMANIZER.md)

12 rules for making AI voiceover scripts sound like a human talking, not a spec sheet read aloud.

### The Core Rules

1. **One connected thought, not bullets.** Every line attaches to the previous with a spoken connector — "so," "and," "but," "then there's," "'cause." Max ONE standalone punch line per script.

2. **Vary rhythm hard.** At least one sentence over 15 words and one under 6. Never three consecutive lines within ~5 words of each other in length.

3. **Contractions everywhere.** it's / didn't / that's / 'cause / wanna. Use "is / has / shows," never "serves as / boasts / offers / features / provides."

4. **Benefit-first intros.** Pattern: "first one's X, and it's basically [what it does FOR YOU]." Never a category label.

5. **"You" owns the benefit.** Every benefit answers "what does this do for you," not "what is this tool."

6. **Spoken list intros.** "first one's...," "then there's...," "and the last one — this one surprised me." Never "Number one:".

7. **2-3 discourse markers total, mid-flow only.** okay / so / honestly / look. Zero = robot. Six = a tic. Never as a manufactured opener.

8. **One emotion drives the whole script.** Pick a single stance and let word choice carry it.

9. **Concrete beats abstract.** "See which pages Google is ignoring," not "indexing data." Write numbers as spoken: "a hundred forty bucks a month," not "$140/mo."

10. **Max one "Question? Answer." beat per script. Zero colons.** Nobody speaks a colon.

11. **Word budget = read-aloud time.** ~150 wpm -> 25s = 60-65 words; 30s = 75-85 words. If benefits don't fit for 3 items, cover 2 items — don't compress into fragments.

12. **End by folding the CTA into the final thought.** One breath — payoff + next action. Never appended fragments.

### Banned Spoken-AI Tells

- Parallel fragment chains (every line the same clipped shape)
- Colon constructions ("Tool: description")
- "Question? Answer." more than once per script
- List-reading cadence ("Number one... Number two...")
- Zero-connector islands (consecutive sentences with no tissue between them)
- Appended telegraphic CTA ("That's in the article. Bio.")
- "Not just X, but Y" / negative parallelism
- Forced rule-of-three ("fast, simple, and free")
- Synonym cycling ("the tool" then "the platform" then "the solution")
- Significance inflation tails ("..., highlighting its value")
- Formal connectors (furthermore, moreover, additionally)
- Banned vocabulary: delve, leverage, utilize, unlock, game-changer, cutting-edge, seamless, robust, elevate, supercharge, powerful, dive in, buckle up, "in today's digital landscape"
- Fake-candor openers ("Honestly?" / "Real talk" / "Here's the thing." as line one)
- Hedging/RLHF balance ("generally," "in many cases")

---

## 5. Anti-AI-Slop Visual Rules

**Stolen from:** Source 3 — Bomx/super-video-maker-skill (SKILL.md Rules 27-28, 30-31)

### Banned AI-Slop Aesthetics (Rule 27)

When generating b-roll, the prompt MUST NOT contain:

- "dark cosmic / cyberspace / neon grid / glowing particles / data streams / neural network"
- "floating" subjects (laptops, icons, devices in a void with no grounding plane)
- Logo glyphs or brand marks of any kind (Android robot, Chrome ball, app icons, company logos)
- "magic / ethereal / ethereal blue / volumetric light rays" cyber-fantasy vocabulary
- Orange/teal "Hollywood look" gradient as the entire palette
- Symbolic visualization of abstract concepts ("data constellation," "merge of two operating systems," "AI brain")

### What to Use Instead

Force prompts into **documentary-realism** territory:

| Instead of | Use |
|-----------|-----|
| Abstract AI brain visualization | A real human in a real environment doing a real action |
| Glowing neon grids | Natural light from a believable source |
| Floating devices in void | 35mm or 50mm photographic feel, shallow depth of field |
| Cyber-fantasy colors | Editorial color grade matched to mood (warm domestic, cool corporate, neutral documentary) |

**Vocabulary that produces better results:**
- "documentary photography"
- "editorial portrait"
- "natural window light"
- "shot on Sony FX3" (or similar real camera)
- "shallow depth of field"
- "real environment"
- "candid moment"

### Visual Variety Rule (Rule 28)

Pick at least **three distinct visual textures** across a 60-90s video:
1. Editorial-photo Ken Burns
2. Stock-footage handheld clip
3. Typographic pull-quote card

Avoid two consecutive clips sharing the same dominant color or composition. "One unified visual language" applies to brand cards/badges/captions, NOT to b-roll content.

### Scale-to-Fill Rule (Rule 30)

```bash
# CORRECT: fit-to-fill + center-crop (no black bars)
-vf "scale=W*2:H*2:force_original_aspect_ratio=increase,crop=W*2:H*2"

# WRONG: pad-with-color (looks amateur on documentary photos)
-vf "pad=W:H:...:color=#0F1320"
```

Padding bars are reserved for a deliberate cinematic letterbox look ONLY — never as a default.

---

## 6. Pipeline Architecture Patterns

**Stolen from:** Source 4 — OpenMontage (GitHub repo)

### Pipeline Manifest Structure

```
research -> proposal -> script -> scene_plan -> assets -> edit -> compose -> deliver
```

Each stage has: input requirements, output contract, quality gates, failure modes.

### Scored Provider Selection (7 dimensions)

When choosing between providers for the same task (TTS, image gen, video gen), score on:

1. Output quality
2. Cost per unit
3. Speed / latency
4. Consistency across generations
5. API reliability / uptime
6. Platform compatibility
7. Fine-tuning / customization options

### Pre-Compose Validation Gate

Before composing the final video, check:
- All planned assets exist and passed QC
- Audio and video durations match within tolerance
- No overlay collisions in the layout zone map
- All captions synced to word-level timestamps
- Codec compatibility for target platform

### Reference-Video-Driven Workflow

1. Download and analyze the reference video (frames + transcript)
2. Extract: scene structure, cut cadence, hook technique, visual style, pacing
3. Generate a production plan that replicates the STRUCTURE with different CONTENT
4. Never copy frames or footage — convert each source scene into owned shot intent

---

## 7. Hyperrealistic Image Generation Framework (12-Part)

**Stolen from:** Source 3 — Bomx/super-video-maker-skill (HYPERREALISTIC_IMAGE_SOP.md)

When generating AI images that must NOT look AI-generated, build every prompt from these 12 sections in order:

| # | Section | What to Specify |
|---|---------|----------------|
| 01 | **Subject** | Age range in years, ethnicity, skin tone (base + undertone), build |
| 02 | **Skin** | WHERE pores are visible (nose tip, cheeks, T-zone), specific imperfections (mole, acne mark, redness), surface quality (oily shine, peach fuzz), asymmetry |
| 03 | **Eyes/Brows/Nose/Mouth** | Exact iris color + limbal ring, catchlight position (clock position), sclera redness, brow stray hairs, lip texture, tooth color (never "perfect white") |
| 04 | **Hair** | Multi-tonal color (lighter front, darker mid-lengths), flyaways at crown, frizz, compression marks from hair ties, curl type (3a/3b/3c/4a/4b) |
| 05 | **Clothing** | Fabric type + weave ("French terry fleece with visible looped texture"), behavior on body ("stretch lines across chest"), wear level (pilling, fading) |
| 06 | **Pose** | Weight distribution, hip shift, spine curve, specific finger position, head tilt in degrees |
| 07 | **Environment** | Real room with specific objects, depth layers (foreground clutter, middle ground subject, background wall/window), imperfect details |
| 08 | **Camera/Lens** | Focal length (35mm, 50mm, 85mm), aperture (f/1.4, f/2.8), DOF behavior, sensor noise at ISO, lens characteristics |
| 09 | **Lighting** | Key light position + color temp, fill ratio, rim/hair light, how light falls on skin (specular highlights on nose bridge, forehead, cheekbone) |
| 10 | **Mood** | One emotional word driving the image, NOT a vibe board |
| 11 | **Anti-AI Notes** | Explicit instructions to PREVENT AI tells: "natural skin asymmetry," "not perfectly symmetrical face," "slight lens distortion at edges" |
| 12 | **Negative Prompt** | What to NOT generate. Since gpt-image-2 has no negative-prompt field, append as "avoid / do NOT render" clauses in the positive prompt |

### The Critical Anti-AI Items (Sections 11-12)

**Must include:**
- Natural facial asymmetry (one eye slightly larger, one brow higher)
- Visible pores, especially on nose tip and cheeks
- Imperfect teeth (natural off-white, slight spacing)
- Hair flyaways and frizz
- Fabric wrinkles and compression marks
- Skin imperfections (mole, redness, under-eye shadow)

**Must explicitly ban:**
- Smooth poreless skin
- Perfectly symmetrical face
- Plastic-looking hair (uniform color, no flyaways)
- Blurred jewelry
- CGI-looking fabric
- Perfect studio lighting with no shadows
- Beauty-filter smoothing

---

## 8. FFmpeg Recipe Book

**Stolen from:** Source 3 — Bomx/super-video-maker-skill (FFMPEG_PLAYBOOK.md)

### Audio Mixing (voice + music)

```bash
ffmpeg -y \
  -i video_no_audio.mp4 \
  -i voiceover.mp3 \
  -i music.mp3 \
  -filter_complex "[2:a]volume=0.12,apad[music];[1:a][music]amix=inputs=2:duration=first:dropout_transition=2[a]" \
  -map 0:v -map "[a]" \
  -c:v copy -c:a aac -b:a 192k \
  video_with_audio.mp4
```

Key: music at volume=0.12 (12%) sits under voice without competing.

### Loudness Normalization

```bash
ffmpeg -y -i input.mp4 \
  -af "loudnorm=I=-16:TP=-1.5:LRA=11" \
  -c:v copy -c:a aac -b:a 192k \
  normalized_audio.mp4
```

- -16 LUFS for web/social
- -14 LUFS for music-forward content

### HeyGen Green Screen Removal

```bash
ffmpeg -y -i heygen_green.mp4 \
  -vf "chromakey=0x00ff00:0.18:0.08,format=yuva420p" \
  -c:v qtrle avatar_alpha.mov
```

### Avatar PiP — Borderless Rounded Corners + Drop Shadow

```bash
ffmpeg -y \
  -i background.mp4 \
  -i avatar_green.mp4 \
  -i assets/pip_mask.png \
  -i assets/pip_shadow.png \
  -filter_complex "\
[1:v]chromakey=0x00ff00:0.18:0.08,scale=492:276,format=rgba[av];\
[2:v]format=rgba[mask];\
[av][mask]alphamerge[avr];\
[3:v]format=rgba[sh];\
[0:v][sh]overlay=x=1378-32+4:y=50-32+16:enable='between(t,15.8,77.8)'[bg2];\
[bg2][avr]overlay=x=1378:y=50:enable='between(t,15.8,77.8)':format=auto[v]" \
  -map "[v]" -map 0:a? \
  -c:v libx264 -preset medium -crf 18 -pix_fmt yuv420p \
  -c:a copy with_pip.mp4
```

Default PiP: 492x276 on 1920x1080, top-right at x=1378, y=50. 24px rounded corners via alpha mask. Shadow offset +4/+16.

### Karaoke Captions (ASS Style)

```
Style: Default,Arial Black,64,&H00FFFFFF,&H000000FF,&H00000000,&H80000000,-1,0,0,0,100,100,1,0,1,5,2,2,80,80,90,1
Style: Active,Arial Black,64,&H0000FFFF,&H000000FF,&H00000000,&H80000000,-1,0,0,0,100,100,1,0,1,5,2,2,80,80,90,1
```

- Alignment=2 (bottom-center)
- MarginL=MarginR=80, MarginV=90
- Font: Arial Black 64px, Bold
- Active word: Yellow (&H0000FFFF)
- Outline=5, Shadow=2 (readable on any background)

### 16:9 to 9:16 Conversion

```bash
# Center-crop (loses edges)
ffmpeg -y -i master_16x9.mp4 \
  -vf "scale=1080:1920:force_original_aspect_ratio=increase,crop=1080:1920" \
  -c:v libx264 -preset medium -crf 18 -c:a aac -b:a 192k \
  vertical_9x16.mp4

# Letterbox (black bars, keep everything)
ffmpeg -y -i master_16x9.mp4 \
  -vf "scale=1080:-1,pad=1080:1920:(ow-iw)/2:(oh-ih)/2:black" \
  -c:v libx264 -preset medium -crf 18 -c:a aac -b:a 192k \
  vertical_letterbox.mp4
```

### Headline Montage (4-6 clips, 0.4-0.7s each)

```bash
ffmpeg -y -loop 1 -t 0.55 -i verge_headline.png \
  -vf "scale=1920:1080:force_original_aspect_ratio=increase,crop=1920:1080,format=yuv420p" \
  -c:v libx264 -preset medium -crf 18 verge_headline.mp4
```

### Source Receipt Card Overlay

```bash
ffmpeg -y -i proof_clip.mp4 -i receipt_card.png \
  -filter_complex "[0:v][1:v]overlay=48:48:enable='between(t,0,3.2)'[v]" \
  -map "[v]" -map 0:a? \
  -c:v libx264 -preset medium -crf 18 -pix_fmt yuv420p \
  -c:a copy proof_with_receipt.mp4
```

### Final Export Defaults

- Video codec: libx264
- Pixel format: yuv420p
- Audio codec: aac
- Audio bitrate: 192k
- FPS: 30
- CRF: 18 (high quality), 20-23 (smaller files)

---

## Quick Reference: What Came From Where

| Idea | Source | Original File |
|------|--------|--------------|
| Two-stage frame sampling | Source 1 | give-claude-eyes.md |
| Contact sheet tile trick | Source 1 | give-claude-eyes.md |
| SQLite+FTS5 memory pattern | Source 2 | claude-mem README (concept only) |
| 3-layer search pattern | Source 2 | claude-mem README (concept only) |
| B-roll routing table | Source 3 | SKILL.md, Rule 22 |
| Layout zone system | Source 3 | SKILL.md, Rule 24 |
| Anti-AI-slop ban list | Source 3 | SKILL.md, Rules 27-28 |
| Visual job labels | Source 3 | SKILL.md, Rule 32 |
| Source repetition budget | Source 3 | SKILL.md, Rule 33 |
| Beat-locking to Whisper | Source 3 | SKILL.md, Rule 14 |
| Cut cadence rules | Source 3 | SKILL.md, Rule 31 |
| VO humanizer (12 rules) | Source 3 | SPOKEN_VO_HUMANIZER.md |
| Hyperrealistic image SOP | Source 3 | HYPERREALISTIC_IMAGE_SOP.md |
| FFmpeg recipe book | Source 3 | FFMPEG_PLAYBOOK.md |
| Karaoke ASS caption style | Source 3 | FFMPEG_PLAYBOOK.md |
| Avatar PiP with rounded corners | Source 3 | FFMPEG_PLAYBOOK.md |
| Pipeline manifest structure | Source 4 | OpenMontage repo |
| Scored provider selection | Source 4 | OpenMontage repo |
| Pre-compose validation gates | Source 4 | OpenMontage repo |
| Reference-video workflow | Source 4 | OpenMontage repo |
| Remotion spring damping (200) | Source 5 | sabrina.dev blog |
| Safe zones (150/170/60px) | Source 5 | sabrina.dev blog |
| Font minimums (56/36/28px) | Source 5 | sabrina.dev blog |
| Stagger timing (8-12 frames) | Source 5 | sabrina.dev blog |
| Transition fades (12 frames) | Source 5 | sabrina.dev blog |
| Scene templates (Hook-Demo-Proof-CTA) | Source 5 | sabrina.dev blog |
