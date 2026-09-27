# Dockerized PostgreSQL ELT Pipeline

A containerized Extract, Load, Transform (ELT) pipeline that transfers data from a source PostgreSQL database to a separate destination PostgreSQL database using Docker, Python, `pg_dump`, and `psql`.

## Overview

This project demonstrates a simple database-to-database ELT workflow using three Docker services:

1. **Source PostgreSQL** — contains the initial dataset.
2. **Destination PostgreSQL** — receives the database dump.
3. **ELT Script** — waits for PostgreSQL to become available, extracts the source database, and loads it into the destination database.

The services communicate through a dedicated Docker bridge network.

## Architecture

```text
                    Docker Network
                  ┌─────────────────┐
                  │   elt_network   │
                  │                 │
                  │  ┌───────────┐  │
                  │  │  Source   │  │
                  │  │ PostgreSQL│  │
                  │  │ source_db │  │
                  │  └─────┬─────┘  │
                  │        │         │
                  │        │ pg_dump │
                  │        ▼         │
                  │  ┌───────────┐  │
                  │  │    ELT    │  │
                  │  │  Python   │  │
                  │  │   Script  │  │
                  │  └─────┬─────┘  │
                  │        │         │
                  │        │  psql   │
                  │        ▼         │
                  │  ┌───────────┐  │
                  │  │Destination│  │
                  │  │ PostgreSQL│  │
                  │  │destination│  │
                  │  │    _db    │  │
                  │  └───────────┘  │
                  │                 │
                  └─────────────────┘
