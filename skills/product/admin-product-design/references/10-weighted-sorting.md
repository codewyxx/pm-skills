# 10 — Multi-Factor Weighted Sorting Model

## Load when

Use when a list's order must combine multiple attributes and operations users can configure factors, weights, or scoring methods in the admin UI.

## Concepts

| Concept | Definition |
|---|---|
| Factor | A normalized score from 0–100 derived from one attribute. |
| Weight | The factor's share of the final score, in percent. |
| Method | The function mapping a raw value to a 0–100 score. |
| Enabled factor | `enabled = true`; participates in scoring. |

## Score formula

```text
score = Σ(enabled_factor_score × enabled_factor_weight)
        ÷ Σ(enabled_factor_weight)
```

Rules:

- **MUST:** only enabled factors participate in numerator and denominator.
- **MUST:** disabled factors have no effect on the total.
- **MUST:** define a tie-breaker; default is `updated_at DESC`, configurable.

## Factor schema

| Field | Type | Rule |
|---|---|---|
| `factor_id` | string | Globally unique, system-generated. |
| `code` | string | Business code; immutable after creation. |
| `name` | string | Editable display name. |
| `method` | enum | One of the supported scoring methods. |
| `params` | object | Parameters required by the method. |
| `weight` | number 0–100 | Percent. |
| `enabled` | boolean | Disabled factors are excluded from scoring. |
| `builtin` | boolean | Built-in factors cannot be deleted, only disabled. |

## Scoring methods

### `field_value`

Use an existing field, optionally normalized to 0–100.

| Param | Meaning |
|---|---|
| `field` | Source field, e.g. `category_weight`. |
| `normalize` | Whether to normalize to 0–100. |

Use for category weights, manual ranking scores, or other direct scores.

### `decay`

Score decays over time; newer objects score higher.

| Param | Meaning |
|---|---|
| `field` | Timestamp field, e.g. `published_at`. |
| `half_life_days` | Days required for the score to halve. |

### `const`

Give every object the same score.

| Param | Meaning |
|---|---|
| `value` | Fixed score from 0–100. |

Use as a placeholder weight or uniform baseline.

## Weight constraints

- **MUST:** enabled weights sum to exactly 100% before activation.
- **MUST:** the configuration UI validates in real time and shows the current sum.
- **MUST:** when the sum is not 100%, show the sum in red and disable save/activation.
- **DEFAULT:** allow an inactive draft with a non-100% sum; do not allow it to take effect.

## Factor management

- **MUST:** built-in factors are system-seeded, `builtin = true`, cannot be deleted, and can be disabled.
- **MUST:** names, methods, params, and weights of built-in factors are editable.
- **MUST:** custom factors are `builtin = false` and support create/read/update/delete.
- **MUST:** deleting a custom factor requires confirmation; if referenced by data, block deletion or surface the dependency risk.
- **MUST:** `code` cannot change after creation; `name` can change.

## Enable, disable, and activation

- **MUST:** disabling a factor immediately removes it from numerator and denominator.
- **MUST:** enabling requires re-validating the total weight to 100%.
- **DEFAULT:** changes take effect through cache, 5 minutes by default and configurable, to avoid frequent full recomputation.
- **MUST:** tell the operator when changes will take effect.

## Tie handling

- **DEFAULT:** equal scores sort by the configured secondary field descending.
- **DEFAULT:** secondary field is `updated_at`, newest first.
- **MUST:** allow the secondary field to be configured and validated.

## Configuration UI

- **MUST:** show a factor table: code, name, method, params, weight, enabled, actions.
- **MUST:** show a live weight-sum validation area.
- **MUST:** provide add custom factor, edit factor, enable/disable, and delete.
- **MUST:** save shows a toast with the cache activation delay; reset restores the last saved values.
- **MUST:** weight edits may be saved as draft but cannot activate below/above 100%.

## Initialization and boundaries

- **DEFAULT:** seed a valid 100% set of built-in factors for the business domain.
- **MUST:** business teams may trim or extend built-in factors according to their scenario.
- **MUST NOT:** include A/B experiment assignment in this model unless explicitly designed as a separate feature.
- **MUST NOT:** provide per-user personalized sorting; all users see the same order for the same list.
- **MUST NOT:** recalculate in a real-time stream; use the documented cache/recompute cycle.

## Required PRD output

- List of factors, types, params, weights, and enabled state.
- Formula and tie-breaker.
- Built-in vs custom behavior.
- Weight validation and activation rules.
- Cache/recompute latency and operator messaging.
- Boundaries and non-goals.
- Any deviation under `差异点`.

## Validation checklist

- [ ] Formula includes only enabled factors in numerator and denominator.
- [ ] Enabled weights sum to 100% before activation.
- [ ] Factor codes are immutable and built-in factors cannot be deleted.
- [ ] Tie-breaker is deterministic.
- [ ] Cache latency and activation behavior are visible to operators.
- [ ] Personalization, A/B assignment, and real-time recomputation are excluded unless explicitly added.