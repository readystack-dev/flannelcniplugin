# flannel CNI plugin: ReadyStack build kit

The offline build kit for the Docker image `readystack/flannelcniplugin:v1.9.1-flannel3-CE-ubuntu24.04-r4`. It holds what the image is built from (upstream source, base images, toolchain, pinned dependencies) and the documents, so the image can be rebuilt with no network access (`docker build --network=none`).

- Release: [v1.9.1-flannel3-CE-ubuntu24.04-r4](https://github.com/readystack-dev/flannelcniplugin/releases/tag/v1.9.1-flannel3-CE-ubuntu24.04-r4)
- Image: [`docker.io/readystack/flannelcniplugin:v1.9.1-flannel3-CE-ubuntu24.04-r4`](https://hub.docker.com/r/readystack/flannelcniplugin/tags), manifest digest `sha256:807fdbc72a55061ba38364d8fd0df87e25fdb0349ae36d84782672ca88a5e6fe`
- Product page: https://readystack.dev/products/flannelcniplugin
- Defects: this repository's Issues (defects recorded from 25 November 2026 on) and https://readystack.dev/defects.html?product=flannelcniplugin

flannel CNI plugin is distributed under its upstream licence (Apache-2.0); the kit contains upstream's source under that licence, and each vendored component under its own.

## Download

From the [v1.9.1-flannel3-CE-ubuntu24.04-r4 release](https://github.com/readystack-dev/flannelcniplugin/releases/tag/v1.9.1-flannel3-CE-ubuntu24.04-r4): `ReadyStack-flannelcniplugin-v1.9.1-flannel3-CE-ubuntu24.04-r4.tar.gz` (434.2 MB), SHA-256 `f16f83d5624caab8d29a164011e876717b7222d7c61d420df52f382c37e03483`.

```sh
sha256sum --check --ignore-missing SHA256SUMS
```

## Verify and rebuild

The rebuild statement is signed with the ReadyStack release key. Check the signature before you rely on it:

```sh
cosign verify-blob --key https://readystack.dev/keys/cosign.pub \
  --bundle ReadyStack-flannelcniplugin-v1.9.1-flannel3-CE-ubuntu24.04-r4.rebuild.json.sigstore ReadyStack-flannelcniplugin-v1.9.1-flannel3-CE-ubuntu24.04-r4.rebuild.json
```

Unpack with `-p` so file modes are kept, then follow the kit's own README.md and docs/REBUILD.md:

```sh
tar -xpzf ReadyStack-flannelcniplugin-v1.9.1-flannel3-CE-ubuntu24.04-r4.tar.gz
cd v1.9.1-flannel3-CE-ubuntu24.04-r4
less README.md docs/REBUILD.md
```

The build trail (`ReadyStack-flannelcniplugin-v1.9.1-flannel3-CE-ubuntu24.04-r4.trail.json`, signed the same way, and its Markdown copy) records how this release was built and checked.

## This repository

`recipe/` holds the kit's recipe files (Dockerfiles, build scripts, pins) as published at https://readystack.dev/products/flannelcniplugin/recipe. The complete kit is the release download. Each release is a tag here.
