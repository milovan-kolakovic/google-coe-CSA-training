# Google Ads CoE — Strategic Review Training

Internal training deck for Client Solutions Advisors, delivered by the Google Ads Center of Excellence.

It is not a Google Ads course. It covers how to **read** an account: the order to check things in, the two numbers that locate a problem, a live teardown including the dead ends, and how to present a monthly Google report to a client.

**Format:** single self-contained HTML page, 18 scroll sections. No build step, no dependencies, no JavaScript framework.

---

## Deploy

### 1. Push to GitHub

```bash
git init
git add .
git commit -m "Google Ads CoE strategic review training"
git branch -M main
git remote add origin git@github.com:<org>/google-ads-coe-training.git
git push -u origin main
```

### 2. Import to Vercel

1. Vercel dashboard → **Add New** → **Project** → import the repo
2. Framework Preset: **Other**
3. Build Command: *leave empty*
4. Output Directory: *leave empty* (repo root)
5. **Deploy**

`vercel.json` handles the rest. There is nothing to configure and no environment variables.

Or from the CLI:

```bash
npx vercel --prod
```

### Access

The page ships with `<meta name="robots" content="noindex, nofollow">` so it stays out of search results. That is *not* access control — anyone with the URL can open it. For genuinely restricted access, turn on **Vercel Authentication** under Project → Settings → Deployment Protection, which limits it to your Vercel team.

---

## Presenting

| Action | How |
|---|---|
| Next / previous section | `→` `↓` `PageDown` / `←` `↑` `PageUp` |
| Jump to any section | Click a dot in the left rail (hover shows the label) |
| Full screen | `F11` (Windows) / `⌃⌘F` (macOS) |

The agenda is on the title slide. Runs about 30 minutes plus questions. Works down to phone width; the dot rail hides below 680px.

---

## Contents

| # | Section | Covers |
|---|---|---|
| 1 | What Google Ads is accountable for | The control boundary — query, click, page, form vs. everything outside it |
| 2 | Where Google sits | Demand capture vs. demand generation |
| 3 | A healthy account | Five numbers with the ranges we hold accounts to |
| 4 | Immature to mature | The five stages and the four evidence gates between them |
| 5–6 | Five common mistakes | Broad match, no steady week, wrong conversion action, thin budget, page mismatch |
| 7 | **The CTR × CVR matrix** | The 2×2 that locates any problem to one half of the funnel |
| 8 | Optimization | Cadence by activity, and the bid strategy ladder |
| 9 | What only Google tells you | Search terms as voice-of-market, the demand ceiling |
| 10–12 | **Brandito teardown** | Real account: June's collapse, three wrong turns, the fix and the result |
| 13 | The handoff | The one question to answer before any client call |
| 14–16 | Part 2 — Monthly report | Nine-beat structure and four client pushbacks |
| 17 | Core principles | Eight-point summary |

### The teardown account

The teardown uses **Brandito**, a real client, with the real June → July turnaround: a conversion tracking gap that made a normal month look like a collapse, broad match moved to phrase and exact, three ad groups paused. Cost per lead went $524 → $321 and leads 9 → 14 on the same budget.

All figures tie out at campaign, brand/non-brand, and account level, so the maths holds if someone checks it live.

To swap in a different account, replace the tables in sections `s10`, `s11`, and `s12`. Keep the shape of the story — a metric that misleads, a root cause, and at least one wrong turn — since the reasoning is the lesson, not the numbers.

---

## Editing

Everything lives in `index.html`. Design tokens are at the top of the `<style>` block:

```css
:root {
  --g: #0a0e17;   /* page background        */
  --s: #111a2b;   /* alternate section      */
  --r: #152034;   /* card surface           */
  --o: #0099D1;   /* Impactable blue        */
  --green: #00C4B3;
  --amb: #FFB627; /* dead ends, warnings    */
  --navy: #1A3B6D;
}
```

Type is Archivo Black (headings), Inter (body), JetBrains Mono (labels and figures), loaded from Google Fonts.

### Adding or removing a section

Three places must stay in sync, or the dot rail desyncs from the content:

1. The `<section id="sN">` itself
2. Its `<button class="pip" … onclick="goto('sN')">` in `#sidenav`
3. The `sections` array in the `<script>` at the bottom

Verify with:

```bash
grep -o 'id="s[0-9]*b\?"' index.html          # sections
grep -o "goto('s[0-9]*b\?')" index.html       # nav buttons
grep -n 'const sections' index.html           # JS array
```

All three lists must match in length and order.

### Reusable components

The deck shares its design system with the Outreach & Nurturing CoE training, so these classes carry over: `.sec` / `.sec.alt` / `.sec.dark`, `.card`, `.q-badge`, `.badge.b-ok|b-watch|b-broken`, `.grid2`–`.grid5`, `.tt` (data tables), `.dtier` (diagnostic rows), `.d-chain` (process strips), `.obs-grid` (observation → meaning → action), `.dead` (dead-end callouts), `.mtx` (the 2×2), `.mf-row` (benchmark bars), `.quote`, `.sb-judgment`.

---

## Accessibility

Contrast was measured against rendered pixels with alpha composited, not estimated from CSS. Every text element clears WCAG AA; all but the smallest mono labels clear AAA (7:1). Sections are keyboard-navigable and the dot rail buttons carry `aria-label`s.

---

*Impactable · Internal. Archive this alongside the training recording.*
