# GENERATED L-009 hermetic build (--network=none, SBOM+SLSA-attestation-producing).
# Pinned bases from BASE_IMAGE_DIGESTS.lock; vendored Go tree + debs from Dockerfile.vendor.
FROM golang:1.26.11-bookworm@sha256:dc40a13b61304647ed7e5d581d246b86413dfc29d63c6d018310feb93cd98fc0 AS build_flannel
WORKDIR /src
COPY vendored/flannelcniplugin-src/ .
ENV CGO_ENABLED=1 GOTOOLCHAIN=local GOWORK=off GOFLAGS="-mod=vendor -buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1795161042
RUN go build -trimpath -tags "netgo osusergo no_stage static_build" -ldflags='-extldflags -static -w -X main.Version=v1.9.1 -X main.Commit=b380f201 -X main.Program=flannel' -o /flannel . && /flannel version > /tmp/flannel.version 2>&1; cat /tmp/flannel.version; grep -qF 'CNI Plugin flannel version v1.9.1' /tmp/flannel.version || { echo 'flannel version does not report CNI Plugin flannel version v1.9.1'; exit 1; } && \
    { readelf -lW /flannel | sed -n 's/.*Requesting program interpreter: \(.*\)]$/\1/p'; readelf -dW /flannel | sed -n 's/.*Shared library: \[\(.*\)\]$/\1/p'; } > /flannel.needs
# rs-probe: the HEALTHCHECK helper (standard library only, from the kit's rs-probe.go)
FROM golang:1.26.11-bookworm@sha256:dc40a13b61304647ed7e5d581d246b86413dfc29d63c6d018310feb93cd98fc0 AS build_rs_probe
WORKDIR /probe
COPY rs-probe.go main.go
COPY rs-probe.mod go.mod
ENV CGO_ENABLED=0 GOTOOLCHAIN=local GOFLAGS="-buildvcs=false" GOPROXY=off SOURCE_DATE_EPOCH=1795161042
RUN go build -trimpath -ldflags='-s -w' -o /rs-probe .
# the chiselled rootfs (vendored/chisel, cut by Dockerfile.vendor), the service user, the binaries
FROM ubuntu:24.04@sha256:9c7f200c07e3d4a03e7249d2c16bf66a51120fb876aa2242cf31451412543289 AS rootfs
ARG SOURCE_DATE_EPOCH=1795161042
ADD vendored/chisel/rootfs.tar /rootfs/
RUN printf 'flannelcniplugin:x:999:999::/var/lib/flannelcniplugin:/bin/sh\n' >> /rootfs/etc/passwd && printf 'flannelcniplugin:x:999:\n' >> /rootfs/etc/group && \
    mkdir -p /rootfs/var/lib/flannelcniplugin && chown -R 999:999 /rootfs/var/lib/flannelcniplugin
COPY --from=build_flannel /flannel /rootfs/flannel
COPY --from=build_flannel /flannel.needs /tmp/needs/flannel
COPY --from=build_rs_probe /rs-probe /rootfs/usr/local/bin/rs-probe
RUN chmod 755 /rootfs/flannel /rootfs/usr/local/bin/rs-probe
RUN --mount=type=bind,source=vendored/chisel,target=/chisel set -eu; \
    for n in /tmp/needs/*; do while read -r lib; do [ -n "$lib" ] || continue; \
      case "$lib" in /*) [ -e "/rootfs$lib" ] ;; *) [ -n "$(find /rootfs/usr/lib /rootfs/usr/lib64 -name "$lib" 2>/dev/null | head -1)" ] ;; esac || \
      { echo "$(basename "$n") needs $lib, which the chiselled rootfs does not have: add its slice to runtime_base.slices" >&2; exit 1; }; \
    done < "$n"; done; rm -rf /tmp/needs; \
    [ -e /rootfs/etc/os-release ] || { echo "no /etc/os-release: base-files_release-info is missing" >&2; exit 1; }; \
    [ "$(grep -c '^Package: ' /rootfs/var/lib/dpkg/status)" = "$(wc -l < /chisel/packages.tsv)" ] || \
      { echo "/var/lib/dpkg/status does not list every package of vendored/chisel/packages.tsv" >&2; exit 1; }; \
    rm -rf /rootfs/var/log/dpkg.log /rootfs/var/log/alternatives.log /rootfs/var/log/apt /rootfs/var/cache/ldconfig/aux-cache /rootfs/var/cache/fontconfig
FROM scratch
ARG SOURCE_DATE_EPOCH=1795161042
COPY --from=rootfs /rootfs/ /
ENV PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin
LABEL org.opencontainers.image.licenses="Apache-2.0"
LABEL org.opencontainers.image.title="flannel CNI plugin"
LABEL org.opencontainers.image.source="https://github.com/flannel-io/cni-plugin"
LABEL org.opencontainers.image.version="v1.9.1-flannel3-CE-ubuntu24.04-r4"
LABEL org.opencontainers.image.revision="b380f201008e9bed159703846cf10d3c50b4f9ce"
# image_healthcheck false: no HEALTHCHECK (a Kubernetes pod component; the kubelet ignores one)
USER flannelcniplugin
ENTRYPOINT []
CMD ["/flannel"]
