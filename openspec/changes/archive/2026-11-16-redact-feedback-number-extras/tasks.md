## 1. Spec delta

- [x] 1.1 Modify **Payload privacy** in `mcp-analytics` so a number in a property sanitized as free text is read as plain digits and becomes `"[redacted]"` when the personal data pass would change it
- [x] 1.2 Add a scenario for a card number in a number feedback field

## 2. Prose alignment (applied at archive, outside the requirement-delta mechanism)

- [x] 2.1 Property reference: a number in `$mcp_feedback_<name>` is sanitized as free text

## 3. Validation

- [x] 3.1 Run `openspec validate --specs --strict`
- [x] 3.2 Run `openspec archive` to sync the delta and archive the change

## 4. Downstream follow-ups (separate changes, not this one)

- [ ] 4.1 posthog-js and posthog-python sanitize number feedback extras
- [ ] 4.2 posthog-sdk-test-harness: a step binding for the new scenario, then add it to
  `acceptance/public/mcp-analytics.feature`
