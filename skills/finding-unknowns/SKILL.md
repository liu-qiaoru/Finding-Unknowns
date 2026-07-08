---
name: finding-unknowns
description: Use when starting or steering complex AI-assisted work with ambiguous requirements, unfamiliar code or domains, unclear success criteria, subjective taste, hidden constraints, long-horizon coding, product/design work, or when a model may need to make assumptions.
---

# Finding Unknowns

## Overview

Use this skill to turn vague intent into workable context before, during, and after AI-assisted work. The core idea: the prompt is the map; the real codebase, domain, user needs, and constraints are the territory; the gap between them is the set of unknowns to discover.

## Unknowns Model

Classify uncertainty before acting:

- **Known knowns:** facts, goals, and constraints already stated.
- **Known unknowns:** open questions the user knows are unresolved.
- **Unknown knowns:** taste, judgment, or standards the user can recognize but has not verbalized.
- **Unknown unknowns:** risks, constraints, conventions, or options neither the user nor agent has surfaced.

## Workflow

1. **Restate the map and territory.**
   Identify what the user gave you, where the work must actually happen, and what constraints might live outside the prompt.

2. **Run a blind-spot pass when the area is unfamiliar.**
   Search or inspect the relevant code/domain/context, then list likely unknown unknowns. Explain why each could change the work.

3. **Expose unknown knowns with artifacts.**
   When success is subjective or hard to verbalize, create lightweight options first: prototypes, sketches, mock HTML, alternative designs, sample outputs, or comparison tables. Ask the user to react before committing to expensive implementation.

4. **Interview only where answers change direction.**
   Ask one concise question at a time. Prioritize questions that would alter architecture, data models, user experience, scope, or integration strategy. If a question would only tweak wording or small styling, make a conservative assumption and log it.

5. **Use references when language is insufficient.**
   Ask for or inspect source code, existing components, prior docs, screenshots, competitor examples, or libraries that embody the desired behavior. Source code is usually the richest reference.

6. **Write an implementation plan before major work.**
   Lead with decisions the user may want to change: data model, public API, UX flow, migration path, risk, and testing approach. Put mechanical refactors and obvious steps later.

7. **Track implementation discoveries.**
   For long tasks, maintain temporary notes such as `implementation-notes.md`. Record deviations, assumptions, edge cases, and conservative choices so the next iteration can learn from them.

8. **Close the loop after implementation.**
   Produce a short explainer for reviewers: what changed, why, remaining assumptions, risks handled, and how to verify. For complex changes, quiz the user or yourself on behavior before calling the work ready.

## Prompt Patterns

Use these as compact templates:

```text
Do a blind-spot pass before implementation. I know [context], but I may be missing hidden constraints in [codebase/domain]. Find my relevant unknown unknowns and help me prompt you better.
```

```text
Before wiring anything up, create [N] lightweight alternatives for [feature/output] so I can react to the direction. Optimize for exposing tradeoffs and assumptions.
```

```text
Interview me one question at a time. Prioritize questions where my answer would change architecture, UX, data model, scope, or integration strategy.
```

```text
Read [reference path/link/module]. Recreate the same semantics/style/behavior for [target], and call out any assumptions where the reference does not map cleanly.
```

```text
Write an implementation plan. Lead with decisions I may want to tweak, then list risks, tests, and only then the mechanical steps.
```

```text
Keep implementation notes. If you deviate from the plan because of an edge case, choose the conservative path, log it under Deviations, and keep going.
```

## Output Contract

When using this skill, produce one of these useful artifacts instead of a generic discussion:

- **Unknowns brief:** knowns, unknowns, blind spots, recommended next questions.
- **Prototype set:** several cheap options for subjective choices.
- **Interview:** one high-leverage question at a time.
- **Implementation plan:** changeable decisions first, mechanical work last.
- **Implementation notes:** assumptions, deviations, edge cases, decisions.
- **Reviewer explainer:** concise handoff with verification and residual risk.

## Common Mistakes

- Treating a longer prompt as sufficient context. Longer maps can still miss the territory.
- Asking many questions before inspecting available code or references.
- Implementing subjective work before giving the user something to react to.
- Hiding assumptions in the final answer instead of recording them while they are made.
- Over-constraining the model so it follows a plan even after discovering the plan is wrong.
