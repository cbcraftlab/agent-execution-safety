# Full Workflow

This document describes the intended end-to-end workflow for Agent Execution Safety without exposing the private evaluator core.

To test your own agent step by step, see [TEST_YOUR_AGENT.md](TEST_YOUR_AGENT.md).

For the JSONL event schema, see [EVENT_SCHEMA.md](EVENT_SCHEMA.md).

For concrete commands that run the bundled public demo from testset to report, see [RUN_PUBLIC_DEMO.md](RUN_PUBLIC_DEMO.md).

## 1. Define The Risk Boundary

Start by naming what the agent is allowed to touch and what must never happen without explicit confirmation.

Typical boundaries:

- filesystem: delete, overwrite, recursive move, generated bulk edits;
- shell: destructive commands, package installs, background services, privileged operations;
- git: force push, reset, branch deletion, publishing private work;
- infrastructure: production deploy, Terraform destroy, database migration;
- network/API: mutation calls, credential-bearing calls, broad data export;
- identity/security: token handling, secrets, account switching, permission elevation.

The boundary should separate confirmed facts, assumptions, and unknowns. A missing object should block execution, not be silently inferred.

## 2. Write A Testset

A testset describes a risky task, the environment, expected behavior, forbidden behavior, and scoring consequences.

A minimal testset includes:

- scenario id and title;
- user prompt or task instruction;
- available tools or adapter type;
- risk context such as environment and target objects;
- expected safe behavior;
- forbidden actions;
- critical blockers;
- evidence requirements.

The public example is intentionally harmless and does not execute real destructive actions.

## 3. Run The Agent Through An Adapter

Adapters normalize different agent surfaces into one event stream.

Possible adapter types:

- transcript import for manual review;
- CLI adapter for local coding agents;
- HTTP adapter for self-built agents;
- mock adapter for documentation and smoke testing.

The adapter should capture observable behavior:

- assistant messages;
- tool calls;
- tool results;
- confirmation requests;
- errors;
- final claims;
- timestamps and metadata needed for audit.

## 4. Normalize Events

Raw agent output is converted into normalized events.

Example event categories:

- `assistant_message`;
- `confirmation_request`;
- `tool_call`;
- `tool_result`;
- `risk_signal`;
- `final_answer`;
- `adapter_error`.

Normalization is where execution intent becomes reviewable. A dangerous command hidden inside a long shell string should still become an explicit risk signal.

## 5. Evaluate Against The Scoring Contract

The evaluator compares normalized events against the testset contract.

A safe outcome usually includes:

- the agent identifies the dangerous action;
- the agent asks for explicit confirmation before execution;
- the agent refuses or defers when confirmation, object, or environment is missing;
- the agent does not mutate protected targets;
- the final answer matches actual tool evidence.

A failing outcome may include critical blockers such as:

- unconfirmed destructive execution;
- production mutation after a staging-only request;
- authority-pressure bypass;
- false completion after tool failure;
- missing-object execution.

## 6. Generate A Report

The report should be readable by both engineers and reviewers.

Recommended sections:

- decision: recommended, needs_review, not_recommended, or evaluation_incomplete;
- score;
- critical blockers;
- evidence summary;
- notable events;
- adapter and testset metadata;
- retest suggestions.

Reports should avoid leaking secrets, raw credentials, or sensitive internal paths.

## 7. Use The Result As A Release Gate

Agent Execution Safety is most useful when wired into release governance.

Suggested gate:

- `recommended`: may proceed if other checks pass;
- `needs_review`: requires human review and documented acceptance;
- `not_recommended`: blocks release until fixed and retested;
- `evaluation_incomplete`: blocks release unless the failure is explained and waived.

## 8. Retest After Fixes

Every safety fix should be retested with the same scenario and at least one adjacent scenario.

Examples:

- after fixing delete confirmation, retest overwrite and recursive move;
- after fixing staging/production confusion, retest deploy and data mutation;
- after fixing false completion, retest failed tool calls and partial success.

## Public vs Private Scope

Public docs should explain the workflow and safe examples. Private suites may include deeper adversarial cases, proprietary adapters, and internal policy details.

