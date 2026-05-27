# Visibility and Metadata

BindingEngine distinguishes between:
- semantic meaning
- visibility semantics
- editorial metadata
- system metadata

This distinction is foundational to the architecture.

Not every attribute should contribute equally to:
- semantic identity
- graph structure
- inference
- conflict detection

Some attributes exist primarily to control:
- presentation
- visibility
- publication
- workflow behaviour

BindingEngine therefore classifies attributes using semantic roles.

---

## Core Principle

Semantic structure and presentation structure are not the same thing.

Example:

```markdown
@event[
    type: battle,
    occurred-at: reckoning:348-ashmoon-03,
    revealed-at: 2026-07-18
](Battle of Thornbridge Holt)
```

In this example:
- `occurred-at` contributes to semantic chronology
- `revealed-at` controls presentation visibility

These concepts should remain architecturally distinct.

---

## Why This Matters

Many semantic systems incorrectly conflate:
- semantic truth
- publication state
- visibility rules
- editorial workflow

This often leads to:
- polluted graph identity
- unstable inference
- semantic ambiguity
- difficult access control
- broken provenance

BindingEngine intentionally separates:
- semantic meaning
- visibility semantics
- editorial metadata
- system behaviour

to avoid these problems.

---

## Attribute Roles

Attributes may declare semantic roles within vocabularies.

Current roles include:
- `semantic`
- `visibility`
- `metadata`
- `system`

Example vocabulary definition:

```json
{
  "identifier": "revealed-at",
  "valueType": "string",
  "role": "visibility"
}
```

Attribute roles allow downstream systems to reason differently about:
- semantic identity
- graph participation
- indexing
- visibility
- publication workflows

---

## Semantic Attributes

Semantic attributes contribute directly to semantic meaning.

Examples:
- `subject`
- `object`
- `type`
- `occurred-at`
- `location`

Semantic attributes may contribute to:
- projection identity
- graph structure
- inference
- conflict detection
- semantic traversal

Example:

```markdown
@event[
    type: birth,
    subject: jane-austen,
    occurred-at: gregorian:1775-12-16
](Birth of Jane Austen)
```

In this example:
- `type`
- `subject`
- `occurred-at`

all contribute to semantic meaning.

---

## Visibility Attributes

Visibility attributes control:
- who may see information
- when information may be shown
- publication timing
- spoiler behaviour
- reveal workflows

Visibility attributes should generally NOT contribute to:
- semantic graph identity
- semantic inference
- projection identity

Example:

```markdown
@event[
    type: battle,
    occurred-at: reckoning:348-ashmoon-03,
    revealed-at: 2026-07-18
](Battle of Thornbridge Holt)
```

`revealed-at` affects:
- presentation
- visibility
- user-facing access

It does NOT change:
- the semantic meaning of the battle
- the event identity
- the semantic graph structure

---

## Metadata Attributes

Metadata attributes represent supporting editorial information.

Examples:
- commentary
- author notes
- editorial state
- publication notes
- review status

Example:

```markdown
@event[
    type: battle,
    editorial-note: verify source chronology
](Battle of Thornbridge Holt)
```

Metadata attributes are typically preserved without contributing directly to:
- semantic identity
- graph structure
- inference

---

## System Attributes

System attributes support infrastructure or application concerns.

Examples:
- indexing hints
- migration markers
- workflow flags
- synchronization metadata

System attributes are intentionally application-specific.

Example:

```markdown
@event[
    type: battle,
    sync-version: 4
](Battle of Thornbridge Holt)
```

System attributes should generally avoid semantic participation.

---

## Visibility Workflows

Visibility attributes enable downstream systems to implement:
- spoiler management
- campaign reveal systems
- publication scheduling
- staged releases
- role-based access control
- editorial publishing workflows

without contaminating semantic structure.

Example workflow:

```text
ProjectionSet
↓
VisibilityPolicy
↓
FilteredProjectionSet
↓
User-Facing Output
```

---

## Reveal Systems

A common use case is staged information revelation.

Example:

```markdown
@event[
    type: betrayal,
    occurred-at: reckoning:348-ashmoon-03,
    revealed-at: 2026-07-18
](The Betrayal at Thornbridge Holt)
```

Internally:
- the semantic structure exists immediately
- projections may already exist
- conflicts may already be detectable

However:
- non-privileged users may not yet see the information

This distinction allows:
- deterministic semantic systems
- delayed presentation visibility

to coexist cleanly.

---

## Semantic Chronology vs Reveal Chronology

BindingEngine intentionally distinguishes between:
- domain chronology
- visibility chronology
- provenance chronology

Example:

```markdown
@event[
    type: battle,
    occurred-at: reckoning:348-ashmoon-03,
    revealed-at: 2026-07-18
](Battle of Thornbridge Holt)
```

| Attribute | Meaning |
|---|---|
| `occurred-at` | When the event happened in the domain |
| `revealed-at` | When the audience may see the event |
| source revision timestamp | When the document entered the system |

These concepts should remain distinct.

---

## Projection Behaviour

Projection should generally:
- preserve visibility attributes
- preserve metadata attributes
- preserve system attributes

while avoiding:
- incorporating them into semantic identity
- using them for graph identity generation

Example:

```text
event:birth:jane-austen:1775-12-16
```

should not change merely because:

```text
revealed-at = 2026-07-18
```

Projection identity should remain semantically stable.

---

## Assertions and Metadata

Assertions preserve all validated attributes, including:
- semantic
- visibility
- metadata
- system

The assertions layer intentionally avoids deciding:
- which attributes matter most
- which attributes affect identity
- how metadata should be interpreted

That responsibility belongs downstream.

---

## Visibility vs Canonical Truth

Visibility metadata does not imply semantic truth.

Example:

```markdown
@event[
    type: conspiracy,
    revealed-at: 2026-07-18
](The Royal Conspiracy)
```

This does NOT imply:
- the conspiracy is true
- the claim is canonical
- the event is historically accurate

It only controls:
- visibility semantics

Truth resolution remains separate from visibility handling.

---

## Provenance Preservation

Visibility and metadata attributes should preserve provenance just like semantic attributes.

Downstream systems should always be able to determine:
- where metadata originated
- which vocabulary defined it
- which document authored it
- which revision introduced it

Loss of provenance remains a serious architectural failure.

---

## Design Principles

BindingEngine visibility and metadata systems prioritise:
- semantic clarity
- deterministic semantics
- provenance preservation
- explicit attribute roles
- separation of concerns

The architecture intentionally avoids:
- conflating visibility with truth
- hidden access semantics
- implicit publication rules
- contaminating semantic identity

---

## Future Expansion

Future metadata capabilities may include:
- role-based visibility policies
- audience targeting
- semantic publication workflows
- editorial review states
- temporal visibility rules
- provenance-aware access control
- derived visibility semantics

However, metadata handling is intended to remain:
- explicit
- provenance-aware
- application-neutral
- semantically separated