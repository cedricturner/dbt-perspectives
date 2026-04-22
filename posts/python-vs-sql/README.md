# Python or SQL is the wrong question

Every few years the debate resurfaces. Python is more expressive. SQL is more readable. Teams pick sides, and the actual question gets missed.

---

## What people think today

The framing is almost always about language capability. What does your team know? What does your data require? Python can do things SQL can't — complex loops, ML models, arbitrary libraries. The comparison is about expressiveness.

This is a reasonable starting point. It's also asking the wrong question.

---

## Why that thinking is incomplete

The language isn't the variable. The location is.

When you write a Python transformation, computation runs on a machine. The data travels from the warehouse to that machine, gets processed in memory, and the result travels back. The machine's resources are the constraint.

When you write a SQL transformation in dbt, computation runs inside the warehouse. The data doesn't move. The warehouse's resources handle it. Those resources scale with the data, not with your machine.

At small scale, this doesn't matter. At large scale, it becomes the whole problem.

---

## A clearer way to think about it

Think of it as two different architectures, not two different languages.

**Compute-near-machine:** data travels to your code. Memory is the ceiling. Works well for ML, complex iteration, operations that genuinely can't be expressed in SQL.

**Compute-in-warehouse:** your code travels to the data. Scale is handled by the warehouse. Works well for anything that's a set operation — which is most of what data transformation actually is.

The language you write in is secondary. The question is whether computation happens where the data lives, or whether data has to travel to where computation lives.

---

## Why this matters

**Practically:** a dbt model that processes 1GB today will process 1TB next year without a code change. A Pandas script that processes 1GB will hit RAM limits at 10GB and need to be rewritten — usually into SQL anyway.

**Operationally:** when computation lives in the warehouse, there's no transfer cost, no external process to monitor, no memory limit to manage. The warehouse has query logs and execution plans. You can debug a SQL transformation by looking at what the warehouse did. Debugging a Pandas pipeline usually means adding print statements and re-running.

**Architecturally:** the teams that struggle most with Python-based pipelines aren't struggling with the language. They're struggling with the overhead of managing an external compute layer that's separate from where the data lives.

---

## The thing worth carrying forward

Before picking a language, ask: where should this computation actually run?

If the answer is "in the warehouse, close to the data" — use SQL. Not because it's better, but because running compute where the data lives is usually the simpler architecture.

If the answer is genuinely "on a separate machine, with libraries the warehouse doesn't have" — use Python. But be clear you're choosing a different architecture, not just a different syntax.

The language debate is a proxy for a location debate. Once you see it that way, the answer is usually obvious.

---

[Read the interactive version →](index.html)
