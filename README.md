# stdout-scanner

Free scanner that inventories your Docker host (containers, ports, networks, volumes, host
facts) and prints a Markdown or JSON report. It can also push the report to a webhook or a
file. It started as StdOut's sidecar; StdOut is now a Sonique module, and the scanner is a
stand-alone free tool.

## Quick Start

```bash
docker run --rm \
  -v /var/run/docker.sock:/var/run/docker.sock:ro \
  ghcr.io/seayniclabs/stdout-scanner --output markdown
```

With no `--output` and no push target, the Markdown report is printed.

## What it discovers

- Docker containers: name, image, ports, status, health, networks, compose project
- Volume mount paths
- Environment variable **names** (never values)
- Restart policies
- Host: OS, CPU, memory, disk
- Docker networks: name, driver, subnet, connected containers

## What it never collects

- Environment variable values
- File contents
- Secrets, credentials, or tokens
- Anything outside Docker

## Options

```
--token     API token for a push target (optional)
--url       Push target URL (optional)
--webhook   POST the report to this URL (optional)
--save-to   Also write the JSON report to this file
--output    json or markdown (print to stdout instead of pushing; with no push target the Markdown report is printed)
--full      Enable all detection modules
--scan-sources Detect installed tooling (Prometheus, Trivy, Loki, etc.)
--skip-host Skip host info collection
--dry-run   Discover but don't push
--version   Print version
```

## Data source auto-registration

When `--scan-sources` is enabled, scanner includes a `data_sources` block in
the payload. StdOut uses this to auto-register supported sources during
`/app/api/stacks/import` (currently Prometheus), so metrics enrichment can work
without manual setup.

## Local output

```bash
# JSON to stdout
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock:ro \
  ghcr.io/seayniclabs/stdout-scanner --output json

# Markdown to stdout
docker run --rm -v /var/run/docker.sock:/var/run/docker.sock:ro \
  ghcr.io/seayniclabs/stdout-scanner --output markdown
```

## Build from source

```bash
go build -o stdout-scanner ./cmd/scanner
```

## License

No license file is included in this repository yet.
