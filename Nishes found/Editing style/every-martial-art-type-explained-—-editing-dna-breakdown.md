# Editing-DNA Breakdown
## Every Martial Art Type Explained in 12 Minutes

**Video:** https://youtu.be/DIPL-IHldog
**Channel:** The Paint Explainer
**Published:** 2024-07-05
**Duration:** 12:44
**Performance:** ~5,008,819 views · 112,153 likes · 5,466 comments

> Breakdown rebuilt from full visual frame-by-frame analysis + the complete 2,257-word spoken transcript. Mapped to timestamps and translated into Remotion-implementable notes.

---

## 1. Cut Rhythm & Pacing

**What it is:** Fast, mechanical, narration-driven rhythm. Cuts land roughly every 5–10 seconds, each new fact or technique triggering a visual change so the frame never sits static. Segments are uniform — every martial art gets its own ~28–32 second block before the subject changes.

**Where it shows:** Karate's opening (0:00–0:10) cuts quickly across "origins," "striking techniques," and "philosophy." A technique trigger fires at 0:11 (punches/kicks stick figure).

**How to build it in Remotion:**
- Drive cuts from a scripted timeline array of `{ start, duration }` scene objects instead of hardcoded sequences.
- Use `<Series>` from `@remotion/series`, giving each scene a 5–10s duration that mirrors the narration length.
- Match cut frequency to the voice-over: split audio at sentence boundaries, measure segment length, and clamp scene duration to that window.

---

## 2. Text & Typography

**What it is:** Sans-serif, black text centered at the top of the frame, naming the current subject ("Karate," "Taekwondo," etc.). Supporting sub-labels surface key facts — and these are highlighted in red for emphasis (e.g., 0:02 "Ryukyu Kingdom"). Text is static: no entry/exit animation, no keying, no underline or highlight effects.

**Where it shows:** Subject labels at the start of each section; the red-highlighted sub-line at 0:02–0:04.

**How to build it in Remotion:**
- Reusable `<SubjectLabel text="Karate" />`: a plain `<AbsoluteFill>` with `<div style={textStyle}>` where `textStyle = { fontFamily: 'sans-serif', fontWeight: 700, letterSpacing: '0.08em', position: 'absolute', top: '8%', width: '100%', textAlign: 'center' }`.
- No `spring()` or opacity animation — render it conditionally with `<Sequence from={sceneStart}>`.
- For the emphasis treatment, allow a `highlightWords` prop that renders the key phrase in red (`color: '#E53935'`) while the rest stays black.

---

## 3. Transitions Between Scenes

**What it is:** Hard cuts are the primary transition. No complex motion graphics, masking, or slide/fade between segments — the restraint keeps the focus on rapid information delivery.

**Where it shows:** Throughout; the cleanest hard cut reads between the archival-photo and stick-figure shots.

**How to build it in Remotion:**
- Prefer `<Series>` default hard cuts.
- Do not layer `slide()` or `fade()` — the signature is its simplicity.

---

## 4. Motion & Camera Movement

**What it is:** Subtle Ken Burns pans and slow zooms on otherwise static stock/historical imagery to keep it alive. No screen shake, no parallax, no depth-of-field drift.

**Where it shows:** Gentle push-ins on the real-life practitioner clips throughout (each framed in a colored box, e.g., 0:04, 0:48).

**How to build it in Remotion:**
- Use the `@remotion/kensburn` package, or hand-rolled `interpolate` on `scale`/`x`: `scale: interpolate(frame, [0, 90], [1, 1.08], { extrapolateRight: 'clamp' })` inside a `<Sequence>`.
- Pan: interpolate `translateX` from `0` to `-4%` over ~3s.
- Keep magnification ≤ ~8% so it reads as camera drift, not a zoom punch.

---

## 5. Color & Visual Treatment

**What it is:** Clean, high-contrast, minimalist palette. White/light background with black line art throughout. Color is used deliberately — each martial art gets its own colored circular icon (orange for Karate, green for Taekwondo, purple for Jiu-Jitsu) and that same color is reused in the box framing its stock clip.

**Where it shows:** The whiteboard stick figures everywhere; color-coded icons at each section; matching colored boxes around the practitioner clips (0:04, 0:48).

**How to build it in Remotion:**
- Base background `#FFFFFF` for animation scenes, `#F4F4F4` for photo scenes.
- Stick figures as `#000000` strokes (`stroke: '#000', strokeWidth: 4, fill: 'none'`).
- Define a per-art color map `Record<string, string>` so the icon, box border, and highlight all pull the same hex.
- Apply a single light `Noise()` overlay (film grain) via `@remotion/noise` at ~3% opacity to avoid a flat digital feel. No LUTs, no saturation boosts.

---

## 6. Overlays, Graphics & Visual Elements

**What it is:** A persistent **circular icon** that acts as chapter navigation and changes with each martial art. Simple icon "shorthand" explains abstract concepts — a brain for "philosophy," a warning triangle for Krav Maga's "no competitions."

**Where it shows:** Top-right circular indicator refreshes at each new art (0:00 → 12:38). Krav Maga's hybrid nature (4:33) is shown by combining multiple martial-arts icons into one.

**How to build it in Remotion:**
- A `<ChapterBadge />` component: `<div style={{ position:'absolute', top:'6%', right:'4%', width:44, height:44, borderRadius:'50%', border:'2px solid #000', display:'flex', alignItems:'center', justifyContent:'center' }}>`.
- Swap the child icon per scene with an SVG asset switched via `interpolate` or a state passed from the scene config.
- Keep icon animation simple — a scale-in at scene start is enough.

---

## 7. B-Roll & Media Handling

**What it is:** Mixed B-roll: stock footage of real practitioners plus the drawn stick-figure animation. Each stock clip is framed by a simple colored box matching its martial art's icon color — flat presentation, no rounded corners or drop shadows. It is kept alive only by the Ken Burns motion from section 4.

**Where it shows:** Practitioner clips at 0:04, 0:48 and one per section, each in its colored frame.

**How to build it in Remotion:**
- Render B-roll as full-bleed `<Img src={...} />` with `objectFit: 'cover'` inside a 100% × 100% container, wrapped in the colored-box frame via a border div.
- No `borderRadius`, no `boxShadow`.
- Apply the Ken Burns transform from section 4 as a wrapper style on the `<Img>`.

---

## 8. Audio-Visual Sync

**What it is:** Strong, intentional sync between narration and visuals — when a technique is named, its stick-figure animation appears immediately. Voice-over only, no music bed to beat-map against.

**Where it shows:** Punches/kicks at 0:11; the Krav Maga multi-icon combo synced to the hybrid explanation at 4:33; the Discord CTA stick figure at 12:38.

**How to build it in Remotion:**
- Build a keyword→visual trigger map: parse the narration transcript for keywords (`punch`, `kick`, `joint lock`, `throw`) and render the matching animation in a `<Sequence from={timestampOfKeyword}>`.
- Data-driven sync: `frame = Math.round((timestamp / fps) * fps)`.
- For crisp sync, use a 60fps composition (`fps: 60`) so animations land exactly on the spoken beat.

---

## 9. Intro & Outro Pattern

**What it is:** Cold-open with a fast montage of the martial-arts icons (0:00) straight into content — no branded logo sting. Outro is a direct spoken + visual CTA ("join my Discord, link in the description") with a stick figure directing attention to the comments section (12:38), over the final frames — no end-screen animation.

**Where it shows:** Icon montage at 0:00; Discord CTA at 12:38 (end of 12:44).

**How to build it in Remotion:**
- Intro: no logo sting; open with the icon-montage `<Sequence>` at frame 0, then the first subject label.
- Outro: an `<AbsoluteFill>` holding a static Discord/logo asset for the last ~5s, plus a `<Sequence>` playing the CTA voice-over and the pointing stick figure.
- Add a subtle 1s fade to black at the very end to signal completion.

---

## 10. Unique Signature Moves

**What it is:** The elements that make this channel recognizable:
1. **The consistent black-and-white stick-figure "character"** reused across every art — readable movement and a distinct house style.
2. **Icon shorthand** for abstract concepts (brain for philosophy, warning triangle for "no competitions," combined icons for hybrid arts).
3. **The color-coded circular chapter indicator** as persistent wayfinding — each art owns a color used across its icon, box frame, and highlights.

**Where it shows:** Stick figures everywhere (0:00–12:38); brain/icon shorthand on concept beats; the top-right color-coded badge throughout.

**How to build it in Remotion:**
- Standardize the character as a shared `<StickFigure pose="..." />` SVG component driven by a `pose` prop, so every scene reuses the same art without re-drawing.
- Define the icon set as a `Record<string, ReactNode>` lookup keyed by martial art.
- The color-coded chapter badge is the single recurring "brand" element — keep it consistent and it becomes your visual signature.

---

### One honest note on section 10
The color-coded circular badge and the icon shorthand are the strongest signature elements the analysis surfaced — they are what make the video feel distinctive, and the most worth protecting as you build the Remotion system.

### Built-in weaknesses worth avoiding
The analysis flagged three: the repetitive stick-figure style can fatigue over 12 minutes; the bordered-box stock integration reads slightly low-budget; and there are no mid-roll "breather" moments or comparison beats to hold attention across the full length. If you rebuild this, consider a comparison-chart slide after every ~4th art (e.g., "Striking vs. Grappling") for added value and visual contrast.
