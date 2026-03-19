# ralph-t

`ralph-t` is an experiment repo for building a service in `ralphthon` using a `Ralph-loop` harness driven by coding agents. This README documents the development method and operating loop. It does not describe the product itself in depth.

## Separation Of Concerns

- `Branch`
  - The target service being built.
  - Product definition, UX intent, and domain decisions belong in `guides/`.
- `Ralph-loop`
  - The development method used to build the service.
  - Task framing, agent execution, verification, logging, and iteration rules belong in the harness.
- `ralphthon`
  - The runtime context where the coding-agent loop is executed.

These are different layers and should not be mixed in the same document or workflow rule.

## Target Service

The current target service is `Branch`. In this repository, `Branch` is treated as the build target only. The source of truth for the service remains the guide documents:

- `guides/2026-03-19-branch-open-possibility-design.md`
- `guides/2026-03-19-branch-open-possibility-options.md`

## Ralph-loop Objective

The purpose of Ralph-loop is to make coding-agent development repeatable, reviewable, and accumulative.

- Turn a product direction into a bounded implementation task.
- Run a coding agent against that task with explicit constraints.
- Verify the resulting code with tests and evaluation checks.
- Capture the artifacts so the next loop starts from evidence, not memory.

The main question here is not "how should Branch work?" but "how do we reliably keep building Branch with agent-only implementation loops?"

## Recommended Harness Layout

The repository currently has product guides only. To run Ralph-loop cleanly, the repo should grow into something like this:

```text
guides/      product documents and decision records
tasks/       loop-sized implementation tasks
prompts/     agent instructions and run templates
fixtures/    reproducible inputs for local runs
evals/       tests, rubrics, and acceptance checks
runs/        per-loop outputs and execution snapshots
artifacts/   diffs, summaries, and failure captures
logs/        operator notes and loop decisions
```

The key rule is simple: product intent lives in `guides/`, while loop execution evidence lives in the harness directories.

## Ralph-loop Execution Cycle

1. `task framing`
   - Pick one bounded task from the current product direction.
   - Write acceptance criteria and constraints in a machine-usable form.
2. `agent run`
   - Run the coding agent in `ralphthon` against that task.
   - Require code changes, not just analysis.
3. `verification`
   - Run tests, lint checks, smoke checks, or structured evals.
   - Treat failed verification as a loop result, not as missing output.
4. `artifact capture`
   - Save the diff, verification results, known risks, and next-step note.
5. `loop review`
   - Decide whether to accept, retry, narrow the task, or escalate to a human decision.

Each loop should end with enough evidence that the next loop can start without reconstructing context from chat history.

## Operating Rules

- One loop should target one main implementation outcome.
- Product docs and harness docs should be updated for different reasons, not by habit.
- Every loop should leave behind:
  - changed files
  - verification results
  - unresolved risks
  - next-loop recommendation
- Failed loops should still be logged.
- Commits should follow loop boundaries, not arbitrary chat boundaries.
- Human input should stay at the control layer:
  - choose goals
  - approve direction changes
  - review risky tradeoffs
- Direct human coding should be avoided if the purpose of the experiment is to test coding-agent-only development.

## What Success Looks Like

This repo is successful if:

- a new loop can start from stored artifacts instead of implicit memory
- agent outputs can be compared across runs
- regressions are caught by verification rather than intuition
- the service continues to move forward through small, repeatable agent-driven increments

## Current State

Right now, this repository is still at the setup stage. The product-side guides exist, but the Ralph-loop harness itself is not yet scaffolded. The next practical step is to add the loop directories and define the first task, prompt, and verification format.
