# What moving to dbt actually changes

The comparison gets framed wrong from the start. You have a Python pipeline, you're evaluating dbt, and someone describes it as "SQL with version control." That makes it sound like a language preference — Python people stay, SQL people switch.

That's not what's actually happening.

---

## What people think today

The standard pitch goes: dbt forces you to write modular SQL, gives you a DAG, adds tests. If you're already doing that in Python — with Pandas, with type-checked DataFrames, with functions you can unit-test — then the value proposition doesn't land.

"I already have modular code. I already have tests. Why would I rewrite everything in SQL?"

This is a reasonable objection. It's also aimed at the wrong target.

---

## Why that thinking is incomplete

The language isn't what changes.

A Pandas pipeline pulls data from the warehouse to your machine, transforms it in memory, and writes the result back. Every `pd.read_sql()` is a data transfer. Every DataFrame is an in-memory object that exists only as long as the process runs.

When the pipeline fails at step 4, the DataFrames from steps 1, 2, and 3 died with the process. To debug, you re-run everything — and now you're waiting for the same data transfers all over again.

More fundamentally: your machine's memory is the constraint. When the data grows past what fits in RAM, the pipeline breaks. Not because the logic is wrong — because the wrong machine is doing the work.

---

## A clearer way to think about it

dbt moves the computation. The SQL runs inside the warehouse — where the data already lives, using the warehouse's compute and memory, not yours.

This isn't a syntax preference. It's a different architecture. The data never leaves the warehouse. The computation happens at scale. Intermediate steps are real, persistent tables — not in-memory objects that vanish when the process ends.

The migration from Pandas to dbt isn't about rewriting logic in SQL. The logic is almost identical. What changes is where that logic runs — and what it leaves behind when it finishes.

---

## Why this matters

**Practically:** a Pandas pipeline that processes 100MB today will fail when it hits 10GB — not because the code is wrong, but because your laptop doesn't have that much RAM. A dbt model that processes 100MB will process 10TB without a code change. The warehouse scales; your machine doesn't.

**Architecturally:** when computation lives in Python, you're managing two systems: the warehouse for storage and your machine for transformation. When computation lives in dbt, you're managing one: the warehouse handles both. Every intermediate step is a real table. Every table is inspectable. Every failure leaves evidence.

**Culturally:** the thing people underestimate is what changes when other teams can query your intermediate tables. They stop asking "what does this script do?" and start looking. The transformation becomes legible without a meeting.

---

## The thing worth carrying forward

When you evaluate a transformation tool, ask: *where does the computation actually run?*

If the answer is "on a machine, in memory" — your data has to travel there and back, and it has to fit. If the answer is "in the warehouse, where the data lives" — the data doesn't move, and scale is someone else's problem.

That's what the migration is actually about. The SQL vs Python debate is almost beside the point.

---

[Read the interactive version →](index.html)
