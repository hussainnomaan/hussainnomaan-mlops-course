# Week 03 Lab

## Reflection

The bad-status error (LATITUDE=999) was easiest to trigger — just an invalid
input value, no environment tricks needed. The connection error was hardest
since I had to make up a URL that reliably fails to resolve.

Exponential backoff doubled the wait each retry — 1s, then 2s, then 4s —
instead of hammering the API at a constant rate. You could see the delays
growing in the printed output before it finally gave up.

We don't retry the 400 case because it's not a transient failure — the
request itself is invalid (bad latitude) and will fail identically no
matter how many times you send it. Retrying it just wastes time and load
for zero chance of success, which connects to the lecture point that
retries should only target failures that might resolve on their own
(network hiccups, brief overload) — retrying a permanent failure at scale
can pile onto an already-struggling system instead of helping.

For a data contract on the raw JSON in data/raw/, I'd want to specify: the
schema (field names/types like temperature_2m as float, current_units
always included), semantics (units per field, timezone handling), an SLA
(how often new files land, how long they're retained), and a change
management policy (advance notice before adding/removing/renaming fields,
so a consuming pipeline doesn't silently break).