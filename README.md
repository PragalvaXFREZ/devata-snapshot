# devata-snapshot

The [devata homelab cluster](https://github.com/PragalvaXFREZ/lab) publishes its own public-safe state here.

`snapshot.json` is machine-written by a read-only CronJob inside the cluster (the snapshot publisher, defined in [`lab/kubernetes/apps/showcase/snapshot-publisher`](https://github.com/PragalvaXFREZ/lab/tree/main/kubernetes/apps/showcase/snapshot-publisher)). Every field is selected by an allowlist transform and validated against a JSON Schema with `additionalProperties: false` before it is pushed. Internal IPs, real node names, and anything credential-shaped never enter the document by construction.

Do not edit this repo by hand. The publisher overwrites `snapshot.json` on the hour, and the commit history doubles as the cluster's off-cluster uptime ledger: each commit is a heartbeat that says the cluster was powered on and healthy enough to describe itself.

Consumed by [pragalva.me/homelab](https://pragalva.me/homelab), which fetches the raw file, renders it, and honestly marks the data stale once it is older than the document's own `freshness.maxAgeHours`.
