# What moving to dbt actually changes

The comparison gets framed wrong from the start.

You have a Python pipeline and someone says dbt is just SQL with version control. So the conversation becomes about language preference. Python people stay. SQL people switch.

That's not what's happening.

---

## What people think today

The pitch sounds like this: dbt forces you to write modular SQL, gives you a dependency graph, adds tests. If you're already doing that in Python — with Pandas, type-checked DataFrames, unit tests — the value proposition doesn't really land.

"I already have modular code. I already have tests. Why rewrite everything?"

It's a reasonable question. It's aimed at the wrong thing.

---

## Why that thinking is incomplete

The language isn't the variable. The location is.

A Pandas pipeline pulls data from the warehouse to your machine, transforms it in memory, and writes the result back. Every `pd.read_sql()` is a data transfer. Every DataFrame is an in-memory object that only exists while the process runs.

When the pipeline fails at step 4, the DataFrames from steps 1, 2, and 3 died with the process. To debug, you re-run everything — same transfers, same wait, same starting from scratch.

And more fundamentally: your machine's memory is the ceiling. When the data grows past what fits in RAM, the pipeline breaks. Not because the logic is wrong. Because the wrong machine is doing the work.

---

## A clearer way to think about it

dbt moves the computation. The SQL runs inside the warehouse — where the data already lives, using the warehouse's compute and memory, not yours.

This isn't a syntax preference. It's a different architecture. Data doesn't travel to your machine. Computation happens at scale. Intermediate steps are real, persistent tables — not in-memory objects that vanish when the process ends.

The migration from Pandas to dbt isn't about rewriting logic in SQL. The logic is almost identical. What changes is where it runs — and what it leaves behind.

---

## Why this matters

**Practically:** a Pandas pipeline that handles 100MB today will fail at 10GB — not because the code is wrong, but because your machine doesn't have that much RAM. A dbt model that handles 100MB will handle 10TB without a code change. The warehouse scales. Your machine doesn't.

**Architecturally:** when computation lives in Python, you're managing two systems: the warehouse for storage, your machine for transformation. When it lives in dbt, you're managing one. Every intermediate step is a real table. Every table is inspectable. Every failure leaves evidence.

**Culturally:** when other teams can query your intermediate tables, they stop asking "what does this script do?" and start looking. The transformation becomes legible without a meeting.

---

## The thing worth carrying forward

Before you pick a tool, ask: *where should this computation actually run?*

If the answer is "in the warehouse, where the data lives" — use SQL. Not because SQL is better, but because running compute where the data already is tends to be the simpler architecture.

If the answer is genuinely "on a separate machine, with libraries the warehouse doesn't have" — use Python. Just be clear you're choosing a different architecture, not just a different syntax.

The Python vs SQL debate is a proxy for a location debate. Once you see it that way, the answer is usually obvious.

---

[Read the interactive version →](index.html)
