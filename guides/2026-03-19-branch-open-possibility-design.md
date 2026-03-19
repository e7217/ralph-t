# Branch: Open Possibility Design

Date: 2026-03-19
Status: Approved design summary

## Product Thesis

Branch is not a planner that recommends one correct route.
Branch is a possibility map that reduces post-choice anxiety by showing that a user's current choice does not fully close their future.

The core promise is:

`Your choice does not close the future. There are still open possibilities.`

## Problem

Most planning tools assume a single optimal path.
That framing increases anxiety after a decision is made because users feel that a wrong turn has permanently closed other futures.

Branch should instead help users feel three things:

- recovery is possible
- convergence is possible
- unconsidered directions still exist

## Product Definition

Branch generates a dynamic possibility graph around a goal.
It does not rely on three fixed path types.
The system may generate many routes, each with its own strategy, tone, tradeoffs, and points of connection.

The primary job is not ranking routes.
The primary job is making remaining possibilities visible after a choice.

## Core UX Principle

Use a `map-first, route-second` experience.

- First show a possibility landscape, not a single detailed route
- Present 4-7 strategic directions at a high level
- Expand one direction into route detail only after user selection
- Keep other directions faintly visible after selection
- Always show recovery, convergence, and alternative openings

This preserves the feeling that the future remains open.

## User Experience Flow

1. User enters a goal.
2. AI generates a possibility landscape with multiple directions.
3. The initial screen shows direction cards plus lightweight visual connections.
4. The user opens one direction.
5. The selected direction expands into a detailed route graph.
6. Other directions remain visible in reduced emphasis.
7. The system highlights:
   - recovery paths
   - convergence points
   - newly opened directions

## Interaction Priorities After Selection

When a user selects a direction, the interface should answer these questions in order:

1. If this goes badly, where can I recover?
2. Where do I meet other viable routes again?
3. What other direction is still available from here?

This means the post-selection view is not a results screen.
It is evidence that possibility remains.

## Information Model

Recommended top-level entities:

- `directions[]`: strategic direction clusters created dynamically by AI
- `routes[]`: concrete route variants inside a direction
- `nodes[]`: steps, states, or milestones
- `connections[]`: meaningful relationships between nodes or routes

`connections[]` matter most and should carry meaning such as:

- `progress`
- `merge`
- `switch`
- `recovery`
- `emergent`

Branch should emphasize the meaning of transitions, not just the existence of steps.

## Layout Recommendation

Use a three-part layout:

- center: possibility graph
- left: available directions
- right: reassurance panel

The right panel is not just a detail panel.
It should consistently explain:

- what this choice does not close
- where recovery remains possible
- where convergence happens
- what other direction may still open later
- what small next action can be taken now

## AI Output Rules

The AI should behave like a possibility interpreter, not a certainty engine.

- do not rank one route as the correct answer
- use conditional language, not deterministic language
- explain openings before risks
- give reasons, not vague reassurance
- treat all routes as hypotheses, not promises

Preferred language patterns:

- this choice does not close other possibilities
- you may still rejoin another direction later
- if this slows down, recovery remains possible here
- another direction can open from this point

Avoid language such as:

- this is the best route
- this is the correct choice
- this is your optimal plan

## Reliability and Failure Handling

Branch must fail honestly.
The product should never present weak AI output as false certainty.

Guardrails:

- validate generated directions for diversity and coherence
- reject outputs with isolated dead ends and no meaningful connections
- reject outputs that implicitly rank a single best route
- degrade gracefully from detailed route graph to simpler direction map
- keep the core message intact even when detail quality is low

Persistent trust message:

`This map is not a prediction of the one right answer. It is an interpretation of still-open possibilities.`

## Non-Goals

- ranking one best path
- forcing exactly three route archetypes
- pretending to predict the future with certainty
- hiding alternative directions after a user selects one

## Summary

Branch should evolve from a fixed multi-path planner into an open possibility map.
Its distinguishing feature is not the number of routes it generates.
Its distinguishing feature is that it reduces post-choice anxiety by making recovery, convergence, and unexplored directions visible.
