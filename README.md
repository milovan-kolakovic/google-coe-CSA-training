# Google Ads CoE — Strategic Review Training

Internal training deck for Client Solutions Advisors, delivered by the Google Ads Center of Excellence.

It is not a Google Ads course. It covers how to **read** an account: the order to check things in, the two numbers that locate a problem, a live teardown including the dead ends, and how to present a monthly Google report to a client.

**Format:** single self-contained HTML page, 23 scroll sections. No build step, no dependencies, no JavaScript framework.

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

Run of show is on the title slide: 30 min core, 15 min for the teardown and Q&A. Works down to phone width; the dot rail hides below 680px.

---

## Contents

| # | Section | Covers |
|---|---|---|
| 1 | What Google Ads is accountable for | The control boundary — query, click, page, form vs. everything outside it |
| 2 | Role in the ecosystem | Demand capture vs. demand generation, and why Google gets credit it didn't earn |
| 3 | Healthy account at a glance | Five numbers with the ranges we hold accounts to |
| 4 | Account maturity | Immature → mature, and the four evidence gates between stages |
| 5–7 | Five common mistakes | Broad match, no steady week, wrong conversion action, thin budget, query/page mismatch |
| — | **The method: CTR × CVR** | The 2×2 that locates any problem to one half of the funnel |
| 8–9 | Optimization | Cadence and impact by activity; the bid strategy ladder |
| 10 | Insights unique to Google | Search terms as voice-of-market, the intent ceiling, retargeting value |
| 11–15 | **Live teardown** | A full review in sequence, including three dead ends, six ranked findings, and the client sentence |
| 16 | The handoff | The one question a CSA must always be able to answer |
| 17–19 | Part 2 — Monthly report | Nine-beat structure and the four client pushbacks |
| 20 | Core principles | Twelve-point summary |

### On the teardown account

**Meridian Compliance is a composite** — a realistic but invented B2B SaaS account, labelled as such on the slide. All figures tie out arithmetically at campaign, non-brand, and account level, so it withstands someone checking the maths live. No client data is used anywhere in this deck.

To swap in a real anonymized account, replace the tables in sections `s11`, `s12`, and `s12b` and the findings list in `s13`. Keep the *shape* of the story — a blended metric that hides a problem, a root cause in the conversion setup, and at least one dead end — because the sequence is the lesson, not the numbers.

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
