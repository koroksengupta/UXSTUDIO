# UX Research Studio

A one-page student handout for a UX research studio course. It sets out five
open-ended research briefs, the ground rules every group follows, what each
group hands in, and how the work is graded.

The site is plain HTML and CSS. It has no JavaScript, no build step and no
dependencies beyond two Google Fonts, which fall back to system fonts.

## Contents of the handout

| Section | Anchor | What it covers |
| --- | --- | --- |
| Overview | `#overview` | What the studio asks of students, and how to read a brief |
| The five briefs | `#briefs` | One card per brief, each with a statement, hidden tension, people to talk to, sharper questions and pitfalls |
| Ground rules | `#rules` | Hypothesis first, sampling, paired comparison, ethics and consent |
| What you hand in | `#deliverables` | Nine deliverables, each with a minimum evidence bar |
| Grading | `#grading` | Rubric weights (total 100) with strong and weak examples |

The five briefs, each built around two roles who see the same problem differently:

1. **Planned, Bought, Still Wasted**: Planner and Cook
2. **Handed Over, Still Independent**: Older adult and Helper
3. **Jobs Everywhere, Candidates Nowhere**: Student and Screener
4. **Neatly Lost**: Storer and Searcher
5. **Agreed, Explained, Still Disputed**: Tenant and Landlord

## Project structure

```
.
├── index.html        # All page content, grouped into commented sections
├── css/
│   └── styles.css    # All styles, in numbered sections (see the contents list at the top)
├── README.md
└── .github/
    └── workflows/    # GitHub Actions
```

## Viewing the page

Open `index.html` in any browser. No server is needed.

To preview it on a local server (for example, to test on a phone on the same network):

```bash
python3 -m http.server 8000
# then visit http://localhost:8000
```

> **Sharing as a file:** the page loads its styles from `css/styles.css`. If you
> send someone only `index.html`, it will display without styling. Share the
> whole folder (or a zip of it), or send the hosted link instead.

### Publishing with GitHub Pages

1. Go to **Settings → Pages** in the repository.
2. Under **Build and deployment**, choose **Deploy from a branch**.
3. Select the `main` branch and the `/ (root)` folder, then save.

The handout will be published at `https://<username>.github.io/<repository>/`.

### Printing

The page has a print stylesheet. When printed or saved as PDF, it hides the
navigation, puts the hero text on white, and keeps each brief card and table
row on a single page.

## Editing the content

All text is in `index.html`. Every part of the page starts with a comment
banner, so you can search for `BRIEFS`, `GROUND RULES`, `DELIVERABLES` or
`GRADING` to find it.

### Adding, removing or renaming a brief

A brief appears in **two places**, and both must be kept in sync:

1. **The hero jump list** (`<ul class="pairs">` near the top). Each entry links
   to its card with `href="#brief-N"`:

   ```html
   <li><a href="#brief-6"><span class="pair"><span>Role A</span><span class="connector" aria-hidden="true"></span><span>Role B</span></span><span class="pair-name">Brief title</span></a></li>
   ```

2. **The brief card** inside `<section id="briefs">`. Copy an existing
   `<article>` and update its IDs:

   ```html
   <article class="brief" id="brief-6" aria-labelledby="brief-6-title">
     <h3 id="brief-6-title">Brief 6: Brief title</h3>
     <p class="brief-pair"><span>Role A</span><span class="connector" aria-hidden="true"></span><span>Role B</span></p>
     <blockquote>The statement students are given.</blockquote>
     <dl class="facts">
       <div class="tension"><dt>Hidden tension</dt><dd>…</dd></div>
       <div><dt>People to talk to</dt><dd>…</dd></div>
       <div><dt>Sharper questions</dt><dd>…</dd></div>
       <div><dt>Watch out for</dt><dd>…</dd></div>
     </dl>
   </article>
   ```

After changing the number of briefs, also update:

- the text that says "five" (the hero list title, the nav link, the section heading and the `<meta name="description">`);
- the staggered animation in section 13 of `styles.css`, which has one `nth-child` delay per row (rows without a delay still appear, just without the stagger).

### Editing the tables

On screens narrower than 720px, each table row becomes a stacked card. Each
cell shows its column name, read from its `data-label` attribute. If you rename
a column in `<thead>`, update the matching `data-label` on every cell in that
column.

The grading weights should add up to 100.

## Styling

`css/styles.css` is split into numbered sections, listed in the comment at the
top of the file. Colours, fonts and layout sizes are CSS custom properties
defined once in `:root`:

| Token | Value | Used for |
| --- | --- | --- |
| `--cobalt` | `#2340E8` | Brand colour, hero background, links, focus ring |
| `--marigold` | `#F5B935` | Accent: role connectors, quote rule, focus ring inside the hero |
| `--ink` / `--muted` | `#171A21` / `#4A5262` | Body and secondary text |
| `--paper` / `--white` / `--tint` | `#F4F6FA` / `#FFFFFF` / `#E7ECFB` | Page, card and highlight backgrounds |
| `--content-max` | `1120px` | Maximum content width |
| `--nav-h` | `3.75rem` | Height of the sticky nav, used as the offset when jumping to a section |

**The connector.** The "Role ●——● Role" line is the `.connector` component
(section 5 of the stylesheet). It is drawn entirely in CSS and stretches to any
width. To change its dot size or line weight for one use, set `--dot` or
`--stroke` on it.

**Breakpoints.** At 820px and below, the hero stacks into one column and fact
rows put their label above the value. At 720px and below, tables become
stacked cards and the section nav becomes a single row that scrolls sideways.

## Accessibility

- A skip link lets keyboard users jump straight to the main content.
- Headings run in order (`h1` → `h2` → `h3`), and each section and brief card is labelled by its own heading.
- Both navigation landmarks have labels ("Sections", and the hero's brief list).
- Decorative connectors are hidden from screen readers with `aria-hidden="true"`.
- Text colours meet WCAG AA contrast. The focus ring is at least 3:1 against every background it appears on.
- Motion is limited to one entrance animation, and it is turned off for visitors who set "reduce motion" in their system settings.

## Browser support

Current versions of Chrome, Edge, Firefox and Safari. The page uses CSS
custom properties, `clamp()`, grid and `:focus-visible`, which have been
supported by all of these since 2022.
