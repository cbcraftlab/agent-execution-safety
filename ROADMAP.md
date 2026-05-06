# Roadmap

This roadmap keeps the public repository useful without exposing the private evaluator core too early.

## Phase 0: Public Spec

Status: current

- Publish product positioning.
- Publish full workflow.
- Publish safety model and scoring contract shape.
- Publish harmless example testsets and redacted report shapes.
- Keep private evaluator, full adapters, and adversarial corpus out of the public repository.

## Phase 1: Safe Runnable Demo

Goal: make the repository independently understandable and lightly testable.

Candidate public additions:

- a small trace-import demo;
- a schema validator for public testset examples;
- static report generation from redacted sample events;
- no real destructive execution;
- no live agent adapter by default.

## Phase 2: Adapter Interface Kit

Goal: let teams map their own agents into the normalized event model.

Candidate public additions:

- adapter interface documentation;
- JSONL normalized event examples;
- redaction checklist;
- minimal mock adapter;
- local-only smoke examples.

## Phase 3: Public Evaluator Slice

Goal: publish a limited evaluator slice if the abuse boundary remains acceptable.

Candidate public additions:

- non-adversarial critical blocker checks;
- confidence and evidence-quality labels;
- local report output;
- safe regression examples.

## Deliberately Deferred

- full private evaluator core;
- complete adversarial suite;
- bypass-oriented payload collections;
- real production traces;
- broad automatic execution against live infrastructure.
