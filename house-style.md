# House style — site, Osservatorio Brutti, Grunt Watch

Three surfaces, one type system, one color per project.

---

## 1. Color

### Shared (all three surfaces)

```
sand          #F2ECDC   light ground (site, Osservatorio cards)
ink           #1E1B16   body text on sand
muted         #6B6557   metadata, captions, secondary text on sand
rule          #D9D0BC   hairlines, borders, dividers on sand
code-bg       #E9E1CD   inline code / code blocks

dark-ground   #141710   dark ground (Grunt Watch cards only)
dark-text     #EFE9D9   text on dark
dark-muted    #9B9684   metadata on dark
```

### Osservatorio Brutti — green

```
green         #1F5241   headword, wordmark, rule, highlight background
green-hover   #143A2D   link hover
green-on-dark #6FC49A   only if a dark surface is ever needed
```
Text on a green highlight is `sand`.

### Grunt Watch — purple

```
purple        #5B2A62   the mark on light surfaces
purple-hover  #3F1C45   link hover
lilac         #C08BD9   waveform on dark
```

Spectrogram colormap (5 stops, dark → bright):

```
#141710  →  #3A1B40  →  #7B3887  →  #C08BD9  →  #EBD5F4
```

The first stop equals `dark-ground` so the image has no visible edge
against the card. Normalize with a hard floor (clip the bottom ~5% of
dynamic range) and gamma ≈ 0.9.

### Rules

- Green and purple each mean one project. Never mix them on one surface.
- The accent marks the thing being observed: the borrowed word, the
  spectrogram, the waveform. Never a border, a band, or decoration.
- On the site, body links are `ink` with a 1px underline; green and
  purple appear only on the Osservatorio and Grunt Watch blocks.
- All pairs above pass WCAG AA at body size. Don't lighten `green`
  or `purple` further on sand, or darken `lilac` further on dark.

---

## 2. Type

Three families, everywhere.

```
Merriweather    400, 400i, 700   running text, gloss, quoted sentences
Archivo         400, 500, 600, 800, 800i   wordmarks, nav, labels, specimens
IBM Plex Mono   400, 500         dates, durations, counts, identifiers
```

One `<link>`:

```
https://fonts.googleapis.com/css2?family=Merriweather:ital,wght@0,400;0,700;1,400&family=Archivo:ital,wght@0,400;0,500;0,600;0,800;1,800&family=IBM+Plex+Mono:wght@400;500&display=swap
```

Rules:

- The specimen (headword / token) is always **Archivo 800 italic**.
  Italic is the linguistics convention for a cited form, so it carries
  meaning, not style.
- Any date, duration, count, or identifier is IBM Plex Mono. No exceptions
  — including publication years on the site.
- Merriweather never appears in a label or a nav item; Archivo never
  appears in running text.

---

## 3. Site (academicpages / Jekyll SCSS)

Colors are CSS custom properties in `_sass/theme/_default_light.scss`
(`:root`) and `_sass/theme/_default_dark.scss` (`html[data-theme="dark"]`).
Font stacks live in `_sass/_themes.scss`; the font link goes in
`_includes/head/custom.html`.

```scss
// _sass/theme/_default_light.scss
--global-bg-color:              #F2ECDC;
--global-text-color:            #1E1B16;
--global-text-color-light:      #6B6557;
--global-border-color:          #D9D0BC;
--global-code-background-color: #E9E1CD;

--global-link-color:            #1E1B16;   // ink + underline
--global-link-color-hover:      #1F5241;
--global-link-color-visited:    #1E1B16;

--global-masthead-link-color:       #1E1B16;
--global-masthead-link-color-hover: #1F5241;

// _sass/_themes.scss
$serif:      'Merriweather', Georgia, serif;
$sans-serif: 'Archivo', -apple-system, system-ui, sans-serif;
$monospace:  'IBM Plex Mono', Menlo, monospace;

$global-font-family:  $serif;
$header-font-family:  $serif;
$caption-font-family: $sans-serif;
```

Project blocks are the only colored elements on the page:
Osservatorio in `#1F5241`, Grunt Watch in `#5B2A62`.

Grunt Watch thumbnails are dark cards on a sand page — give them
generous margin and no border so they read as objects, not holes.
Gloss text on an entry page is real HTML, never baked into the image.

Two things to check: the dark-mode block in `_sass/theme/_default_dark.scss`
(invert ground and text, lift green to `#6FC49A` and purple to `#C08BD9`),
and hardcoded hex values outside the theme files — currently only the
`theme-color` meta in `_includes/head/custom.html`.

---

## 4. Osservatorio card (1080 × 1080)

```
ground        sand
padding       72px
wordmark      Archivo 600, 27px, green
rule          2px green, 18px below wordmark
headword      Archivo 800 italic, fit to width, ink
first-seen    IBM Plex Mono 400, 21px, muted
sentence      Merriweather 400, 36px / 1.55, ink
highlight     green background, sand text, 0 8px padding
attribution   Archivo 400, 22px, muted
```

---

## 5. Grunt Watch card (1080 × 1920)

```
ground        dark-ground
padding       72px 72px 88px
wordmark      Archivo 600, 27px, dark-text
handle        IBM Plex Mono 400, 18px, dark-muted, right-aligned
rule          2px dark-text, 18px below wordmark
spectrogram   936 × 860px, purple ramp
waveform      110px, lilac, directly beneath the spectrogram
axis line     IBM Plex Mono 400, 29px, dark-muted
token         Archivo 800 italic, fit to width, dark-text
gloss         Merriweather 400, 38px / 1.45, dark-text
attribution   Archivo 400, 32px, dark-muted; air date in IBM Plex Mono
```

Specimen sizing, by card:

- Osservatorio headword spans ~820px, clamped to 90–320px.
- Grunt Watch token spans ~600px, clamped to 90–220px.

Never let either wrap. Fit by measuring the rendered word, not by
letter count.

Gloss: one sentence, 10–14 words, 18 / ~110 characters hard maximum.
The claim only — no names, no setup. Those go in the caption.

Time window: the window is whatever the token needs, fades included.
A token is never clipped to fit. The axis reports the true duration,
which is what makes length legible; cards do not need matching windows.

Spectrogram rendering: narrowband window so harmonics resolve as
distinct horizontal lines, hard floor so the background is true
`dark-ground`, 4kHz ceiling on every card.

Renderer: `viz/grunt_viz.py --theme house`, fonts in `viz/fonts/`.
