# Provenance — flannel CNI plugin (`v1.9.1-flannel3-CE-ubuntu24.04-r4`)

Every item below is copied from a record in this archive; the record is named in brackets.

## Source

- Upstream repository: https://github.com/flannel-io/cni-plugin
- Revision built: `v1.9.1-flannel3` (commit `b380f201008e9bed159703846cf10d3c50b4f9ce`)
- Source tree: `0a7880b2dc90b22720e84af9cc7fe703812caf54d2c51fd01849a861d6fc7508` over 26 files [`docs/provenance/SOURCE_TREE_HASH.json`]
- Community Edition only: enterprise code is removed or refused before the build (CE audit at acquire).

## Build

- Method: `source-rebuild-go`; base image `scratch + a chiselled Ubuntu 24.04 runtime (vendored/chisel/slices.txt, packages.tsv)`
- Compiled with `--network=none` from vendored source, dependencies and base images; BuildKit pinned to `moby/buildkit:v0.31.2` (shipped in `toolchain/`).
- SOURCE_DATE_EPOCH: `1795161042` [`SOURCE_DATE_EPOCH.txt`]
- Frozen inputs: [`docs/provenance/FREEZE_MANIFEST.json`], build recipe: [`docs/provenance/BUILD_RECIPE.json`].

## Output

- Published image: `readystack/flannelcniplugin:v1.9.1-flannel3-CE-ubuntu24.04-r4` — index digest `sha256:73b0caff72ac84cf7a1893b68e662c7909e11e32075df04fe6041eae9ea89f34` [`docs/provenance/LOCKED_DIGEST.txt`]
- linux/amd64 image digest `sha256:807fdbc72a55061ba38364d8fd0df87e25fdb0349ae36d84782672ca88a5e6fe` — reproduced from this archive before publishing [`docs/provenance/REPRO_VERIFICATION.json`].

## Attestations and signature

- SBOM + SLSA provenance attached to the image: attached: an SPDX SBOM and SLSA v1 provenance [`docs/provenance/SCOUT_VERDICT.json`]
- cosign signature by the ReadyStack release key: verified before publishing. Check it: `cosign verify --key https://readystack.dev/keys/cosign.pub readystack/flannelcniplugin:v1.9.1-flannel3-CE-ubuntu24.04-r4`

## Pinned inputs, and why

- 19 pinned inputs, each with where it came from, why this one, how it was checked and when it was decided: `docs/PINS.md` [`docs/provenance/PINS.json`] (upstream source 2, base and build images 3, image digests 2, pins in the kit's dockerfiles 5, readystack's build engine 5, dependencies upstream chose 2).

## Build trail

- How this release passed through the ReadyStack harness, record by record (every chain, drive, stage, review round, defect and check, each naming the record it is copied from): `ReadyStack-flannelcniplugin-v1.9.1-flannel3-CE-ubuntu24.04-r4.trail.json`, published beside this archive and signed with the release key (`ReadyStack-flannelcniplugin-v1.9.1-flannel3-CE-ubuntu24.04-r4.trail.json.sigstore`), and readable at https://readystack.dev/products/flannelcniplugin/trail/v1.9.1-flannel3-CE-ubuntu24.04-r4.

