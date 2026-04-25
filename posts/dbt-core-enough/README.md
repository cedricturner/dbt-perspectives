# Data teams don't have a quality problem. They have a trust problem.

The reflex is to add more tests. When a pipeline produces a wrong number, the answer is: write assertions, add checks, expand coverage.

It's not a wrong instinct. It's aimed at the wrong problem.

---

## What people think today

The pitch for data quality tooling usually goes: if the data fails a test, you know it's broken. If everything passes, you can trust it.

This treats trust as a function of test coverage. More tests → higher coverage → more trust. Clean model. Also doesn't explain why teams with comprehensive test suites still rebuild the same model five times.

---

## Why that thinking is incomplete

Tests tell you *when* something broke. They don't tell you *what happened* — how the data was shaped at each step, whether the logic is doing what you think, whether the output means what the analyst assumes it means.

A test is binary: pass or fail. Trust is built on legibility. Can I look at what this pipeline did and understand it?

Here's the classic symptom. Two teams independently built a "revenue" model. Both pass their tests. Neither team trusts the other's number. They schedule a meeting to align on definitions, and six weeks later the question is still open. That's not a quality problem. It's a visibility problem.

When a pipeline is opaque — when intermediate steps vanish, when logic is buried in a script — people stop building on top of it and start building around it. Tests don't fix that. The pipeline was already passing its tests.

---

## A clearer way to think about it

Trust comes from legibility. Legibility comes from visibility.

When every intermediate step is a real, persistent table — when `stg_orders` and `int_orders_with_payments` exist in the warehouse after the run finishes — other people can query them. They can check their assumptions. They can trace a discrepancy without scheduling a call.

This is the thing dbt does that tests don't. Tests verify correctness. Persistent intermediate tables make the pipeline *inspectable*. Those are different capabilities, and they solve different problems.

---

## Why this matters

**Practically:** when a metric looks off, the answer isn't "the tests passed, so it's fine." It's "let me query `int_orders` and see what's there." The difference is 40 minutes of re-running versus a two-line SELECT.

**Culturally:** most data teams don't rebuild because the platform is unreliable. They rebuild because they can't see inside it. "I trust it" usually means "I built it." When intermediate steps are visible and queryable, trust can transfer — you can build on someone else's model because you can inspect what it actually does.

**Organizationally:** the "five versions of revenue" problem isn't really a definition problem. It's a visibility problem. When there's one canonical `stg_orders` that everyone references — and it's sitting in the warehouse for anyone to query — the debate ends. Not because someone won the meeting. Because there's only one place to look.

---

## The thing worth carrying forward

When you evaluate your data platform, don't just ask whether it has tests. Ask whether it makes the pipeline visible.

Tests prevent bad data from propagating. Visibility prevents teams from duplicating each other's work, losing trust in shared infrastructure, and reverting to their own scripts.

The trust problem is almost never about the data being wrong. It's about not being able to tell.

---

[Read the interactive version →](index.html)
