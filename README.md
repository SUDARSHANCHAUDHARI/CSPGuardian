# CSP Guardian

[![Python](https://img.shields.io/badge/Python-3.10%2B-blue)](#requirements)
[![Status](https://img.shields.io/badge/status-MVP-green)](#status)
[![Security](https://img.shields.io/badge/security-defensive%20lab-purple)](#safe-use)
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)

Website security header and iframe policy analyzer. Inspects CSP, X-Frame-Options, cookies, CORS, and HSTS configuration to flag clickjacking, XSS, and framing risks.

---

## Overview

CSP Guardian is a defensive analysis tool that fetches a URL's response headers, parses Content-Security-Policy directives, evaluates iframe and framing posture, and produces a risk-scored report with remediation hints. Useful for auditing security headers on production sites, kiosks, signage, and embedded webviews.

The current MVP is a Python CLI. A FastAPI + React web dashboard is scaffolded under `apps/` for future development.

## Features

- Fetches and parses response security headers
- Analyzes Content-Security-Policy directives
- Detects iframe / framing policy gaps (clickjacking risk)
- Checks cookie security flags (`Secure`, `HttpOnly`, `SameSite`)
- Scores CORS and HSTS posture
- Outputs JSON findings, risk summary, Markdown report, and triage handoff

## Requirements

- Python 3.10 or newer
- Linux, macOS, or Windows
- No third-party Python packages (standard library only)
- Optional: Docker for the demo container
- Network access for live URL scanning (sample mode works offline)

## Installation

```bash
git clone https://github.com/SUDARSHANCHAUDHARI/CSPGuardian.git
cd CSPGuardian
pip install .
```

This registers the `csp-guardian` CLI command.

To run without installing:

```bash
python3 main.py --help
```

## Usage

Scan a target URL:

```bash
python3 main.py --url https://example.com --out-dir reports
```

Generated outputs in `reports/`:

- `headers.json` — captured response headers
- `findings.json` — flagged policy gaps
- `summary.json` — risk score and severity counts
- `report.md` — Markdown header / CSP report
- `triage.md` — analyst triage checklist

## Project Structure

```
CSPGuardian/
├── apps/
│   ├── api/        FastAPI app scaffold (planned)
│   └── web/        React/Next.js app scaffold (planned)
├── data/
│   ├── samples/    Safe sample headers for offline demo
│   └── reports/    Example generated output
├── docker/         Dockerfile + compose support
├── docs/           Architecture, security notes, demo
├── scripts/        Setup, seed, and run helpers
├── tests/          Unit and integration tests
├── main.py         CLI entrypoint
├── pyproject.toml  Package metadata
└── LICENSE
```

## Testing

```bash
python3 -m unittest discover -s tests -p 'test_*.py'
```

## Docker Demo

```bash
docker compose run --rm api
```

## Safe Use

This project is defensive and analysis-focused. Use only on websites, kiosks, and lab environments you own or have explicit written permission to assess.

## Status

Working Python CLI MVP. Web dashboard scaffold present but not yet implemented.

## Roadmap

- Live HTTPS certificate inspection
- Subresource Integrity (SRI) checks
- Bulk URL scanning with concurrency
- GitHub Actions integration for policy regression checks
- Web dashboard for findings and remediation suggestions

## License

Released under the [MIT License](LICENSE). You are free to use, modify, and distribute this software with attribution.

## Author

**Sudarshan Chaudhari** — [SudarshanTechLabs](https://github.com/SUDARSHANCHAUDHARI)
Bangkok, Thailand

For inquiries: open an issue on [GitHub](https://github.com/SUDARSHANCHAUDHARI/CSPGuardian/issues).
