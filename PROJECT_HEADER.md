# StdOut Scanner — Project Header

**Status:** active
**Repo:** https://github.com/seayniclabs/stdout-scanner (public) — free stand-alone tool
**Image:** ghcr.io/seayniclabs/stdout-scanner (built by `.github/workflows/build.yml` on push to main and on `v*` tags)

## Project Identity

Free Docker-host inventory scanner. Prints a Markdown or JSON report, or pushes it to a webhook,
a file or an API. Absorbs the `scanner-standalone` idea (same code; archived 2026-10-22).

## Last Decisions

- 2026-10-22 House Cleaning: module path moved to `github.com/seayniclabs/stdout-scanner` after the
  org move; Docker Hub workflow removed (no image was ever published there), ghcr under the org is
  the one image; committed binaries untracked; with no push target the report is printed.

## Next Steps

1. Charlie: pick a licence. The README says "Proprietary" but the repo is public and the tool is free (other free tools are MIT).
2. Tag v2.2.0 so the release and ghcr image carry the new module path; confirm `ghcr.io/seayniclabs/stdout-scanner` pulls anonymously.
3. Add tests for `internal/network` and `internal/output` (only `sources` and `update` have tests).
4. Run `gofmt -w .` (15 files were already unformatted before 2026-10-22).
