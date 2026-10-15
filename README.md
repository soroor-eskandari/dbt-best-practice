# dbt best practice

dbt + Postgres starter project.

## Layout

```
models/
  staging/       # 1:1 with sources, light cleaning (views)
  intermediate/  # reusable transformation steps (ephemeral)
  marts/         # business-facing models (tables)
seeds/ macros/ tests/ snapshots/ analyses/
```

## Setup

```bash
cp .env.example .env            # adjust if needed
docker compose up -d            # start Postgres
uv sync                         # install dbt-core + dbt-postgres
set -a; source .env; set +a     # export connection env vars
uv run dbt deps                 # install dbt packages
uv run dbt debug                # verify connection
```

`profiles.yml` lives in the project root (dbt picks it up automatically) and reads
credentials from environment variables, so no secrets are committed.
