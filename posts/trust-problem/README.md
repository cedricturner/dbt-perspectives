# Data teams don't have a quality problem. They have a trust problem.

The reflex is to add tests. When a data pipeline produces a wrong number, the answer is: write more tests, add more assertions, expand coverage. It's an engineering instinct — and it's not wrong, exactly. It's just aimed at a different problem.

---

## What people think today

The pitch for data quality tooling usually goes like this: if the data fails a test, you know it's broken. If everything passes, you can trust it.

This frames trust as a function of test coverage. More tests → higher coverage → more trust. It's a clean model. It also doesn't explain why teams with comprehensive test suites still rebuild the same model five times.

---

## Why that thinking is incomplete

Tests tell you *when* something broke. They don't tell you *what happened* — how the data was shaped at each step, whether the logic is doing what you think it's doing, whether the output means what the analyst assumes it means.

A test is a binary: pass or fail. Trust is built on legibility — can I look at what this did and understand it?

The canonical symptom: two teams independently built a "revenue" model. Both models pass their tests. Neither team trusts the other's number. They schedule a meeting to align on definitions, and six weeks later the question is still open. The problem wasn't quality. It was that neither team could see inside the other's pipeline.

When a pipeline is opaque — when intermediate steps vanish, when the logic is buried in a script someone else wrote — people stop building on top of it and start building around it. Tests didn't help. The pipeline already passed its tests.

---

## A clearer way to think about it

Trust comes from legibility. Legibility comes from visibility.

When every intermediate step is a real, persistent table — when `stg_orders` and `int_orders_with_payments` exist in the warehouse after the run completes — other people can query them. They can compare them against their assumptions. They can trace where a discrepancy came from without asking you to add a debug log and re-run.

This is the thing dbt does that tests don't. Tests verify correctness. Persistent intermediate tables make the pipeline *inspectable*. Those are different capabilities, and they solve different problems.

---

## Why this matters

**Practically:** when a metric looks off, the answer isn't "the tests passed, so it's fine." The answer is "let me query `int_orders` and see what's there." The difference between those two responses is 40 minutes of re-running versus a two-line SELECT.

**Culturally:** most data teams don't rebuild because the platform is unreliable. They rebuild because they can't see inside it. "I trust it" usually means "I built it." When the intermediate steps are visible and queryable, trust can transfer — you can build on someone else's model because you can inspect what it actually does.

**Organizationally:** the "five versions of revenue" problem isn't a definition problem. It's a visibility problem. When there's one canonical `stg_orders` that everyone references — and when that table is sitting in the warehouse for anyone to query — the definition debate ends. Not because someone won the meeting, but because there's only one place to look.

---

## The thing worth carrying forward

When you evaluate your data platform, don't just ask whether it has tests. Ask whether it makes the pipeline visible.

Tests prevent bad data from propagating. Visibility prevents teams from duplicating each other's work, losing trust in shared infrastructure, and reverting to their own scripts. Both matter. They solve different problems.

The trust problem is almost never about the data being wrong. It's about not being able to tell.

---

[Read the interactive version →](index.html)
