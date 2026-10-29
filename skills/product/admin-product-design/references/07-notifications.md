# 07 — Notifications, Channels, Copy, and Frequency Control

## Load when

Use for system-triggered messages: in-app inbox, app push, SMS, email, IM group notification, or operational alerts.

## Notification levels and channels

| Level | Typical scenario | Default channels |
|---|---|---|
| Strong alert | Money, security, deadline, account anomaly | In-app + SMS. SMS cost/threshold is **PENDING**. |
| Business warning | Quota, balance, cost anomaly, reconciliation mismatch | In-app + email; cannot be disabled. |
| Normal reminder | Review result, order state change, workflow node | In-app + app push. |
| Weak reminder | Comments, likes, social activity | In-app only, aggregated. |

Additional rules:

- **MUST:** SMS is for strong alerts only; never send the same event twice by SMS.
- **DEFAULT:** users may disable normal and weak push; strong alerts cannot be disabled.
- **DEFAULT:** B2B service notifications use in-app + email, including quota, reconciliation, and adjustment messages.
- **MUST:** the in-app inbox groups messages by business domain tabs, shows unread counts per tab and item, and supports `全部已读` and `仅看未读`.

## Trigger contract

Every notification **MUST** be defined by four fields:

| Trigger event | Recipient | Level | Channel(s) |
|---|---|---|---|

Rules:

- **MUST NOT:** write only "发送通知" without the four fields.
- **MUST:** trigger after the state change succeeds, never before the action commits.
- **MUST:** send at most once per event per recipient.
- **MUST:** aggregate batch events into one message and state the count.
- **MUST NOT:** notify the operator of their own action unless it is a security confirmation.
- **MUST:** define threshold tables for warning levels (e.g. 20% / 10% / 0%), with exact values supplied by the business.

## Copy structure

- **MUST:** use `事项 + 关键信息 + 引导动作`.
- **MUST:** include complete amounts, times, and IDs; do not replace them with "等".
- **MUST:** every notification has a link to a landing page that matches the message. If no landing page exists, state why.
- **DEFAULT:** title ≤ 20 characters; body ≤ 100 characters. Both limits are **PENDING**.
- **MUST NOT:** use exclamation-mark stacking, marketing hype, or emoji.

## Frequency and quiet hours

- **DEFAULT:** aggregate weak reminders of the same type within 1 hour. The window is **PENDING**.
- **DEFAULT:** avoid SMS between 22:00 and 08:00; money/security alerts are exempt. Quiet hours are **PENDING**.
- **MUST:** if daily volume grows abnormally, degrade to an aggregated digest. Define the threshold and behavior in the PRD.
- **MUST NOT:** aggregate or quiet-hours suppress warning alerts; send a recovery notification when the anomaly clears.

## Required PRD output

- A notification table with trigger event, recipient, level, channels, copy, landing page, and frequency cap.
- User preference behavior and non-disableable alerts.
- Threshold table for warning levels.
- Aggregation, quiet hours, retry, and recovery behavior.
- Every deviation under `差异点`.

## Validation checklist

- [ ] Every notification has all four trigger fields.
- [ ] Channel choice matches the level.
- [ ] Copy includes the key amount/time/ID and a working landing page.
- [ ] Batch events aggregate and state the count.
- [ ] No self-notification except security confirmations.
- [ ] Warning thresholds and quiet hours are configurable and marked when `PENDING`.