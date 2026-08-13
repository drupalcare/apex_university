# APEX University

Higher-education sub-theme for [APEX](https://www.drupal.org/project/apex). Document-portal + featured-program homepage with three landing layouts (program / curriculum, faculty bio, event). Targets universities, colleges, vocational training, and K-12 districts.

## Overview

apex_university is the catalog's institutional-gravitas sub-theme. Per the [APEX Sub-Theme Catalog](../../docs/planning/APEX-SUBTHEME-CATALOG.md):

- **Audience**: universities, colleges, vocational training, K-12 districts
- **Visual identity**: serif display (EB Garamond) + readable sans body (Inter); deep-navy + crimson admissions accent + warm-gold outcomes accent
- **Homepage archetype**: Document portal + featured-program hero
- **Landing layouts**: program / curriculum, faculty bio, event (lecture / seminar)
- **Content emphasis**: service (degree programs), person (faculty + students), event (lectures / seminars), resource (research papers, course materials), announcement (admissions deadlines)

## Audience

Sites that need APEX's design-token rigor *and* institutional gravitas. Drupal already powers Harvard, Yale, Princeton, Stanford, MIT, NYU and hundreds of other universities — the audience research backs higher-ed as **the** highest-Drupal-vertical-adoption segment of the catalog. WCAG 2.2 AA minimum (DOJ Title II readiness for state/local public entities by 2026-2027), AAA where possible. AI tutor / assistance slots and microcredential prominence are first-class concerns per the 10-year audience read.

## Visual identity

| Aspect | Choice |
|---|---|
| Display font | Institutional serif (EB Garamond; Garamond / Book Antiqua / Palatino / Georgia fallback) |
| Body font | Readable sans (Inter; system fallback) |
| Type scale | Compact in directories (line-height 1.4), generous in program detail (1.65) |
| Palette | Deep-navy `#1e3a8a` primary + crimson `#b91c1c` admissions accent + warm-gold `#b45309` outcomes accent (overridable via `apex_schemes` for institution-specific colors) |
| Density | Dense in directory pages, generous in program detail |
| Layout direction | LTR + RTL via logical properties |
| Accessibility | WCAG 2.2 AA baseline; elevated focus ring (3px outline + 2px offset) for SC 2.4.11 readiness |

## Layouts

### Homepage — Document portal + featured-program

Region map per the catalog:

```
[apex_top_bar — current students / faculty / alumni quick-links]
[apex_header — logo + utility nav]
[apex_main_navigation — admissions / academics / research / about]
[apex_hero — featured program (degree + outcomes + Apply CTA)]
[apex_content_pre — quick links (apply / visit / give)]
[apex_content — news + events + program-finder]
[apex_content_post — outcomes data strip + alumni stories]
[apex_footer — comprehensive site map + accreditation + accessibility statement]
```

### Landing layouts

| Archetype | Drupal template | Content type |
|---|---|---|
| Program / curriculum | `node--apex-service--full.html.twig` | apex_service |
| Faculty bio | `node--apex-person--full.html.twig` | apex_person |
| Event (lecture / seminar) | `node--apex-event--full.html.twig` | apex_event |

## SDC components

Per the catalog spec — 5 components ship with apex_university:

- `apex-university-program-card` — degree summary in three sizes (hero featured / grid program-finder / compact related-programs); credits + duration + outcomes preview + Apply CTA
- `apex-university-faculty-card` — directory or feature-size card with portrait + name + title + research areas + optional contact
- `apex-university-outcome-strip` — career-outcomes data band (3-5 metrics) with optional source citation; the #1 buyer-credibility cue per EDUCAUSE buyer research
- `apex-university-deadline-banner` — admissions deadline countdown with low / medium / high urgency states; inline-start accent bar carries state per the no-background-state rule
- `apex-university-credit-badge` — microcredential / certificate badge in pill or card sizes; supports the 10-year-read prediction that microcredentials become prominent

Components live in `components/<name>/` per the [sub-theme contract](../../docs/architecture/sub-theme-contract.md#sdc-components-contract). Each ships a `.component.yml` schema, `.twig` template, and component-scoped `.css`.

## Demo content

apex_university's demo content pack (`content/`) imports ~50 nodes via `drush apex:import-demo apex_university` once the manifest is finalized:

| Content type | Count |
|---|---|
| apex_service (degree programs) | 8 |
| apex_person (faculty) | 12 |
| apex_event (lectures / seminars) | 8 |
| apex_resource (research papers, course materials) | 10 |
| apex_announcement (admissions deadlines) | 7 |
| apex_article | 5 |

## Installation

```bash
composer require drupal/apex_university
drush theme:enable apex_university
drush config:set system.theme default apex_university
drush cr
```

The sub-theme **automatically enables every APEX module** the parent theme depends on.

To install the demo content pack:

```bash
drush apex:import-demo apex_university   # Drush command shipped by W5 Phase A scaffolding
```

## Customization

Per the [APEX cascade-layer contract](../../docs/architecture/css-cascade-layers.md):

- **Plain CSS** in this sub-theme beats every `@layer apex.*` rule. Brand assertions (typography pair, palette anchors, focus-ring color) go here.
- **Layered CSS** (`@layer apex.base`, `@layer apex.components`, etc.) opts into a default that admin Live Editor / modules can override.

Institutional brands typically swap the navy primary, crimson accent, and warm-gold outcomes for their own school colors via apex_schemes — the engine derives the full per-region palette from those three anchors.

## Dependencies

- Drupal core `^11.1`
- `apex_theme` (parent theme — auto-pulls every APEX module the parent depends on)

## Screenshots

_Pending Phase 5 docs polish per [W2 v1-readiness](../../docs/planning/workstreams/2-apex-v1-readiness.md)._

## Changelog

See [CHANGELOG.md](./CHANGELOG.md).

## Troubleshooting

_Pending Phase 5 docs polish. For now, see [APEX-KNOWLEDGE-BASE.md](../../docs/APEX-KNOWLEDGE-BASE.md) and the [APEX briefing](../../docs/APEX-BRIEFING.md)._

## License

GPL-2.0-or-later. Part of the [APEX](https://www.drupal.org/project/apex) design system. Sub-themes are FREE per the [APEX commercial structure](../../docs/planning/workstreams/INDEX.md#commercial-structure-locked-expanded-2026-04-26) — more sub-themes = stronger sales funnel for the paid `apex_builder`.
