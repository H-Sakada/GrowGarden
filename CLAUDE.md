# GrowGarden

## Skills

Use only these from the `taste-skill` plugin:

- `taste-skill:taste-skill` (design-taste-frontend)
- `taste-skill:minimalist-skill`
- `taste-skill:soft-skill`
- `taste-skill:redesign-skill`

Do not use the others (`brutalist`, `brandkit`, `gpt-tasteskill`, `image-to-code`,
`imagegen-frontend-*`, `output-skill`, `stitch`, `taste-skill-v1`).

## Ponytail + taste skills

Ponytail stays active. When the two conflict:

- **Ponytail wins on how much code exists** — no speculative abstractions, no
  scaffolding, no new dependency for what CSS or a few lines already do.
- **Taste skills win on how it looks** — typography, spacing, color, motion,
  component structure.

Visual quality is a requirement, not over-engineering. Shipping a bland default
to save lines is the wrong trade here. Shipping a component library to style one
page is also the wrong trade.
