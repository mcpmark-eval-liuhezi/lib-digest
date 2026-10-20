# Python HTTP Client Intake Brief

Shortlist: **requests** vs **httpx**. All figures below come from live lookups against
PyPI and the projects' source repositories at the time of writing — no numbers from
memory or third-party blog posts.

## Data sources (paper trail)

| What | Where |
| --- | --- |
| requests metadata (machine-readable) | `https://pypi.org/pypi/requests/json` |
| httpx metadata (machine-readable) | `https://pypi.org/pypi/httpx/json` |
| requests human-facing project page | `https://pypi.org/project/requests/` |
| requests license text | `https://github.com/psf/requests` — file `LICENSE` |
| httpx license text | `https://github.com/encode/httpx` — file `LICENSE.md` |

Source repositories are the ones the PyPI metadata's `project_urls` point to
(requests → `github.com/psf/requests`; httpx → `github.com/encode/httpx`).

## Findings

| Library | Current version | License | Minimum Python | Dependency count |
| --- | --- | --- | --- | --- |
| requests | 2.34.2 | Apache-2.0 | 3.10 (`requires_python: >=3.10`) | 6 |
| httpx | 0.28.1 | BSD-3-Clause | 3.8 (`requires_python: >=3.8`) | 12 |

### Dependency counts, spelled out

- **requests — 6** entries in `requires_dist`: charset_normalizer, idna, urllib3,
  certifi, PySocks (optional extra `socks`), chardet (optional extra `use-chardet-on-py3`).
- **httpx — 12** entries in `requires_dist`: anyio, certifi, httpcore, idna, brotli
  (extra `brotli`), brotlicffi (extra `brotli`), click (extra `cli`), pygments (extra `cli`),
  rich (extra `cli`), h2 (extra `http2`), socksio (extra `socks`), zstandard (extra `zstd`).

## Cross-checks

1. **PyPI project page vs. metadata (requests):** the human-facing page at
   `https://pypi.org/project/requests/` displays **requests 2.34.2**, which matches the
   `version` field in the machine-readable metadata. **MATCH.**
2. **License texts vs. declared licenses:**
   - requests: `LICENSE` in `psf/requests` is the full **Apache License, Version 2.0**
     text (terms and conditions, definitions, patent grant, etc.). Metadata declares
     `Apache-2.0`. **MATCH.**
   - httpx: `LICENSE.md` in `encode/httpx` is a **3-clause BSD** license (copyright
     notice, binary redistribution clause, non-endorsement clause, warranty disclaimer).
     Metadata declares `BSD-3-Clause`. **MATCH.**

## Warehouse

The warehouse target was database `library_intake`, table `public.packages`, one row
per library (name, version, license, minimum python, dependency count).

**Warehouse row count: 0** — the database could not be created. The connected Snowflake
account denies all database creation (every `CREATE DATABASE` route is rejected by the
server's allowed-databases policy, and `library_intake` does not already exist), so the
table and its two rows were never written. The database is *not* present when databases
are listed. The figures above therefore stand on the live PyPI/GitHub paper trail only.

## Summary for the standup

- requests 2.34.2, Apache-2.0, Python >=3.10, 6 dependencies named.
- httpx 0.28.1, BSD-3-Clause, Python >=3.8, 12 dependencies named.
- PyPI page version matched the metadata (requests).
- Both license texts matched their declared licenses.
- Warehouse row count: 0 (creation denied — see above).
