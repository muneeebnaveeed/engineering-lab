# engineering-lab

A deliberate-practice repository for controlled failures — **not** a portfolio. The goal is to
break things on purpose, observe them with real tools, diagnose them, and be able to explain
the mechanism afterwards.

Selection and rationale live in the personal wiki (`reference/Engineering Lab.md`); the method
is `frameworks/Deliberate Practice Loop.md`. This repository holds the work.

This lab complements the integrated project (`career-tech/MiniPay.md`): isolate a failure mode
here, then apply the resulting judgment there.

## Layout

```text
engineering-lab/
├── README.md
├── TEMPLATE.md              # the 8-section lab writeup
├── browser/
├── javascript/
├── postgres/
├── go/
├── distributed-systems/
├── observability/
└── incidents/
```

One folder per lab inside an area, each with a `README.md` copied from `TEMPLATE.md`.

## What makes a lab finished

Every lab states: the concept, the expected behavior, the failure introduced, the tools used to
observe it, the diagnosis, the fix, the verification, and a two-minute explanation. A lab
without a **measurement before and after** is not finished — "it seems faster" is not evidence.

Write sections 4–6 while debugging. Reconstructing them afterwards produces a tidy narrative
that hides the wrong turns, and the wrong turns are the part worth keeping.

## Priority scenarios

Drawn from the wiki page, roughly in the order the timeline reaches them:

| Area | Scenarios |
|---|---|
| Browser | layout thrashing, long tasks, rendering performance |
| JavaScript | event-loop starvation, memory retention |
| PostgreSQL | N+1 queries, transaction anomalies, locks and deadlocks, query plans |
| Go | data races, goroutine leaks, connection-pool exhaustion, CPU/memory profiling |
| Distributed systems | retry storms, duplicate delivery, tail latency, partial failure |
| Observability | tracing, metrics, load testing |
| Incidents | runbooks, postmortems |

## Conventions

- One failure per lab. If two things break, that's two labs.
- Keep the reproduction as small as it can be while still failing.
- Prefer real tooling over `console.log` — profilers, `EXPLAIN ANALYZE`, `pprof`, traces.
- Record time spent. It feeds the sustainability column of the monthly dashboard.

## CI

`.github/workflows/ci.yml` runs on push and pull request. It is a skeleton: it sets up Node and
Go and runs each toolchain's tests only when that toolchain's config is present, so it passes on
an empty repository and starts doing real work as labs land. Extend it per lab rather than
building it out speculatively.
