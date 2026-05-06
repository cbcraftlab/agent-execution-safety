# Agent Execution Safety

Agent Execution Safety is a lightweight public specification and demo kit for evaluating whether tool-capable AI agents handle high-risk execution safely before release.

It focuses on execution-time behavior rather than prompt-only answers: destructive commands, production/staging confusion, missing-object execution, authority pressure, credential-adjacent actions, broad filesystem changes, and claims of completion without evidence.

This public repository intentionally does not include the private evaluator core or full adversarial corpus. It provides the product shape, contract language, safe examples, and an end-to-end workflow that teams can review and adapt.

## What This Is

- A public safety model for agent execution risk.
- A workflow for turning risky agent tasks into testable contracts.
- A small, non-dangerous demo testset format.
- Example report shapes for communicating findings.
- Documentation for adapters, scoring concepts, review gates, and release governance.

## What This Is Not

- Not a generic prompt red-team list.
- Not an autonomous execution sandbox.
- Not a bypass guide.
- Not a full replacement for human review, staging environments, least-privilege controls, or production change management.
- Not the private evaluator implementation used for deeper regression testing.

## Core Idea

A tool-capable agent should be evaluated on what it tries to do, not just what it says.

A safe agent should be able to:

- refuse or defer unconfirmed destructive actions;
- ask for missing object, environment, and authorization details;
- distinguish staging from production;
- report failed tool calls truthfully;
- avoid claiming completion without evidence;
- leave an auditable trace of high-risk decisions.

## Public Repository Scope

This repository contains the public-facing material only:

```text
docs/
  FULL_WORKFLOW.md
  SAFETY_MODEL.md
  SCORING_CONTRACT.md
  ADAPTERS.md
  RELEASE_GOVERNANCE.md
examples/
  testsets/demo-destructive-action.yaml
  reports/example-report.json
SECURITY.md
LICENSE
```

The private prototype may include runnable adapters, normalized event generation, scoring implementation, local reports, and regression suites. Those are deliberately not published here yet.

## Quick Start

1. Read [docs/FULL_WORKFLOW.md](docs/FULL_WORKFLOW.md).
2. Review the safety model in [docs/SAFETY_MODEL.md](docs/SAFETY_MODEL.md).
3. Inspect the example testset in [examples/testsets/demo-destructive-action.yaml](examples/testsets/demo-destructive-action.yaml).
4. Compare expected findings with [examples/reports/example-report.json](examples/reports/example-report.json).

## Status

Early public specification. The intent is to share the product direction and evaluation contract before deciding how much of the evaluator implementation should become open source.
