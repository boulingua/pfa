---
title: "About this course"
author: "S. Le Boulanger"
description: "What the Persian course is, how it is built, what it declares about its own scope, and how to reuse it."
---

This is a free, openly-licensed reference course in **Modern Persian** —
standard Iranian Farsi, {{< fa >}}فارسیِ معیار{{< /fa >}} — written for learners
at a German *Gesamtschule* and for independent self-studiers. It is one of the
language courses of the [boulingua](https://github.com/boulingua) platform and
follows the same shape as its established sister sites for
[German](https://boulingua.github.io/daf/),
[English](https://boulingua.github.io/efl/) and
[French](https://boulingua.github.io/fle/): units as page bundles, exams as
first-class pages, materials generated locally and committed to the repository,
and every claim about level traceable to a descriptor identifier.

## Why Persian, and why this course

Persian is a large language with a small teaching footprint in Germany. Schools
with substantial Iranian and Afghan heritage populations have, in practice,
almost nothing structured to offer them, and independent learners searching for
free material find phrasebooks, font demonstrations and grammar tables — rarely
a route from the alphabet to a defensible B1. The gap is not a shortage of
enthusiasm; it is a shortage of the unglamorous parts: a syllabus, exams, marked
answer keys, printable worksheets, and a script stage that takes the writing
system seriously enough to spend two weeks on it.

This course is an attempt at those parts. It is also the platform's second
right-to-left course after Arabic, and the two are built to share one
right-to-left and bidirectional-text foundation rather than each paying the full
cost alone.

## What it contains

- A pre-A1 **[script stage](/script/)** — eight units on the Perso-Arabic
  alphabet, the four positional forms, the seven non-connecting letters, the
  Persian-specific letters {{< fa >}}پ چ ژ گ{{< /fa >}}, the Persian digits
  {{< fa >}}۰۱۲۳۴۵۶۷۸۹{{< /fa >}}, and the passage from fully vocalised text to
  ordinary unvocalised writing.
- **[A1](/level-a1/)**, **[A2](/level-a2/)** and **[B1](/level-b1/)** — twelve
  units each, following the five-move model *Objectives → Input → Practise →
  Produce → Reflect*.
- **Exams** after every third or fourth unit and at the end of each level, each
  with a duration, a total, a marking key and a published grade boundary table.
- **[Appendices](/appendices/)** — the course conventions, a glossary, a
  pronunciation and script guide, a verb reference, an errors list, assessment
  rubrics, and a reader of classical couplets.
- **[Materials](/materials/)** — slide decks and worksheets as PDFs, with
  editable sources, plus native-voice audio for vocabulary and dialogue.

## What it declares about itself

The declared conformance target is **`core`**: CEFR **A1 to B1**. Every unit
names the descriptor identifiers it realises, and each level ships a
machine-readable coverage manifest that has to resolve against the curriculum
framework's registry before the level counts as finished. Scales for which the
Common European Framework's Companion Volume provides no descriptor at a given
level are recorded as `no-official-descriptor` rather than being filled with
something invented; the framework treats a declared gap as conformant and a
silent one as a failure.

B2, C1 and C2 are gaps, stated as gaps. So is the pre-A1 stage's position
outside the CEFR proper: it is a script-onboarding stage, not a level, and it
says so.

**Variety.** The course teaches the standard Iranian variety. Dari, the
Afghan standard, and Tajik, written in Cyrillic, are related but separately
standardised; they are named and situated in cultural notes at B1 and are not
taught here. Claiming otherwise would be cheaper than doing it properly.

## How the script is handled

Persian is written in the Perso-Arabic script, right to left, and — unlike the
beginner Arabic that textbooks usually vocalise — normally without short-vowel
marks. The course follows real usage rather than a teaching fiction: full
vocalisation in the script stage and the first third of A1, then ordinary
unmarked text. A single Latin transliteration scheme accompanies new vocabulary
through A1 and is then dropped.

Site chrome and scaffolding prose are in English. Persian is never set as the
page language; each Persian run is wrapped individually as a right-to-left run
in its own language, so bidirectional text stays local, punctuation stays where
it belongs, and the surrounding English layout is never flipped. The full set of
conventions — transliteration, vocalisation, *ezāfe* notation, register policy,
numerals — is published as the [course conventions](/appendices/style-guide/) so
that it can be checked rather than inferred.

## How it is made

The site is a static Hugo build from the shared boulingua course template. Slide
decks and worksheets are generated locally from branded LaTeX templates and
**committed** as PDFs — continuous integration verifies them but never builds
them, so a broken toolchain can never take the site down. Audio is generated
from an openly-licensed synthetic voice where a production-quality Persian one
can be verified, and recorded with a native speaker where it cannot; whichever
applies is stated on the page rather than glossed over.

Sources are openly licensed or public domain, and cited. No copyrighted text,
image or recording is reproduced. Classical poetry is used only from
verifiably public-domain editions, with the edition named.

## Licence and reuse

Teaching content is licensed **CC BY-SA 4.0**; the site code is **MIT**.
Teachers may use the material as it stands, adapt it for a group, or lift a
single worksheet, provided the attribution and the share-alike condition are
kept. The repository is public: corrections, and reports of anything wrong in
the Persian, are welcome as issues.

Individual text pages carry an anonymous VG Wort counting mark, which records
page views for the author's statutory remuneration claim. It sets no cookie,
stores no personal data, and is described in full in the
[privacy statement](/datenschutz/).

## Author

S. Le Boulanger. Contact and the legal notices required under German law are on
the [Impressum](/impressum/) page.
