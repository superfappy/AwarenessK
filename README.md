# Case File №9183 — *The Lagos Lie*

> Kitopi · Information Security · Phishing simulation post-incident debrief.
> An interactive forensic walkthrough of the **Microsoft 365 sign-in alert** phishing campaign launched 27 April 2026.

A self-contained, dark-noir, 600 × 600 training experience — paired specifically with the *"Unusual sign-in activity detected"* payload. Trainees are walked through the message they just received as if it were a case file, with each red flag recovered as an "Exhibit" and stamped accordingly.

---

## Twelve scenes, one investigation

| # | Scene | Beat |
|---|-------|------|
| 0 | **Cold open** | Typewriter narrative + InfoSec badge reveal |
| 1 | **Case file cover** | Manila folder, red string, click-to-open |
| 2 | **Exhibit A** | The phishing email itself, stamped `FORGERY` |
| 3 | **EV·01 — The Sender** | Magnifying glass on `.co` vs `.com` |
| 4 | **EV·02 — The Clock** | Animated 4-hour countdown — urgency = manipulation |
| 5 | **EV·03 — The Geography** | Lagos vs Dubai pin map — "geographic shock" tactic |
| 6 | **EV·04 — The Weapon** | File flip — `.docx` → `credential_harvester.exe` |
| 7 | **EV·05 — The Silence** | "Do not reply" — no out-of-band channel |
| 8 | **The Pause** | Pull quote: *amygdala fires before cortex reads* |
| 9 | **Field Manual** | Four protocols: PAUSE / READ / VERIFY / REPORT |
| 10 | **How to report** | Outlook → Report Message → Phishing + `security@kitopi.com` fallback |
| 11 | **Field Exam** | Five interactive drills, 100-pt scoring, ranked badge |
| 12 | **Case closed** | Stamp slam, sign-off, restart option |

### Field Exam (Scene 11) — full certification flow

An intro pane introduces the structure, then five interactive missions with a live score meter and 5-pip progress tracker:

| # | Mission | Pts | Mechanic |
|---|---------|----:|----------|
| I | **STAKEOUT** | 25 | Find tells in a mock email — tap each suspicious element; tooltip explains why it's wrong. 5 tells worth 6/6/5/5/3 pts. 3 of 5 needed to pass. |
| II | **DOMAIN FORENSICS** | 15 | Pick the imposter URL out of four. The trap: `microsoft.com.id` (where the real domain is `.com.id`, an Indonesia ccTLD). |
| III | **RAPID TRIAGE** | 25 | Sort 4 inbox cards into Safe / Suspicious / Phish. Includes homoglyph (`amaz0n-billing.com`), typo-squat (`docusgn.net`), genuine Atlassian, and an in-domain-but-suspicious payroll message. |
| IV | **THE PAUSE** | 15 | A pulsing red "VERIFY NOW" alert appears with a 5-second countdown ring. Don't click. The button IS the trap. |
| V | **RECONSTRUCTION** | 20 | Place 4 response steps in correct order. "Reply asking if it's real" is a deliberate trap tile worth -5 if used. |

Result screen shows: animated final score, ranked badge, per-mission breakdown (color-coded by full/partial/zero), personalized tutor summary, generated CERT ID + filing date, and Retake / Close The Case buttons.

Score tiers:
- **90–100 → AGENT** · Phishing Defence Tier IV (badge in phosphor green)
- 75–89  → **INVESTIGATOR** · Tier III
- 55–74  → **OBSERVER** · Tier II
- 0–54   → **RECRUIT** · Tier I (badge muted, encourages a retake)

---

## Audio narration (optional)

Each substantive scene has a corresponding audio slot. To enable narration, drop voiceover files into a top-level `/audio` folder using the naming convention `audio01.mp3` through `audio10.mp3`. The controller will:

- Play the audio for the current scene automatically when the scene becomes active.
- Stop the previous audio cleanly on every scene transition (forward or backward) — no overlap is possible.
- Stop and restart correctly when the user clicks PREV/NEXT mid-narration.
- Try `.mp3` first, then fall back to `.mp4` (audio track only — useful if you're exporting from video editors that won't render mp3).
- Silently fall back to no-audio if neither file exists for a scene.

Mapping (scene index → file):

```
audio/audio01.mp3  →  Scene 1  · Case file cover
audio/audio02.mp3  →  Scene 2  · Exhibit A — the email
audio/audio03.mp3  →  Scene 3  · EV-01 The Sender
audio/audio04.mp3  →  Scene 4  · EV-02 The Clock
audio/audio05.mp3  →  Scene 5  · EV-03 The Geography
audio/audio06.mp3  →  Scene 6  · EV-04 The Weapon
audio/audio07.mp3  →  Scene 7  · EV-05 The Silence
audio/audio08.mp3  →  Scene 8  · The Pause (interlude)
audio/audio09.mp3  →  Scene 9  · Field Manual
audio/audio10.mp3  →  Scene 10 · How to Report
```

Cold open (0), Field Exam (11), and Case Closed (12) are intentionally silent — the exam shouldn't have voiceover competing with the trainee's focus.

A small audio toggle button sits in the HUD next to the EVIDENCE counter. It animates a 4-bar wave equalizer when audio is playing and switches to a muted-speaker icon when the user mutes it. The user's mute preference persists across all subsequent scenes in the session.

**Browser autoplay note:** modern browsers block autoplay until the user has interacted with the page. The controller queues the first scene's audio and triggers it on the user's first click or keypress (typically the OPEN CASE FILE button on the cold-open). Subsequent scene transitions play immediately.

## Aesthetic

Forensic noir + cyberpunk surveillance. Manila folder cream against deep night-blue, blood-red ink stamps that slam in with rotation, terminal phosphor green for data readouts, surveillance amber for highlights. Paper grain + scanline + vignette overlays throughout.

**Type stack** — Special Elite (typewriter body), Black Ops One (military stencil headers/stamps), JetBrains Mono (data/terminal), DM Serif Display (pull quotes).

---

## Project structure

```
case-file-9183/
├── index.html          # 13 scenes + HUD + nav + disclaimer + interactive exam
├── style.css           # Noir + scene-specific styling + exam UI + audio toggle
├── script.js           # Scene controller, typewriter, exam scoring, audio engine
├── audio/              # (optional) narration files — audio01.mp3 .. audio10.mp3
└── README.md
```

Pure HTML/CSS/JS. **No build step. No npm. No bundler.** Fonts pulled from Google Fonts CDN. Drop-in deploy.

---

## Deploy to GitHub Pages

1. Create a new repo (e.g. `case-file-9183` or your campaign repo).
2. Push the four files above to the repo root:
   ```bash
   git init
   git add .
   git commit -m "Case File 9183 — phishing debrief"
   git branch -M main
   git remote add origin git@github.com:<user>/<repo>.git
   git push -u origin main
   ```
3. In the repo on GitHub: **Settings → Pages → Build and deployment → Source: Deploy from a branch → Branch: `main` / root → Save**.
4. Within ~60 seconds the site is live at `https://<user>.github.io/<repo>/`.

To pair this with the phishing simulator, drop the GitHub Pages URL into the post-click landing redirect in your campaign config.

---

## Controls

- **Click** the `[ OPEN CASE FILE ]` button or the manila folder to advance early scenes.
- **Hover** the sender domain card on EV·01 to deploy the magnifying glass.
- **Reveal True Payload** flips the file on EV·04.
- **Arrow keys** or the **PREV / NEXT** buttons navigate between scenes once past the cold open.
- **`i`** in the top-right opens the simulation disclaimer.

---

## Customization

- **Trainee location** — EV·03 hard-codes Dubai as "YOU". Edit `pin-pulse-you` / `pin-label-you` in the SVG block of `index.html` if you re-run this for non-EMEA tenants.
- **Reporting address** — Scene 10 references `security@kitopi.com`. Change the `.email-snip .es-v` text in `index.html` if your IR mailbox differs.
- **Case ID** — `2026-04-27-9183` appears in five places (cold open, HUD, folder, closed scene). Search/replace as one block.
- **Severity / vector / filed date** — `index.html` § `.folder-grid`.

---

## Browser support

- Chrome, Edge, Firefox, Safari — current versions.
- Mobile: scales proportionally below 660 × 660.
- Reduced motion: respected via `prefers-reduced-motion`.

---

## Credits

Built for Kitopi · Information Security.
Design + implementation: Ahmed (Jimmy) · Senior Security Analyst.
Campaign vector: M365 Identity Alert · Lagos persona.

---

*"The next time you see one in the wild — you'll see it."*
