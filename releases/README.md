# Cilium Envoy releases

Release tags promote an already tested, digest-pinned candidate to the public
`cilium-envoy` GHCR package in this repository owner's namespace. Promotion
copies the image manifests; it does not rebuild the binary. The workflow checks
that the promoted amd64 manifest is identical to the tested candidate and that
the binary reports the expected source and Envoy versions.

`v1.37.6-cilium1.20.2-tigo.1` contains the null-address guard for local
overload responses. It is based on the Cilium 1.20.2 proxy source, uses Envoy
1.37.6, and was exercised on a single production node with 201 isolated
overflow responses. The production deployment should pin the released image
by its registry digest, not by a mutable tag.

The candidate image is retained for traceability. A later release requires a
new candidate build, canary validation, a release metadata file with its exact
source commit and digest, and a corresponding update to the workflow's
allowlist before publishing a new tag. The tag prefix identifies the upstream
Envoy and Cilium versions; `tigo.N` is the local patch revision.
