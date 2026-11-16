## Why

**Property reference** sends a number feedback extra as is, but the same number inside an object extra
is sanitized as free text. A host that declares an integer report argument such as `reference` gets a
card number like `4111111111111111` sent raw as `$mcp_feedback_reference`, while
`{"reference": 4111111111111111}` in an object extra comes out redacted. The agent writes both, so both
can carry the personal data free text is cleaned of.

## What Changes

- **Property reference**: a number in `$mcp_feedback_<name>` is sanitized as free text. A boolean is
  still sent as is.
- **Payload privacy**: a number in a property sanitized as free text, on its own or inside JSON text,
  is read as its digits written out with no exponent. A number the personal data pass would change
  becomes the string `"[redacted]"`; any other number stays a number. One new scenario.
- A redacted number is sent as a string, so an SDK that starts doing this changes that property's type
  for those values. "Event schema stability" allows that for a rule the SDK did not meet before, with a
  release note.

## Capabilities

### New Capabilities

_None._

### Modified Capabilities

- `mcp-analytics`: **Payload privacy** and the Property reference.

## Impact

- **posthog-rs** already does this (PostHog/posthog-rs#310).
- **posthog-js** (`@posthog/mcp`) and **posthog-python** (`posthog.mcp`) send a number extra as is and
  need a small follow-up. Numbers inside object and array extras are unchanged.
