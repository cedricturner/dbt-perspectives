# The stored procedure is not your enemy

Stored procedures work. That's kind of the whole problem.

When teams migrate to dbt, they usually frame it as a modernization. Better SQL. Version control. Modular files. Tests. That framing is accurate — but it misses the actual change.

The migration isn't about how you write SQL. It's about what your pipeline leaves behind when it runs.

---

## What people think today

The standard pitch goes something like this: your stored proc is buried in one big file, hardcoded with schema names, impossible to test or parallelize. dbt breaks it into modular files with clear dependencies, puts it in Git, gives you lineage you can visualize.

All of that is true. But it frames the problem as organizational — messy code that needs cleanup.

The actual problem is architectural.

---

## Why that thinking is incomplete

Here's what a stored procedure actually does at runtime.

It creates temp tables, runs data through a series of steps, produces a final output, and ends. When the session ends, those temp tables disappear. The intermediate work is gone.

If it fails at step 4, everything from steps 1, 2, and 3 is gone. To debug, you re-run the whole thing from the top — adding print statements, adding debug tables, trying to reconstruct what happened.

The pipeline runs. The pipeline ends. Nothing survives.

And that's not just an inconvenience. Over time it creates distrust. When you can't see what happened — when every failure starts from zero — you stop trusting the pipeline. You start working around it instead.

---

## A clearer way to think about it

dbt models are real tables in your warehouse. Not temp tables. Not session-scoped state. Actual tables that exist after the run finishes, whether it succeeded or failed.

When a dbt run fails at step 4, steps 1, 2, and 3 are still sitting in your warehouse. You can query them. You can see exactly what state the data was in when the failure happened. You can re-run just the model that failed.

The shift is from *execution* to *artifacts*.

A stored procedure executes and disappears. A set of dbt models executes and leaves evidence. Every step is a table. Every table is a checkpoint. The whole thing is inspectable by design.

There's a second thing that follows. Because each model is a real, standalone table, it can be referenced by other teams. When someone needs clean orders, they point to `ref('stg_orders')` instead of copying the logic into their own procedure. The definition lives in one place. It can't drift.

---

## Why this matters

**Practically:** debugging becomes inspection instead of archaeology. At 3am, the difference between "re-run everything from scratch" and "query the intermediate table and see where it went wrong" is the difference between 45 minutes and 5 minutes. Multiplied across a team and a year, that's a lot of time recovered.

**Culturally:** when the pipeline leaves artifacts, people start trusting it — not because it breaks less, but because when it breaks, you can see what happened. Most data teams don't rebuild because the platform is unreliable. They rebuild because they can't see inside it.

---

## The thing worth carrying forward

When you evaluate any data pipeline, ask: *what does it leave behind when it runs?*

If the answer is just the final output — you're one failure away from starting over blind. If the answer is every intermediate step as a queryable table — you're debugging from evidence instead of memory.

That's what the stored procedure migration is actually about. The SQL syntax is almost beside the point.

---

[Read the interactive version →](index.html)
