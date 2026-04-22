# Python or SQL is the wrong question

Every few years, the debate resurfaces. Python is more expressive. SQL is more readable. Python has better libraries. SQL is closer to the data. Teams pick sides, adopt tooling based on preference, and largely miss the variable that actually matters.

---

## What people think today

The framing is almost always about language capability. Python can do things SQL can't — complex loops, ML models, arbitrary libraries. SQL can do things Python can't — or at least can do them more concisely. The conversation becomes: what does your team know, and what does your data require?

This is a reasonable starting point. It's also asking the wrong question.

---

## Why that thinking is incomplete

The language isn't the variable. The location is.

When you write a Python transformation, the computation runs on a machine — usually yours, or a container somewhere. The data travels from the warehouse to that machine, gets processed in memory, and the result travels back. The machine's resources are the constraint: memory for DataFrames, CPU for computation, network for the transfers.

When you write a SQL transformation (in dbt or otherwise), the computation runs inside the warehouse. The data doesn't move. The warehouse's resources handle it — and those resources scale with the data, not with your machine.

At small scale, this doesn't matter. A 100MB dataset fits in RAM. Python and SQL both work fine. At large scale — millions of rows, terabytes — the difference becomes structural. A Pandas pipeline that works locally breaks in production not because the logic is wrong, but because the wrong machine is doing the work.

---

## A clearer way to think about it

Think of it as two different architectures, not two different languages.

**Compute-near-machine:** data travels to your code. You control the execution environment. Memory is the limit. Works well for ML, complex iteration, operations that genuinely can't be expressed in SQL.

**Compute-in-warehouse:** your code travels to the data. The warehouse controls execution. Scale is handled for you. Works well for anything that can be expressed as a set operation — which is most of what data transformation actually is.

The language you write in is secondary. The question is whether the computation happens where the data lives, or whether the data has to travel to where the computation lives.

---

## Why this matters

**Practically:** a dbt model that processes 1GB today will process 1TB next year without a code change. You may pay more for warehouse compute, but you don't rewrite the pipeline. A Pandas script that processes 1GB will hit RAM limits at 10GB and need to be rewritten with chunking, Dask, Spark, or a warehouse query — which is often just SQL.

**Operationally:** when computation lives in the warehouse, the data never leaves. There's no transfer cost, no latency for pulling rows down, no external process to monitor. The warehouse has a job history, query logs, execution plans. You can debug a SQL transformation by looking at what the warehouse did. You can debug a Pandas pipeline by reconstructing what happened in memory — which usually means adding print statements and re-running.

**Architecturally:** the teams that struggle most with Python-based pipelines aren't struggling with the language. They're struggling with the overhead of managing an external compute layer — containers that go down, memory limits that change with data volume, intermediate state that vanishes when a process exits.

---

## The thing worth carrying forward

Before choosing between Python and SQL, ask: where should this computation actually run?

If the answer is "in the warehouse, close to the data" — use SQL. Not because SQL is better, but because running compute where the data lives is almost always the simpler architecture.

If the answer is genuinely "on a separate machine, with libraries the warehouse doesn't have" — use Python. Just be clear that you're choosing a different architecture, not a different syntax.

The language debate is a proxy for a location debate. Once you see it that way, the answer is usually obvious.

---

[Read the interactive version →](index.html)
