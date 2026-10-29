# Přehled knowledge base

This is an independent Git repository containing generated knowledge records.
SQLite is the authoring source; this repository is a validated, readable snapshot.
Statements may be unverified, disputed, predictions, or attributed opinions.
An export or Git commit is not an endorsement of their truth.

Records are UTF-8 JSONL, one sorted-key JSON object per line, ordered by ID.
Numeric IDs are sharded into fixed ranges of 1,000; sources and assessors each
use one shard. An identity is (dataset_id, table, id), not a wording fingerprint.
IDs and merged-claim redirects remain intact; merges never erase old records.
schema.json describes the versioned projection; manifest.json records counts
and SHA-256 checksums. There is no changing export timestamp in the data.

Claim definitions, historical definitions, article occurrences and metadata,
assessment histories, evidence, graph relationships, research questions, compact
identity decisions and research provenance are included. Strength s estimates
truth probability; confidence c expresses the assessor's certainty in that
estimate. Both are independent subjective values in [0,1], or both null.
Research model proposals are retained separately from validated stored values.

Article bodies, RSS descriptions, personal notes/stars, credentials, search
indexes, raw prompts/candidate pools, model usage, process logs and worker
heartbeats are excluded. Event details and research inputs use explicit field
projections; omitted event keys are listed in omitted_detail_fields. Full raw
audits remain in the private SQLite archive. Article metadata reflects its last
collected version; occurrence hashes also retain historical versions.

From the application checkout:

    .venv/bin/python -m newsroom kb-export
    .venv/bin/python -m newsroom kb-verify

The exporter validates a consistent database read, checks references and scores,
and commits locally only if the resulting files change. No remote is created and
nothing is pushed. The app exports daily once this repository exists, and batches
new assessment histories into further snapshots at most once per thirty minutes. Make
knowledge edits in the app/database; direct corpus authoring/import is not yet
supported. Export refuses dirty repositories and invalid existing snapshots.
If interrupted while publishing files, the previous Git commit remains intact;
inspect the working tree before restoring generated files from that commit.

Migration bundles preserve this repository's committed branches, tags and
history separately from the application's Git history and live database.
