# Instructions — Modern Coaching Landing Page (Safarov & Sagi)

## Goal

Rebuild the landing page from scratch, inspired by MacroFactor.com's design language — alternating high-contrast sections, bold editorial typography, minimal nav, and confident copy — but adapted for a **human fitness coaching service** (frontal + online). No app downloads, no AI-slop imagery, no generic stock photos.

---

## Files Involved

| File | Action |
|---|---|
| `index.html` | Full rewrite |
| `assets/styles.css` | Full rewrite |
| `assets/coach1.jpg` | Keep as-is |
| `assets/coach2.jpg` | Keep as-is |
| `INSTRUCTIONS.md` | Keep as-is (deployment guide) |

No npm, no build step, no external JS libraries. Pure HTML + CSS + vanilla JS.

---

## Design Philosophy (MacroFactor-inspired, coaching-adapted)

| MacroFactor Principle | Our Adaptation |
|---|---|
| Alternating black/white full-width sections | Same — creates visual rhythm |
| Bold wide headings | Bebas Neue (numbers/Latin) + DM Sans Bold (Hebrew) |
| Clean body copy | DM Sans 400 for all body text |
| Blue accent glow | Warm orange (#e8611a) — energetic, human, non-generic |
| Minimal fixed navigation | Sticky nav: brand name left, single CTA right |
| Real photos, not stock | Use existing coach1.jpg / coach2.jpg |
| Authoritative short-form copy | Short Hebrew power statements + one-line explanations |

---

## Color Palette

```
--color-black:      #0a0a0a      (near-black backgrounds)
--color-white:      #f5f4f0      (warm off-white backgrounds)
--color-accent:     #e8611a      (warm orange — main accent)
--color-accent2:    #c94f10      (darker orange — hover states)
--color-text-light: #1a1a1a      (text on white sections)
--color-text-dark:  #f0ede8      (text on black sections)
--color-muted:      #888888      (secondary text / labels)
```

---

## Typography

```
Headings (H1/H2):  "Bebas Neue" — for Latin/numerals/brand name
                    All-caps, letter-spacing: 0.04em
Hebrew headings:   "DM Sans" weight 700 — has clean Hebrew support
Body / Labels:     "DM Sans" weight 400
Both imported via Google Fonts CDN
```

> **Hebrew + Bebas Neue note:** Bebas Neue has no Hebrew glyphs. Hebrew headings render in DM Sans Bold. Bebas Neue is used for: logo/brand name, stat numbers, and any Latin text. This is intentional — creates strong typographic contrast and a premium dual-language feel.

---

## Implementation Plan

### Section 1 — `<nav>` Sticky Minimal Navigation
- Transparent background on load → solid black after 60px scroll (JS scroll listener)
- Left (RTL = visual right): Brand name "SAFAROV & SAGI" in Bebas Neue, orange separator dot
- Right (RTL = visual left): Single button "ייעוץ חינם" → anchors to #contact
- Height: 64px, `position: fixed`, `z-index: 100`
- Transition: `background 0.3s ease`

---

### Section 2 — `.hero` Dark Black Background
- Big H1 in two lines using DM Sans Bold (Hebrew): "אל תתפשר / על הגוף שלך"
- Sub-copy: "ליווי מקצועי בפיזי ואונליין. מבוסס מדע. מותאם אישית."
- Two CTA buttons: Primary orange "ייעוץ ראשוני חינם" + ghost "הכר את הצוות ↓"
- Coach portraits: side-by-side portrait cards (coach1.jpg, coach2.jpg), grayscale by default
- Bottom: warm orange glow divider

---

### Section 3 — `.method` Off-White Background
- Headline: "המתודולוגיה"
- 3 cards (number + icon + title + body):
  - 01 — מדע: "כל תוכנית מבוססת על עקרונות היפרטרופיה המוכחים"
  - 02 — מעקב: "ניטור שבועי, עדכונים שוטפים, ותיאום מתמיד"
  - 03 — אדפטציה: "התוכנית מתאימה לך — לא אתה לתוכנית"
- Card style: Large orange number (01/02/03 in Bebas Neue) + bold DM Sans title

---

### Section 4 — `.services` Black Background
- Headline: "איך עובדים איתנו"
- Two large side-by-side cards:
  - Card A: "אימון פרונטלי 1:1" — bullet list of inclusions + CTA link
  - Card B: "ליווי אונליין" — bullet list of inclusions + CTA link
- Card style: 1px orange border, hover → orange glow `box-shadow`

---

### Section 5 — `.coaches` Off-White Background
- Headline: "הצוות"
- Two portrait cards using coach1.jpg / coach2.jpg
  - Grayscale → color on hover (CSS `filter` transition)
  - Name in DM Sans Bold, Role in DM Sans italic, 2–3 line bio
- Roman Safarov: training & hypertrophy specialist, 10+ years experience
- Sagi: nutrition & online coaching specialist

---

### Section 6 — `.results` Black Background
- Headline: "תוצאות אמיתיות"
- Sub-line: "לא לפני-אחרי מזויפים. רק מספרים." 
- 3 stat cards with count-up animation on scroll:
  - +12 ק"ג — שריר ממוצע בשנה הראשונה
  - 87% — מהמתאמנים עמדו ביעד ב-6 חודשים
  - 4+ — שנות ניסיון ממוצעות של לקוחותינו
- **Note:** Placeholder stats — client provides real numbers

---

### Section 7 — `.contact` Orange Background (only colored section)
- Headline: "מוכן להתחיל?"
- Sub: "השאר פרטים ונחזור אליך תוך 24 שעות."
- Form fields: Name, Email, Phone (optional), Goal dropdown
- Dropdown options: מסה | חיטוב | כוח | שיפור כללי
- Submit button: Black with white text
- Backend: Existing Google Sheets script URL (copy verbatim from current index.html)

---

### Section 8 — `<footer>` Black Background
- Brand name + tagline on one side
- Instagram + WhatsApp icon links (inline SVG) on the other
- Copyright line

---

## Animations & Interactions

| Element | Animation |
|---|---|
| Nav | bg fades to black on scroll (JS event listener) |
| Section entry | IntersectionObserver → fade + slide up (CSS keyframes) |
| Coach photos | grayscale → color on hover (CSS filter transition) |
| Service cards | orange glow box-shadow on hover |
| CTA buttons | scale(1.03) + brightness on hover |
| Stats | Vanilla JS count-up on IntersectionObserver trigger |

All via CSS transitions + vanilla JS. Zero external libraries.

---

## Risks / Edge Cases

1. **Hebrew RTL layout:** Use `margin-inline-start/end` instead of `margin-left/right`. Test all flex rows under `dir="rtl"`.
2. **Bebas Neue — no Hebrew:** Architecture above accounts for this. DM Sans covers all Hebrew.
3. **Coach photo dimensions unknown:** Use `object-fit: cover` in a fixed-aspect-ratio container.
4. **Stat numbers (placeholder):** Mark clearly in code comments so client can update.
5. **Form Google Sheets URL:** Copy from current index.html — do not change.
6. **No `styles.css` in root — it's in `assets/styles.css`:** Keep this path.

---

## Troubleshooting Log

_(empty — implementation not yet started)_
