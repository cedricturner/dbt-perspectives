# dbt perspectives

Not documentation. Not tutorials.

A collection of perspectives on what dbt actually changes — for teams, for pipelines, and for the way data organizations work.

**Live site → [cedricturner.github.io/dbt-perspectives](https://cedricturner.github.io/dbt-perspectives/)**

---

## Posts

Each post is a scrolling narrative page with interactive visuals. Read the essay (README) or open the interactive version.

| Post | Interactive | Essay |
|------|-------------|-------|
| **The stored procedure is not your enemy** | [↗ open](https://cedricturner.github.io/dbt-perspectives/posts/stored-procedures/) | [README](posts/stored-procedures/README.md) |
| **What moving to dbt actually changes** | [↗ open](https://cedricturner.github.io/dbt-perspectives/posts/scripts/) | [README](posts/scripts/README.md) |
| **Data teams don't have a quality problem. They have a trust problem.** | [↗ open](https://cedricturner.github.io/dbt-perspectives/posts/trust-problem/) | [README](posts/trust-problem/README.md) |
| **Python or SQL is the wrong question** | [↗ open](https://cedricturner.github.io/dbt-perspectives/posts/python-vs-sql/) | [README](posts/python-vs-sql/README.md) |

---

## What each post argues

**[The stored procedure is not your enemy](https://cedricturner.github.io/dbt-perspectives/posts/stored-procedures/)**
The real problem isn't the technology. It's that your pipeline was designed to execute — not to be inspected. Stored procedure → dbt is an execution model change, not a code quality cleanup.

**[What moving to dbt actually changes](https://cedricturner.github.io/dbt-perspectives/posts/scripts/)**
Not the SQL syntax, version control, or modular files. Computation moves from your machine to the warehouse — and that changes scale, parallelism, and what survives a failure.

**[Data teams don't have a quality problem. They have a trust problem.](https://cedricturner.github.io/dbt-perspectives/posts/trust-problem/)**
Tests tell you when something broke. They don't make the pipeline legible. Most teams rebuild the same model five times not because the first was broken, but because they couldn't tell whether it was right.

**[Python or SQL is the wrong question](https://cedricturner.github.io/dbt-perspectives/posts/python-vs-sql/)**
The language doesn't matter. Where the computation runs does. Run compute where the data lives unless you have a specific reason not to.

---

## About

I'm a Solutions Architect with a background in data engineering, moving toward product and technical marketing.

My interest is in how technical systems get adopted — or don't — and why the gap between "this works" and "this gets used" is usually a visibility problem, not a capability problem.
