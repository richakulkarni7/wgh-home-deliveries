# West Garo Hills — Non-Institutional Delivery Dashboard

## Project overview
This is a single-file HTML dashboard tracking non-institutional (home) deliveries
across 15 health facilities in West Garo Hills district, Meghalaya, India.

The dashboard file is `index.html`. Do not create separate JS or CSS files —
everything must stay in one self-contained file.

---

## Weekly update task

When asked to update the dashboard with a new PPT:

1. Extract text from the PPT file (it will be in the `ppts/` folder)
2. Find the summary slide — usually titled "Overall Total" near the end —
   and read the facility-wise HD / ID / Total counts from it
3. Get the district total row for the overall pct, hd, and tot values
4. Add the new week as a single entry at the END of the `WKS` array in index.html
5. Update the KPI cards and metadata (see "What to update" below)
6. Confirm what was added — week label, district totals, and any notable patterns

---

## WKS array — data structure

Each week entry in the `WKS` array looks like this:

```js
{w:"2–8 Mar", pct:83, hd:31, tot:183, fac:{
  "Allagre CHC":    {hd:0, tot:1},
  "Asanang PHC":    {hd:4, tot:10},
  "Babadam PHC":    {hd:0, tot:3},
  "Bhaitbari CHC":  {hd:1, tot:37},
  "Chibinang PHC":  {hd:0, tot:5},
  "Dalu CHC":       {hd:2, tot:15},
  "Dadenggre CHC":  {hd:9, tot:12},
  "Darengre PHC":   {hd:3, tot:13},
  "Jeldupara PHC":  {hd:0, tot:5},
  "Keraphara PHC":  {hd:1, tot:7},
  "Phulbari CHC":   {hd:0, tot:20},
  "Pedaldoba PHC":  {hd:1, tot:6},
  "Purakhasia PHC": {hd:5, tot:16},
  "Selsella CHC":   {hd:0, tot:10},
  "Tikrikilla PHC": {hd:5, tot:23}
}}
```

Field definitions:
- `w`   — short week label, e.g. "9–15 Mar" (use en-dash –, not hyphen -)
- `pct` — district institutional delivery % (integer or one decimal, e.g. 83 or 83.5)
- `hd`  — district total home deliveries (15 facilities only, exclude UPHCs/UHWCs)
- `tot` — district total deliveries (15 facilities only, exclude UPHCs/UHWCs)
- `fac` — per-facility object; ALL 15 facilities must be present every week

If a facility has no deliveries reported that week, use {hd:0, tot:0}.

---

## The 15 facilities — use these exact names, always

```
Allagre CHC
Asanang PHC
Babadam PHC
Bhaitbari CHC
Chibinang PHC
Dalu CHC
Dadenggre CHC
Darengre PHC
Jeldupara PHC
Keraphara PHC
Phulbari CHC
Pedaldoba PHC
Purakhasia PHC
Selsella CHC
Tikrikilla PHC
```

---

## Facilities to EXCLUDE from all data

These urban facilities (UPHCs and UHWCs) appear in the PPTs but are NOT part
of the dashboard analysis. Ignore them entirely:

- Dobasipara UPHC
- Matchakolgre UPHC
- Sampalgre UPHC
- Rongkhon UHWC
- Agillanggre UHWC
- Santinagar UHWC
- Soragre UHWC
- Lower Sangsanggre UHWC
- A'kim Dora UHWC
- Danakgre UHWC

---

## What to update in index.html after adding a new week

### 1. WKS array
Add the new week entry at the very end of the array (before the closing `];`).

### 2. KPI cards (in the overview pane)
Update these four values:
- **Total deliveries** — add the new week's `tot` to the previous running total
- **Home deliveries** — add the new week's `hd` to the previous running total
- **Avg. inst. %** — recalculate as the average of all non-null `pct` values in WKS
- **Best week** — update if the new week's pct is higher than the current best

### 3. Week count — update everywhere it appears:
- `hdr-meta` div in the header (e.g. "26 wks · 15 facilities")
- Page description under "District Summary" (e.g. "26 weeks · 15 facilities · West Garo Hills, Meghalaya")
- Card subtitles that say "all N weeks"
- Footer text
- The `of N weeks` text in the facility detail KPI card (in the JS template string)

---

## Week label format

Use short format with an en-dash:
- ✓ "9–15 Mar"
- ✓ "16–22 Mar"  
- ✓ "30 Mar–5 Apr"
- ✗ "9th to 15th March 2026"
- ✗ "9-15 Mar" (hyphen instead of en-dash)

---

## What NOT to change

- Do not modify any CSS
- Do not modify any JavaScript logic or functions
- Do not change the REASONS, FAC_REASONS, REASON_BY_FAC, or REASON_ACTION data
  (these are updated manually when a significant new reason pattern emerges)
- Do not restructure or reformat the file
- Do not split into multiple files

---

## Notes on the PPT format

- The summary slide is usually the second-to-last slide and is titled something like
  "Overall Total [date range]" or has a district total row at the bottom
- The district total row gives you pct, hd, and tot directly
- Per-facility counts come from the same summary slide
- Individual case narratives (earlier slides) are for qualitative reference only —
  they do not need to be parsed for the weekly data update
- Some weeks have partial facility data (a few facilities missing) — if so, use
  {hd:0, tot:0} for missing facilities and note it in your confirmation

---

## GitHub Pages deployment (optional)

After updating index.html, push to GitHub to update the live URL:

```bash
git add index.html
git commit -m "Add week of 9–15 Mar 2026"
git push
```

GitHub Pages will republish within ~1 minute.
