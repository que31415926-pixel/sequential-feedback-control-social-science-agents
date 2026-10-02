# Formal Review Packets

Each formal gate uses a fresh packet under:

review_packets/<GATE>/

Required files:

- REVIEW_REQUEST.md
- CLAIMS.md
- EVIDENCE_INDEX.md
- METRICS.csv
- CHANGES.diff
- REPRO_COMMANDS.md

The packet indexes evidence; it does not replace source evidence.

Reviewer must:

1. read protocol/FROZEN_PROTOCOL.md;
2. read REVIEW_REQUEST.md;
3. inspect CLAIMS.md;
4. follow EVIDENCE_INDEX.md to direct evidence;
5. use permitted read-only reproduction commands where necessary;
6. return PASS, REVISE, or BLOCK.

Missing evidence must not be silently inferred.

Formal reviews use fresh isolated reviewer sessions.
