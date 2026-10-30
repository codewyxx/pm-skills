# Example: Reducing Manual Follow-up in a Support Queue

## Request

The operations team asks for a bulk reminder button in the support queue.

## Problem chain

- Original request: add a bulk reminder button.
- User: operations specialist handling overdue support tickets.
- Scenario: each morning the specialist opens the queue and manually copies ticket IDs into an IM group.
- Current workaround: manual copy and paste, around 40 tickets per day.
- Cost: missed reminders, inconsistent wording, and 30–45 minutes of repetitive work.
- Desired outcome: every overdue ticket receives a traceable reminder without manual copying.
- Why now: the queue has grown and missed reminders are affecting response time.

## Recommendation

Recommend a pilot: add a bulk action that sends the existing reminder template to selected overdue tickets, with a result page and audit log. Do not build custom reminder scheduling in this iteration.

## Scope

**In scope:** select overdue tickets, choose the standard reminder template, preview count, send, show per-ticket result.

**Out of scope:** custom template editor, scheduled reminders, multi-channel delivery, customer-facing messages.

## Metrics

- Primary: percentage of overdue tickets with a reminder sent within 24 hours.
- Leading: manual copy time per day.
- Guardrail: duplicate reminder rate and opt-out/complaint rate.

## Key assumptions

- The existing reminder template is approved for this use.
- Operations can define overdue criteria.
- A single daily send window is enough for the pilot.

## Open questions

- Who owns the overdue criteria?
- Should tickets with no assignee be excluded?
- What is the maximum batch size?

## Decision

`pilot` — proceed to PRD after confirming the overdue criteria and batch limit.