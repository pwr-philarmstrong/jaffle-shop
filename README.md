# Powwr Jaffle Shop Challenge — Setup (dbt + DuckDB)

This repository is a ready-to-run dbt project using DuckDB and seed data to simulate a small e-commerce pipeline. Use this README to get your environment configured and verify dbt + DuckDB are working locally. Once setup is complete, continue to the TECH_TEST_CHALLENGES.md document for the step-by-step exercises and evaluation tasks.

Start here:
- Follow the "Quick setup" and "Configure dbt to use DuckDB" sections below to prepare your environment.
- After setup, open TECH_TEST_CHALLENGES.md (in the repository root) to begin the tech test challenges in order.

This README explains how to set up the local environment, configure dbt to use DuckDB, and load the project's default seed data.

This Project is a folk of the std dbt repo https://github.com/dbt-labs/jaffle-shop

## Prerequisites
- Git
- Python 3.9+
- Poetry
- dbt-core and dbt-duckdb (installed via Poetry or pip)

## Quick setup (recommended)
1. Clone the repo and enter it:
   ```bash
   git clone https://github.com/pwr-philarmstrong/jaffle-shop.git
   cd jaffle-shop
   ```

2. Install Poetry (if not installed):
   ```bash
   pip install --user poetry
   ```
   (or follow https://python-poetry.org/docs/#installation)

3. Install project dependencies:
   ```bash
   poetry install
   poetry self add poetry-plugin-shell
   ```

4. Activate the virtual environment (optional):
   ```bash
   
   poetry shell
   ```
   Or prefix commands with `poetry run` (e.g., `poetry run dbt debug`)


## Configure dbt to use DuckDB
- Create or update your dbt profiles file at `%USERPROFILE%\.dbt\profiles.yml` (Windows) or `~/.dbt/profiles.yml` (macOS / Linux).
- Example minimal `profiles.yml` for this project or copy from sample_profiles.yml:

```yaml
# Example: ~/.dbt/profiles.yml
default:
  outputs:        
    local:
      type: duckdb
      path: "jaffle-shop-challenge.duckdb"
      threads: 1
      keep_open: true
  target: local
```

## Verify dbt setup
- ```bash
  dbt debug
  ```
- You should see connection success for the DuckDB target.

## Load default data (seed) and build
1. Seed the project (this loads the default CSV/seed data used by the models):
   ```bash
   dbt seed --full-refresh --vars '{"load_source_data": true}'
   ```

2. Build the project (runs models, tests, analyses as configured):
   ```bash
   dbt build
   ```


## Challenge Approach

1. **Read** `TECH_TEST_CHALLENGES.md` carefully - each challenge has detailed instructions
2. **Start with Level 1** - SQL fundamentals before architectural patterns
3. **Test frequently** - Run `dbt build` after each model
4. **Document your work** - Add comments explaining your approach
5. **Reference errors** - Check `target/compiled/` for compiled SQL if debugging

## Resources
- [dbt documentation](https://docs.getdbt.com) — dbt core docs and best practices.
- [DuckDB SQL documentation](https://duckdb.org/docs/sql/introduction) — DuckDB intro and SQL reference.
- [dbt unit tests](https://docs.getdbt.com/docs/build/unit-tests) — dbt's unit testing guide.
- [dbt contracts](https://docs.getdbt.com/docs/collaborate/contracts) — data contract docs.
- Visual Studio Code (IDE): https://code.visualstudio.com/ — lightweight, extensible editor. Useful extensions: Python, SQL, and dbt helper extensions (e.g., dbt Power User).
- DuckDB Studio / UI: https://duckdb.org/docs/tools/duckdb_studio — UI for exploring DuckDB files and running ad-hoc queries.
- Poetry (dependency manager): https://python-poetry.org/ — used here for Python and dbt dependency management.
- Jaffle Shop (official dbt demo repo): https://github.com/dbt-labs/jaffle_shop — canonical example to reference.
- DuckDB regex functions: https://duckdb.org/docs/sql/functions/regexp — reference for REGEXP-related functions used for SKU parsing and pattern extraction.
- DuckDB JSON functions: https://duckdb.org/docs/sql/functions/json — reference for JSON_EXTRACT, JSON_PARSE, and other JSON helpers used for audit log extraction.
