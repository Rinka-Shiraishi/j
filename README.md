# PdfCraft — independent archival snapshots

**Upstream:** [storytold/pdfcraft](https://github.com/storytold/pdfcraft) (ArtCraft / Acrobat-style software)

This repository independently preserves the public **Git commit history** of the upstream repository through immutable [GitHub Release snapshots](../../releases). It is not a GitHub fork and is not affiliated with upstream maintainers.

## How it works

- GitHub Actions checks upstream every day at about **12:17 JST** (03:17 UTC), or when manually triggered.
- If any upstream branch or tag changes, the workflow creates a new `snapshot-<fingerprint>` Release containing `upstream.bundle` and `SNAPSHOT.txt`.
- Every bundle is a complete Git snapshot (all observed Git branches and tags, with original commit IDs). Old snapshots are **never overwritten or deleted** by the workflow.
- If upstream is unavailable, the task fails safely: previously saved snapshots remain untouched.
- No personal token or local GitHub CLI is needed for the automatic process.

## Restore from a snapshot

Download `upstream.bundle` from a snapshot Release, then use:

```bash
git clone upstream.bundle restored-project
```

The default `main` branch contains only these archive instructions and the workflow, **not** the application source. To inspect original source code, restore the bundle.

**Limits:** Git LFS content, GitHub Releases binaries, issues/PRs/discussions and externally hosted files are not included. GitHub storage is not an off-site backup; keep a separate copy for stronger preservation. Check the original license before redistributing or using the code.
