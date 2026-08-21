# PFA — Persian course roadmap

Build plan for the boulingua Persian-as-a-Foreign-Language course (`pfa`,
signature accent `#B5892B` light / `#E7C97E` dark, hover `#8C6A21`, pentagon
mark). This repo is currently a scaffold (LICENSE, README, brand icons) and is
flagged "coming soon" on the world map. This document is the actionable plan to
build the **entire** course — content and website — from the `pagegen` template
and the `curriculum` framework, conforming to the boulingua standards.

---

## 1. Overview

**What it is.** A free, openly-licensed (CC BY-SA 4.0 content, MIT code)
reference course in **Modern Persian / Farsi (فارسیِ معیار)** — the standard
Iranian variety — for German *Gesamtschule* learners and independent
self-studiers, published as a static Hugo site with committed slide decks,
worksheets, native-voice audio and CEFR-traceable units — the same shape as the
mature sister sites [DaF](https://boulingua.github.io/daf/),
[EFL](https://boulingua.github.io/efl/) and [FLE](https://boulingua.github.io/fle/).

**Realistic CEFR scope.** A pre-A1 **script-onboarding stage** ("Level 0") plus
**A1 → B1** proper. That maps to the framework's `core` conformance target
(A1–B1). B2/C1/C2 are declared as gaps, not faked — openly-licensed,
CEFR-traceable Persian OER is thin beyond intermediate level, and closing that
gap is a multi-year effort better left honest than simulated.

**Why this language.** Persian is a strategically important, under-served
language in German schools (a large heritage population from Iran and
Afghanistan) and among independent learners, with almost no free, structured,
CEFR-aligned, RTL-correct OER available. It is also a second proof point —
after Arabic — for the platform's RTL/Perso-Arabic-script capability, letting
the two RTL courses share infrastructure rather than each paying the full
technical cost alone.

**The 3–5 defining challenges.**
1. **Right-to-left layout + Perso-Arabic script** — the same category of lift
   as Arabic: hugo-coder chrome, CSS, the LaTeX materials pipeline and TTS all
   need to be RTL- and script-aware. Persian's script adds four letters
   (پ چ ژ گ) and its own digits (۰–۹) on top of Arabic's, so this is
   substantially — but not entirely — reusable from the `afl` build.
2. **The ezāfe construction (ِ‑ or ‑ی)** — an unstressed vowel/particle linking
   nouns to modifiers (خانه‌یِ من, "my house") that is usually **unwritten** in
   normal orthography but obligatory in speech, with no close German/English
   analogue. It must be taught explicitly and early since it silently
   underlies most everyday Persian syntax.
3. **Formal written vs. colloquial spoken register** — Persian has a wider gap
   between literary/formal register (writing, news, textbooks) and colloquial
   Tehrani speech (contracted forms, e.g. written *می‌روم* vs. spoken *می‌رم*)
   than most European languages. The course needs an explicit, honest policy
   for which register it teaches when.
4. **No grammatical gender, regular verb morphology** — a genuine pedagogical
   *advantage* relative to Arabic: grammar can move faster once the script is
   secure, freeing unit budget for vocabulary, register and the
   ezāfe/preposition system.
5. **Native-voice TTS coverage — better than Arabic's, not worse.** The
   assumption that Persian is the thinner of the two RTL courses here is
   backwards: upstream ships **five** `fa_IR` voices and **four of them are
   `CC0`**, while **no** Arabic voice states a licence at all. Audio is not gated
   on finding a voice. It is gated on auditioning one for quality on unvocalised
   running Persian (§2, §9).

---

## 2. Language & localisation decisions

Concrete, opinionated calls to make before authoring a single unit.

- **Variety → standard Iranian Persian (Farsi, فارسی).** *Recommended.* A
  reference course needs one written, teachable standard with a plausible CEFR
  mapping and the deepest pool of openly-licensed material; Tehran-based
  standard Farsi is it. **Dari** (Afghanistan) and **Tajik** (Cyrillic script,
  Tajikistan) are related but distinct standardised varieties — out of scope
  for v1, mentioned only in a short cultural/awareness note (mirrors how the
  Arabic course frames dialects it does not teach). Do not build a Dari or
  Tajik track in v1.
- **Script handling → native Perso-Arabic script throughout, with scaffolded
  transliteration that fades out.** Persian is normally written **without**
  short-vowel diacritics (unlike Arabic, which vocalises beginner text); the
  course follows real-world usage: full short-vowel marking only in the
  **Level-0 script stage** and early A1, then unmarked running text from A1
  core onward. A light Latin transliteration (one course-defined scheme,
  stated in the style guide) accompanies new vocabulary only through A1, then
  is dropped, as in the Arabic course.
- **RTL → first-class, shared with `afl`.** *Recommended architecture:* site
  **chrome and scaffolding prose in English**, matching EFL/AFL, with every
  Persian run wrapped `dir="rtl" lang="fa"` via a reusable `{{< fa >}}` inline
  shortcode and a `dir`-aware content CSS layer (logical properties:
  `margin-inline`, `padding-inline`, `text-align: start`). Enable hugo-coder's
  RTL affordances. This CSS/shortcode layer should be **built once and shared**
  with `afl` (see §8) rather than duplicated — Persian's needs are a superset
  (extra letters, different digits) of Arabic's, not a divergent system.
  German medium is a live open decision (§9), same as for Arabic.
- **Level-0 script-onboarding stage → YES, required.** A `pre-alpha` section
  ("The Persian alphabet / الفبای فارسی") before A1: the 32-letter Perso-Arabic
  alphabet (28 shared with Arabic + پ چ ژ گ), the four positional forms,
  non-connecting letters, Persian digits (۰۱۲۳۴۵۶۷۸۹) alongside Western
  numerals, and reading fully-vocalised words before normal unvocalised text.
  Modelled as its own content section, not a CEFR level; its can-dos map to
  `preA1` descriptors where they exist, else `no-official-descriptor`.
- **Web font → Vazirmatn as primary, Noto Naskh Arabic as fallback.**
  *Recommended.* **Vazirmatn** (SIL OFL, purpose-built for Persian UI/web text)
  gives authentic Persian glyph shapes and variable-font efficiency; **Noto
  Naskh Arabic** (SIL OFL) is the fallback/creative face for literary
  quotations and has full coverage of the Persian-specific letters and digits
  as a safety net. Confirm the pairing with a side-by-side legibility check in
  M1. Latin text keeps the template's Source Sans 3. Self-host both as WOFF2
  under `static/fonts/`; declare `unicode-range` so Perso-Arabic glyphs
  (including U+067E پ, U+0686 چ, U+0698 ژ, U+06AF گ and the Persian digit
  block U+06F0–U+06F9) come from the chosen face and Latin from Source Sans.
- **TTS → the survey is done, and Persian is well covered.** This entry used to
  defer the question to an M1 survey and to contrast Persian unfavourably with
  Arabic's `ar_JO-kareem`. The comparison was backwards. Upstream
  `rhasspy/piper-voices` (catalogue snapshot 2026-08-21, 174 voices) ships
  **five** Persian voices, all at `medium` tier, with these licences copied
  verbatim from their MODEL_CARDs:

  | voice | quality | licence | usable |
  |---|---|---|---|
  | `fa_IR-amir-medium` | medium | `CC0` | yes — **primary** |
  | `fa_IR-ganji-medium` | medium | `CC0` | yes |
  | `fa_IR-ganji_adabi-medium` | medium | `CC0` | yes — literary register |
  | `fa_IR-reza_ibrahim-medium` | medium | `CC0` | yes |
  | `fa_IR-gyro-medium` | medium | `See URL` | no — an unstated licence is not permission |

  Arabic has **no** voice with a stated licence: both `ar_JO-kareem` models read
  `License: See URL` and point at a repository carrying no licence statement. So
  Persian is the better-provisioned of the two RTL courses, not the poorer one.
  **Decision:** **`fa_IR-amir-medium`** is the primary voice, and
  **`fa_IR-ganji_adabi-medium`** — a literary register — is the natural second
  speaker, which gives `pfa` two distinct voices for dialogue and a register-apt
  reader for the classical-literature strand (§5). Voice IDs are read from
  **`audiogen/voices.yml`** (relocating to `kit/audio/voices.yml` at F1) and are
  never hand-typed; a transliterated ID is how a 404 gets written into a download
  script, and the old instruction to "add any viable voice to `audiogen`'s voice
  table" names a mechanism that no longer exists. **What stays open is an
  audition, not a search:** smoke-test on normal unvocalised running Persian
  (ezāfe-linked phrases, colloquial contractions) before bulk generation.
  **Fallback ladder:** `amir` → `ganji` / `ganji_adabi` / `reza_ibrahim` (same
  locale, all CC0) → **recorded human native-speaker audio for A1 core**, with
  `audiogen` coverage marked partial. Never an Arabic voice: the script is shared,
  the phonology is not, and voices are never substituted across languages.

---

## 3. Instantiation from pagegen

Stand up the site by copying the template verbatim, then changing only the
marked values.

1. **Copy the template** into this repo (preserve the existing `brand/`,
   `LICENSE`, `README.md`, `ROADMAP.md`): bring over `hugo.toml`, `go.mod`,
   `archetypes/`, `content/`, `layouts/`, `assets/`, `data/`, `i18n/`,
   `static/`, `scripts/`, `.github/`, `lychee.toml`, `.gitignore`,
   `.gitattributes`, `.nojekyll`, `LICENSE-CONTENT.md`, `CITATION.cff`.
2. **Edit `hugo.toml`** — change only the marked keys: `baseURL =
   "https://boulingua.github.io/pfa/"`; `title = "Persian (Farsi) — S. Le
   Boulanger"`; `languageCode`/`defaultContentLanguage = "en"` (chrome stays
   English/lingua-franca, Persian content wrapped per-run, §2/§9);
   `[params].navTitle = "Persian"`, `description`, `keywords`
   (`persian,farsi,cefr,rtl,course,oer`); `params.code = "pfa"` (selects the
   accent already in `data/accents.yaml`: `#B5892B` / hover `#8C6A21` / dark
   `#E7C97E`); `[[params.social]].url =
   "https://github.com/boulingua/pfa"`; `[params.plausible].domain =
   "boulingua.github.io/pfa"` (keep this block **last** under `[params]` —
   the TOML sub-table trap); `[[menu.main]]` sections mirroring `content/`:
   Script · A1 · A2 · B1 · Materials · About · Legal.
3. **Enable RTL affordances** — turn on hugo-coder's RTL layout support and add
   the `[dir="rtl"]` / `:lang(fa)` CSS layer to `assets/css/custom.css` (built
   jointly with `afl`, see §8); wire the `{{< fa >}}` shortcode analogous to
   Arabic's `{{< ar >}}`.
4. **Regenerate brand assets** — `python brand/make_icon.py` (or
   `python brand/make_icon.py pfa` if run from a different `code`) to render the
   pentagon + favicons at `#B5892B`; confirm `data/accents.yaml` already carries
   the `pfa` row (verified: `accent: "#B5892B"`, `hover: "#8C6A21"`,
   `dark: "#E7C97E"`, `dark_hover: "#EFDCA9"`) so no CSS colour values are
   hand-edited.
5. **Fill legal placeholders** — the ⟨…⟩ fields in `impressum` / `datenschutz` /
   `haftungsausschluss`; keep the VG Wort METIS disclosure in `datenschutz`, and
   remove the `|| true` on `verify_legal_placeholders.py` in
   `.github/workflows/build-deploy.yml` once genuinely filled (the template
   ships with `|| true` because pagegen itself has unfilled placeholders).
6. **First green build** — `hugo server` locally to confirm the accent, font
   and (initially, mostly-empty) RTL chrome render; then push to `main` so
   `build-deploy.yml` builds, runs the gate battery, and deploys to GitHub
   Pages; enable Pages (source: GitHub Actions). Milestone: a live,
   empty-but-styled Persian-accent site with the Perso-Arabic font wired and a
   working RTL smoke page.

---

## 4. Curriculum conformance target

- **Declared level → `core` (A1–B1).** Realistic and honest for openly-licensed
  Persian OER, matching the Arabic course's declared level. B2/C1/C2 declared
  as gaps per `docs/conformance.md` ("declare the gap; do not lower the
  framework to hide it").
- **Scales.** The registry (`curriculum/schema/scale-registry.yml`) has
  **79 in-scope** illustrative scales across REC / PROD / INT / MED / PLUR /
  LING / SOC / PRAG (SIGN is out of scope framework-wide). `core` requires
  implementing every in-scope scale with an official A1/A2/B1 descriptor.
  - **Implement fully:** reception, production, interaction, linguistic,
    sociolinguistic and pragmatic scales with A1–B1 descriptors — the
    backbone, where Persian's regular morphology (§1) buys extra unit budget.
  - **Implement thinly but present:** mediation (MED) and plurilingual (PLUR)
    scales — thin in beginner OER for any language, but every scale with an
    A1–B1 descriptor gets at least one realization; a silent gap is a
    conformance failure, a declared `no-official-descriptor` cell is not.
  - **Record `no-official-descriptor`** for every (scale, level) the CV leaves
    empty at A1/A2/B1, and `see-reference` where the CV points elsewhere.
- **Mapping units → descriptor IDs.** Each unit's `curriculum` front-matter
  block (`framework: cefr`, `cefr_level`, `cefr_can_do`) references stable
  descriptor IDs `{LEVEL}.{DOMAIN}.{SCALE}.{SEQ}` (e.g.
  `A1.INT.information-exchange.01`), per `curriculum/docs/id-scheme.md`. Author
  original Persian realizations of each ID; never reproduce Council of Europe
  text verbatim (a short `cite` + optional ≤15-word `quote` only, per
  `schema/can-do.schema.json`).
- **Publish the machine-readable scope/coverage manifest** — a `pfa`
  `conformance.yml` (mirroring `curriculum/examples/de-a1/conformance.yml`):
  `framework: boulingua-curriculum`, `framework_version`, `language: fa`,
  `level: A1` (then A2, B1), `declared_conformance: core`, and `realizations:`
  mapping each `implements_id` to its Persian can-do (`fa:` key, Perso-Arabic
  script), published at the **repo root**.
- **Gate.** The reusable workflow
  `boulingua/.github/.github/workflows/course-build.yml@v1` runs
  `python .curriculum/scripts/conformance_audit.py resolve --manifest conformance.yml --content content`,
  which covers format, uniqueness and that every `implements:` resolves to a real
  in-scope scale/level. `id-audit.sh` audits the framework's *own* level files and
  **cannot** validate this repo. Do not wire it here. Keep the template's reserved
  `verify_cefr.py` slot in `build-deploy.yml` alongside it.

---

## 5. Content creation plan

Phased by stage/level; each unit is a leaf page bundle
(`content/<section>/units/<unitNN-slug>/index.md`, `page_type: unit`) following
the five-step model (Objectives → Input → Practise → Produce → Reflect). Exams
are **first-class sibling bundles** (`…-exam/`, `page_type: exam`, sharing
`unit_nr`). Effort tags: **S** ≈ ½ day, **M** ≈ 1–2 days, **L** ≈ 3–5 days per
unit incl. materials + audio.

- **Recurring cast & theme.** A small ensemble anchored in **Tehran** — e.g.
  Sārā (سارا) a university student, Kāve (کاوه) who runs a family bookshop near
  the bazaar — reused across levels so vocabulary and story compound. Each
  unit centres one everyday theme; the ezāfe and formal/colloquial register
  distinction run through as a recurring grammar strand, not one-off topics.

| Phase | Section | Units | Focus | Effort |
|---|---|---|---|---|
| **0** | `content/script/` (pre-A1) | 6–8 | Alphabet, positional forms, non-connectors, Persian-specific letters (پ چ ژ گ), Persian digits, vocalised reading | M each |
| **1 (MVP)** | `content/level-a1/` | 10–12 | Greetings & politeness register, self/family, the ezāfe construction, café & food, numbers, city/directions, daily routine | M–L each |
| **2** | `content/level-a2/` | 10–12 | Past narration, shopping/bargaining (bāzār), travel, health, work, weather, comparison, colloquial-vs-formal verb contractions | L each |
| **3** | `content/level-b1/` | 10–12 | Opinions, news/media register, subjunctive, formal correspondence, an introduction to classical literary excerpts (Hafez/Saadi couplets as reading texts) | L each |

- **Exams.** One per 3–4 units + an end-of-level exam, each a `…-exam/` bundle
  with `duration_min`, `total_points`, `notenschluessel`, and a committed PDF
  under `static/downloads/<level>/`. Effort **M** each.
- **Appendices** (`content/appendices/<slug>/`, `page_type: appendix`):
  Persian–English glossary (transliterated A1 headwords), pronunciation &
  script guide, common-errors list (ezāfe omission, register mixing, bidi
  pitfalls), verb-conjugation reference, numerals & the Iranian calendar,
  assessment rubrics, and a **classical-literature reader** (public-domain
  Hafez/Rumi/Saadi/Ferdowsi couplets, graded by level — see copyright note
  below). Effort **M–L**.
- **The classical-literature advantage.** Persian's canonical poets (Hafez,
  Rumi/Mowlānā, Saadi, Ferdowsi) are long out of copyright, giving B1+ reading
  material a depth few OER courses have (short couplets as B1 reading texts,
  longer excerpts reserved for a future B2/C1 phase). Seed from A2/B1 onward as
  short, glossed, always-cited extracts (source + transcription edition).
- **Acceptance criteria per phase:** every unit has (1) a filled `curriculum`
  block with resolvable descriptor IDs, (2) `skills_focus` set, (3) a committed
  slide deck + worksheet with thumbnails, (4) native-voice audio for vocab &
  dialogue (or a recorded-audio fallback flagged per §2/§9), (5) all Persian
  wrapped `dir="rtl" lang="fa"`, (6) a registered VG Wort mark (§7), (7) a
  green build with all gates passing. A phase is "done" when its section
  landing lists every unit + exam and `conformance.yml` is green under the §4
  gate at that level.

---

## 6. Website & materials

- **Section landings via shortcodes.** Each `_index.md` (`page_type: section`)
  uses the template shortcodes (`hero`, `lead`, `card-grid`, `card`,
  `downloads`, `callout`, `kicker`, `details`) — never raw HTML. Add an
  `{{< fa >}}` inline shortcode wrapping Persian in `<span dir="rtl"
  lang="fa">`, plus a `dir`-aware block callout for worked examples —
  implemented once and **shared with `afl`** (§8) since the mechanics (wrap a
  run, flip direction, keep surrounding English LTR) are language-agnostic.
- **RTL/bidi CSS.** Extend `assets/css/custom.css` with logical properties and
  a `[dir="rtl"]` / `:lang(fa)` layer so Persian runs, tables and lists align
  right while English chrome stays LTR; self-host Vazirmatn (primary) + Noto
  Naskh Arabic (fallback) WOFF2 with `unicode-range` splits for the
  Persian-specific code points (§2) — the shared RTL base built with `afl`,
  extended with Persian's digit and letter ranges.
- **Materials pipeline (committed).** Decks from **slidegen** (Beamer) and
  worksheets from **sheetgen** — both already XeLaTeX + fontspec, so extend the
  Arabic-script branch (polyglossia + bidi, or `\arabicfont` via `fontspec`)
  with a Persian language variant: `\setotherlanguage{farsi}` (polyglossia
  supports Persian directly), Vazirmatn/Noto Naskh as `\newfontfamily`, RTL
  environments for Persian blocks, Persian digit rendering. Build locally with
  `build_materials_latex.py`; commit PDFs under `static/materials/` (+ ODP
  editable decks) and exam PDFs under `static/downloads/`. CI only verifies —
  no TeX Live in the deploy path.
- **Native-voice audio.** `audiogen` with **`fa_IR-amir-medium`** (CC0, §2) and
  **`fa_IR-ganji_adabi-medium`** (CC0) as the second, literary-register speaker →
  OGG/Opus committed under `static/materials/audio/` and referenced via the
  `audio-block` partial. Both are rows in `audiogen/voices.yml`
  (`kit/audio/voices.yml` from F1); fetch them with `get_voices.sh` and never
  retype an ID by hand. **Availability note, corrected:** Persian voices exist and
  are licence-clear — four of the five are CC0. What is unconfirmed is *quality*
  on unvocalised running Persian, so audition in M1 before bulk generation; the
  recorded-audio fallback (§2/§9) sits behind the voice ladder, not in front of
  it.
- **Thumbnails & downloads.** `render_thumbs.py` for deck/worksheet previews;
  `verify_downloads.py` gate confirms every referenced material exists and is
  attributed. Downloads hub and materials hub carry **no** VG Wort pixel (§7).

---

## 7. VG Wort — pixel assignment for ALL content pages

**Required and non-skippable.** Per `pagegen/docs/vgwort-standard.md`, every
editorial page ≥ 1800 rendered characters gets exactly **one** VG Wort
Zählmarke on exactly **one** URL. This is the author's statutory remuneration
right, not tracking — emitted static, JS-free, no consent gate, loading eagerly
for every reader, via the shared resolver `layouts/_partials/vgwort/url.html`.

- **Which pages get a mark:** every **unit**, every **exam**, every
  **appendix**, and long-form **editorial** pages (`/about/`, each section
  landing whose prose reaches 1800 chars). **Never** the home page, the
  materials/downloads hubs, tag/category indexes, paginated continuations, or
  the templated legal pages (Impressum/Datenschutz/Haftungsausschluss).
- **Note on Persian and Mindestumfang:** the 1800-char threshold counts
  *rendered prose*. Persian script is compact and pages mix Latin scaffolding,
  transliteration and Persian script; check the coverage audit's per-page char
  count and only register pages that genuinely clear 1800 chars of authored
  text — do not pad with transliteration purely to clear the threshold.
- **Process per page:** draw a fresh **public** code (32-hex) from the
  author's **T.O.M.** account → add it to `data/vgwort.yaml` keyed by `url:`
  (or `path:`) with `pixel_url`, `public_id`, `min_chars: 1800`, `author`,
  `registered_at` → the shared resolver renders the preload + eager `<img>` →
  record the code in the private usage registry kept **outside** this repo
  (§8 of the standard). Never invent codes, expose the private code, or reuse
  an assigned code.
- **Gates:** coverage audit (`verify_vgwort_coverage.py`, warns on
  unregistered ≥1800-char pages), manifest ↔ data (`verify_all_pixels.py`),
  render verify (`verify_rendered_pixels.py`, blocking: each registered pixel
  on exactly one URL), the manifest pixel gate (`scripts/verify-vgwort.sh`),
  and the hub guard (no `met.vgwort.de` on the materials hub). Exclude
  `vgwort.de` from `lychee.toml`.
- **Estimated total marks needed:** ~6–8 script-stage units + ~32 A1–B1 units
  + ~10 exams + ~6 appendices (incl. the classical-literature reader) + ~4
  editorial pages ≈ **58–64 Zählmarken** for the full `core` course. Draw them
  in batches per phase — script + A1 first (~22–24) — not all at once, so
  unused codes are not sitting idle against T.O.M.'s allocation.

---

## 8. Milestones & sequencing

- **M0 — Instantiation (S/M).** §3 complete: site copied, `hugo.toml` set,
  brand regenerated, legal filled, first green Pages deploy. *Depends on:*
  nothing.
- **M1 — RTL foundation (L), shared with Arabic.** Perso-Arabic web fonts
  self-hosted (Vazirmatn + Noto Naskh Arabic, unicode-range split), `{{< fa >}}`
  shortcode, RTL/bidi CSS layer, slidegen/sheetgen Persian branch,
  `fa_IR-amir-medium` auditioned on unvocalised running Persian — the survey is
  already done (§2), so this is a listening test, not a search. *Depends on:* M0.
  **Gating milestone** — no content authoring at scale until RTL renders
  correctly on site and in PDFs. **Coordinate with `afl`'s own M1:** design
  the shortcode mechanics, `[dir="rtl"]` CSS layer and LaTeX bidi/polyglossia
  scaffolding once as a shared RTL base, specialised per language (font,
  unicode ranges, digits) — whichever course lands M1 first makes the
  second course's M1 cheaper.
- **M2 — Script stage live (M).** `content/script/` (6–8 units) + glossary +
  pronunciation appendix, materials, audio, VG Wort marks. *Depends on:* M1.
- **M3 — MVP: A1 live (L).** 10–12 A1 units + exams + `conformance.yml` green
  under the §4 gate at A1. *Depends on:* M2. **First flip-worthy state.**
- **M4 — A2 (L).** *Depends on:* M3.
- **M5 — B1 + full appendices, incl. classical-literature reader (L).**
  `declared_conformance: core` complete. *Depends on:* M4.

**Definition of "done / ready to flip from coming-soon to active":** the map
pin flips at **M3** — script stage + full A1 with exams live, every A1 unit
CEFR-mapped and VG-Wort-marked, materials and audio committed (or audio scope
narrowed per §2/§9), all CI gates green, RTL correct on site and in PDFs,
`conformance.yml` passing at A1. "Course complete" is **M5** (A1–B1 `core`).

---

## 9. Open decisions & risks

- **Piper Persian voice — resolved in the course's favour, and no longer the
  highest content risk.** Availability and licence are settled: five `fa_IR`
  voices upstream, four of them `CC0`, primary `fa_IR-amir-medium` (§2). The
  contrast this entry once drew with Arabic's `ar_JO-kareem` was the wrong way
  round — that voice states no licence at all, so `afl` is the RTL course with the
  audio problem, not `pfa`. What remains is an **audition** in M1: does the
  synthesis handle unvocalised running Persian, ezāfe-linked phrases and
  colloquial contractions? If nothing clears the smoke test, fall to the other CC0
  `fa_IR` voices, then to recorded human audio for A1 core with audiogen coverage
  marked partial. *(Open as a quality question only; it no longer blocks
  planning.)*
- **Medium language (en vs de).** Recommended `en` for chrome consistency;
  the Gesamtschule audience argues for German scaffolding, same tension as
  Arabic. Decide before M2; prefer the same answer as `afl` for consistency
  across the two RTL courses unless a language-specific reason argues
  otherwise. *(Open.)*
- **Vazirmatn vs. Noto Naskh Arabic as primary body face.** Recommended
  Vazirmatn (native Persian shapes) with Noto Naskh Arabic as fallback/creative
  face; confirm with a side-by-side legibility check in M1. *(Open, low risk.)*
- **hugo-coder RTL completeness.** The theme may not fully support `dir=rtl`
  chrome; the English-chrome + wrapped-run approach sidesteps most of this, but
  navbar/ToC/footer need auditing under mixed bidi — shared work with `afl`.
  *(Risk.)*
- **LaTeX Perso-Arabic shaping.** polyglossia's Farsi support + bidi must
  render Persian-specific letters, digits and ligatures correctly in decks and
  worksheets; budget iteration time in M1, reusing lessons from the Arabic
  branch of slidegen/sheetgen. *(Risk.)*
- **Register policy drift (formal vs. colloquial).** The written-formal vs.
  spoken-colloquial split (§1) needs one style-guide rule (e.g. "formal
  written forms are the reference spine, with an explicit colloquial
  callout from A2 onward") applied consistently — otherwise the easiest thing
  for the course to drift on unit-by-unit.
- **Ezāfe notation policy.** Decide and record whether the unwritten ezāfe is
  marked (diacritic or transliteration gloss) in Level 0/A1 only, then left
  implicit from A2 — matching the vocalisation fade-out policy in §2.
- **Transliteration scheme.** Pick one Latin scheme and apply it uniformly
  through A1 only, then drop it — mixing schemes confuses learners more than
  an imperfect but consistent choice.
- **Numerals.** Decide Western (0–9) vs. Persian-Eastern-Arabic (۰–۹)
  presentation per level; recommend Persian digits (distinct glyphs from the
  Arabic-Eastern digits used in `afl`) in the script stage, Western numerals
  in English scaffolding.
- **Classical-literature copyright diligence.** The poets are public domain,
  but the specific edition/transcription of any excerpt must be checked —
  modern critical editions can carry their own copyright. Source only from
  verifiably public-domain transcriptions and cite the edition used.
- **Shared RTL infrastructure sequencing with `afl`.** Both courses are
  scaffolds today; whichever reaches M1 first effectively designs the shared
  RTL base for both — flag this cross-repo dependency so the second course
  does not duplicate or diverge from the first's RTL/bidi decisions.
