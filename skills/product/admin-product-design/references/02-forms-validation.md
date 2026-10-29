# 02 — Forms, Fields, Validation, and Submission

## Load when

Use for create/edit forms, login/registration forms, modal forms, field-level validation, or multi-step data entry.

## Required and optional fields

- **MUST:** mark required fields with a red asterisk before the label.
- **MUST:** leave optional fields unmarked; do not add a "选填" label.
- **MUST NOT:** submit a default value as if the user entered it unless the default unambiguously expresses user intent.

## Validation timing

| Check type | When it runs | UI behavior |
|---|---|---|
| Format validation | On blur | Show the error immediately below the field. |
| Required and cross-field validation | On submit | Validate together; focus the first invalid field. |
| Server or systemic failure | On submit/response | Show a form-level summary at the top. |
| Error recovery | On edit | Clear that field's error immediately. |
| Submit failure | After request | Preserve all entered values. |

## Error copy

- **MUST:** use "problem + required action", e.g. "手机号格式不正确，请输入 11 位手机号".
- **MUST NOT:** use content-free messages such as "格式错误" or "参数错误".
- **MUST:** inline field errors stay below the field; blocking system errors appear at the form top.

## Field defaults

| Field type | Validation |
|---|---|
| Phone | 11 digits, starts with `1`. |
| ID card | 18 characters, including checksum validation. |
| Unified social credit code | 18 characters, valid encoding rules. |
| Email | Standard email syntax. |
| Unique fields | Server-side uniqueness check on submit; conflict message and correction guidance. |
| Amount | Non-negative number, at most two decimal places; business upper bound comes from the PRD. |
| Text length | Frontend blocks excess input; show a counter near the limit. |

## Special form patterns

- **MUST:** a modal exact-lookup control requires the complete value (for example, all 11 phone digits) before querying.
- **MUST:** no-match handling follows `03-feedback-states.md`.
- **MUST:** multi-step matching flows (e.g. registration phone → employer-bound phone) document the matching chain and show it in the preview.
- **MUST:** conditionally displayed fields define the exact trigger condition.
- **MUST:** file and media fields use `06-display-and-media.md`; tabular uploads define file size, required columns, and format.

## Submit and leave behavior

- **MUST:** while submitting, disable the submit button and show a loading state; backend must enforce idempotency.
- **MUST:** leaving with unsaved changes prompts "当前内容未保存，确定离开？".
- **DEFAULT:** long forms over one viewport support draft autosave. The exact threshold is **PENDING**; confirm before implementing.
- **MUST:** restoring a draft tells the user that a draft was restored.

## Required PRD output

- Required/optional status for every field.
- Default values and whether they represent user intent.
- Validation timing, rule, error copy, and error placement.
- Cross-field and conditional-display rules.
- Unique/server-side checks and failure recovery.
- Submit loading, idempotency, unsaved-change handling, and draft behavior.
- Field-level deviations under `差异点`.

## Validation checklist

- [ ] Every field has a type, requiredness, default, validation rule, and error copy.
- [ ] Format and submit-validation timing are distinct.
- [ ] First-error focus and top-level error summary are specified.
- [ ] Dynamic fields state their trigger conditions.
- [ ] Submit is protected against double submission.
- [ ] `PENDING` thresholds are marked `TBD`, not presented as approved values.