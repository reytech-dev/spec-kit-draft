---
description: Draft clarified feature specification input text for speckit.specify without creating files.
---

## User Input

```text
$ARGUMENTS
```

You **MUST** consider the user input before proceeding. If the input is empty,
ask the user for a short description of the feature they want to specify.

## Purpose

Create polished, clarified flow text that the user can pass directly to
`/speckit.specify`. This command is a drafting helper only. It must not create a
feature directory, write a Speckit `spec.md`, run Speckit scripts, or modify any
project files.

## Optional Design Context

Before drafting, check whether this file exists:

```text
designs/design-processing/specify-context.md
```

If it exists:

1. Read it as normative project design context.
2. Preserve this command's implementation-neutral behavior.
3. Use design context to improve the feature draft only when it affects observable product behavior or downstream specification quality.
4. Include design-driven constraints when they affect:
   - user-visible flows
   - required states
   - interaction behavior
   - accessibility
   - localization
   - responsive behavior
   - content structure
   - acceptance criteria
5. Treat warnings in the design context as possible clarification candidates.
6. If design context conflicts with explicit user input, prefer the user input.
7. Record non-blocking design deviations as assumptions.

Do not copy low-level implementation details into the final draft unless they define the product contract.

Avoid including:

- component names
- token names
- CSS classes
- file paths
- framework names
- GraphQL operation names
- database tables

## Outline

Given the feature idea from the user input, do this:

1. **Extract the feature intent**:
   - Identify the primary user-visible outcome.
   - Identify the actors or roles involved.
   - Identify the core actions users need to perform.
   - Identify important data, lifecycle, permissions, and constraints.
   - Identify explicit non-goals or scope boundaries if provided.
   - Incorporate applicable user-visible constraints from `designs/design-processing/specify-context.md` when present.

2. **Check for material ambiguity**:
   Ask clarification questions only when the answer would materially change
   product scope, user experience, privacy/security behavior, data ownership,
   acceptance scenarios, or downstream planning.

   Prioritize questions in this order:
   - Scope and user roles
   - Security, privacy, permissions, or data visibility
   - Critical user flow and navigation behavior
   - Data persistence and lifecycle
   - Error, empty, loading, and retry behavior
   - Localization, accessibility, and responsiveness
   - Success criteria and measurable outcomes
   - Warnings or conflicts from the Open Design context, when present

   Do not ask about implementation details unless they directly affect the
   feature contract. Use sensible assumptions for low-impact gaps and record
   those assumptions in the final response.

3. **Ask questions interactively when needed**:
   - Ask concise, targeted questions.
   - Prefer multiple-choice questions with a recommended option when there are
     clear tradeoffs.
   - Allow a custom answer when appropriate.
   - Ask related questions together when that reduces back-and-forth.
   - Stop asking when the remaining uncertainty is low-impact or better suited
     for `/speckit.clarify` after the first formal specification exists.

4. **Draft the final flow text**:
   Produce a single coherent plain-language feature description suitable as
   input for `/speckit.specify`. The text should be understandable to
   non-technical stakeholders and should focus on observable behavior, not code
   architecture.

   Include these aspects when relevant:
   - User outcome
   - Actors and permissions
   - Primary user journeys
   - Direct URL or navigation behavior
   - Normal, loading, empty, success, error, retry, unavailable, and unauthorized
     states
   - Data ownership, persistence expectations, and external dependencies
   - Privacy and security constraints
   - Accessibility, localization, and responsive behavior
   - Edge cases
   - Success criteria
   - Relevant design-context constraints that affect observable behavior
   - Explicit out-of-scope items

5. **Keep the draft implementation-neutral**:
   - Do not specify frameworks, component names, database tables, GraphQL
     operation names, file paths, or test files unless the user explicitly
     requests them or they are part of the product contract.
   - It is acceptable to mention existing systems at a product-contract level,
     such as "reuse the existing contact flow" or "use the existing API-defined
     matching rules".
   - Do not include Open Design component names, token names, CSS classes, or
     generated artifact paths unless they define the user-visible contract.

## Output Format

When ready, respond with:

1. A short note indicating whether any important assumptions remain.
2. A fenced `text` block containing only the final flow text to pass to
   `/speckit.specify`.

If unresolved questions remain that are too important to assume, ask those
questions instead of producing the final flow text.

## Quality Checklist

Before returning the final draft, verify internally that:

- The draft describes user value and observable behavior.
- The draft can be used directly as `/speckit.specify` input.
- Critical roles, permissions, and privacy rules are clear.
- Primary flows and important alternate states are covered.
- Success criteria are included and are measurable or directly verifiable.
- Implementation details are avoided unless they define the product contract.
- Any assumptions are explicit and non-blocking.