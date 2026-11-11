# Visual experience architecture
## Screen map
| Route proposal | Primary visual | Action |
|---|---|---|
| /stories | Person portrait/story cards | Select theme and content mode |
| /stories/:slug | Present-day scene | Choose behavior |
| Same player, layer state | Emotional/appraisal layers | Open meaning, need, strategy |
| Same player, timeline state | Life periods and related moments | Inspect past without erasing present |
| Same player, perspective state | Same event from another participant | Compare reports/interpretations |
| Same player, loop state | Repeating interaction sequence | Identify reinforcing steps |
| Same player, scenario state | Side-by-side possible continuation | Choose and compare |
| Same player, context state | Family/work/community neighborhood | Change scale |
| /studio/:id | Scene and graph authoring | Draft, validate, review |
| /account/data | Private data controls, S5 | Export/delete |

## Visual grammar
Observation: solid outline plus document icon. Participant report: quote icon and attribution. Hypothesis: dashed outline and question marker. Authored fiction: persistent fiction badge. Scenario: branching icon and conditional caption. Meaning: separate ornamental frame and named tradition. Unknown: visible empty placeholder, never a fabricated memory.

Warm/cool colors distinguish narrative tension and possibilities, not good/bad people. No brain scan imagery suggesting measured biology. An illustrative bodily reaction is labeled illustrative. Subject identity is not encoded as an enduring red dangerous-person badge.

Animation indicates the author's proposed relationship. A directional arrow alone cannot imply proven causation. Edge labels remain available in compact form and full accessible text.

## Composition
Desktop: scene occupies roughly two-thirds of viewport, contextual controls at side, time scrubber below. Inspection drawer opens on demand, never three permanent walls of prose. Mobile: full-width scene, bottom sheet for detail, stacked perspective comparison. Only one focused subgraph is rendered at once.

Five primary actions: Keçmişə bax; İç dünyanı aç; Baxışı dəyiş; Başqa izah; Başqa yol. Additional actions appear contextually. Back restores exact scene, perspective and timeline position.

## Scene contract
A scene references a background asset, stable character assets, expression/pose variants, caption keys, optional dialogue/audio cues, hotspot geometry, relation IDs and accessible narrative text. Media are illustrative; changing a facial expression cannot create a new psychological claim.

Play/pause controls sequence timing. Scrub goes to authored scene boundaries and supported cue timestamps. A skipped scene preserves required context through a brief neutral summary. The timeline supports approximate dates and unknown intervals rather than inventing birthdates.

## Interaction requirements
- Selecting a hypothesis opens supporting, contradicting and missing information.
- Perspective switching preserves event and story revision, not necessarily emotional interpretation.
- Alternative explanation highlights changed edges without moving every node.
- Counterfactual changes appear in a separate branch overlay; canonical history stays intact.
- Scale change expands a bounded neighborhood; default max 30 nodes, hard request cap 100.
- Selecting an outcome shows conditions and agency limits, not a success probability.
- Meaning mode can be disabled at any time and cannot affect factual filtering.

## Accessibility and performance proposals
Keyboard-accessible hotspots with visible focus; ordered DOM text mirrors scene order; captions/transcripts for all narration; minimum target size 44 CSS px; WCAG 2.2 AA contrast targets; no color-only information. Reduced-motion replaces traveling animation with highlighted snapshots. Screen-reader mode provides a linear event/report/hypothesis/choice reading order.

Do not announce every animation tick. Announce state changes once. Audio never autoplays with sound. Pause animation on hidden tabs. Use optimized responsive images; load next likely scene rather than whole biography. Static image + text fallback supports WebGL-disabled devices.
