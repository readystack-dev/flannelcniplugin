# flannel CNI plugin v1.9.1-flannel3 — ReadyStack release `v1.9.1-flannel3-CE-ubuntu24.04-r4`

Generated 2026-11-20 from this release's build records and strategy. Statements that come from a single record name it in brackets; the others come from this release's strategy and build log.

## Release

- **Image:** `readystack/flannelcniplugin:v1.9.1-flannel3-CE-ubuntu24.04-r4` (linux/amd64). Index digest `sha256:73b0caff72ac84cf7a1893b68e662c7909e11e32075df04fe6041eae9ea89f34` [`docs/provenance/LOCKED_DIGEST.txt`].
- **Image manifest digest:** `sha256:807fdbc72a55061ba38364d8fd0df87e25fdb0349ae36d84782672ca88a5e6fe` [`TARGET_DIGEST.txt`].
- **Upstream:** flannel CNI plugin v1.9.1-flannel3 built from source at `v1.9.1-flannel3` of https://github.com/flannel-io/cni-plugin — upstream notes: https://github.com/flannel-io/cni-plugin/releases/tag/v1.9.1-flannel3 [`docs/provenance/BUILD_RECIPE.json`].
- **Base image:** none (`FROM scratch`): a chiselled Ubuntu 24.04 runtime, the files Canonical's chisel cut from Ubuntu's own packages (`vendored/chisel/slices.txt`, `vendored/chisel/packages.tsv`); runtime user `flannelcniplugin`.
- **Build:** `source-rebuild-go`, compiled offline with `--network=none`.
- **Supersedes:** ReadyStack release `v1.9.1-flannel3-CE-ubuntu24.04-r3`.

## What changed in this release

- Upstream version unchanged (v1.9.1-flannel3); ReadyStack rebuild.
- flannel CNI plugin v1.9.1-flannel3 is unchanged from the release this supersedes (v1.9.1-flannel3-CE-ubuntu24.04-r3); this release rebuilds it. Changes: the image is rebuilt on the current ubuntu:24.04 image (sha256:9c7f200c07e3…), which its maintainers updated after v1.9.1-flannel3-CE-ubuntu24.04-r3 was built on sha256:2198e4c65076…. Settings, ports and data volumes are those of v1.9.1-flannel3-CE-ubuntu24.04-r3: replace the container with this image on the same volumes.

## Security status at release (measured 2026-11-20)

- **Docker Scout:** 0 fixable critical/high vulnerabilities; runs as `flannelcniplugin` (non-root); SBOM + provenance attestations present (SPDX SBOM + SLSA v1) [`docs/provenance/SCOUT_VERDICT.json`].
- **OSV cross-check:** no fixable critical/high vulnerability beyond Docker Scout's findings.
- **Signature:** cosign signature verified by ReadyStack's release gate before publishing; check it yourself with `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/flannelcniplugin:v1.9.1-flannel3-CE-ubuntu24.04-r4` (signatures are recorded in the public Sigstore transparency log).
- **ReadyStack release check at release:** passed (ReadyStack's own test, not a Docker Scout grade). Vulnerabilities are disclosed every day and the image never changes, so it is re-checked daily, beside Docker Scout's own dated grade, at https://readystack.dev/queue.

## Reproducibility

Rebuilds offline from this archive to the identical image digest `sha256:807fdbc72a55061ba38364d8fd0df87e25fdb0349ae36d84782672ca88a5e6fe`: run `./BUILD_OFFLINE.sh`, then `./VERIFY_OFFLINE.sh` (add `--online` to confirm the Docker Hub tag holds the same digest). Before publishing, ReadyStack rebuilt the kit with `./BUILD_OFFLINE.sh` and compared the result with the published digest [`docs/provenance/REPRO_VERIFICATION.json`], then ran `./BUILD_OFFLINE.sh` and `./VERIFY_OFFLINE.sh` from this archive (without `--online`).

## Validation

- 5 of 5 runbook checks passed (5 authored) on the stack's 3-node integration cluster, recorded 2026-10-29T02:34:55Z [`docs/validation/test-results.json`, from the run's record `docs/stack/RUNBOOK_EVIDENCE.json`]. They are the checks of the stack's operator runbook that name this component; no container of this image was started on its own for them. The record does not show this release's image (`sha256:807fdbc72a55061ba38364d8fd0df87e25fdb0349ae36d84782672ca88a5e6fe`) in that run: it lists the component's images as they were then, an earlier build or a tag, so the checks describe the component, not this digest.
- Failed cases are listed in `docs/validation/FAILED_TESTS.md`.

## Known issues

- None recorded.

## Defects fixed

- 1 problem found before release and fixed before it shipped (1 by review); each is listed in `docs/defects/defects.json`.

## Verify this archive

```
sha256sum -c CHECKSUMS.sha256
./BUILD_OFFLINE.sh && ./VERIFY_OFFLINE.sh --online
cosign verify --key https://readystack.dev/keys/cosign.pub readystack/flannelcniplugin:v1.9.1-flannel3-CE-ubuntu24.04-r4
```

ReadyStack records every signature in the public Sigstore transparency log (Rekor), so the command needs no extra flags.

