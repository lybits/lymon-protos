# lymon-protos

Protocol Buffers definitions for the Lymon platform.

This repository contains the gRPC contracts used across Lymon components — the Lymon Agent, the Ingest Gateway, the Cloud control plane, and any third-party integrations.

## Contents

```
proto/
└── lymon/
    └── ingest/
        └── v1/
            └── ingest.proto      # Agent → Ingest Gateway
```

## Versioning

Each protobuf package is suffixed with a version (`v1`, `v2`, ...). Breaking changes require a new version; non-breaking additions are made in place.

The [Buf](https://buf.build/) toolchain is used for linting and breaking-change detection. See `buf.yaml`.

```bash
# Lint
buf lint

# Check for breaking changes vs main
buf breaking --against '.git#branch=main'
```

## Code generation

This repo does **not** ship generated code. Each consumer generates from the `.proto` files in their own build:

| Language | Tool | Where |
|---|---|---|
| Rust | `tonic-build` | `lymon-agent/build.rs` |
| TypeScript | `ts-proto` or `@grpc/proto-loader` | `lymon-ingest-spike/build` |
| Go | `protoc-gen-go` + `protoc-gen-go-grpc` | (future Go services) |

The `lymon-agent` and `lymon-ingest-spike` repos pull this repo as a git submodule or via `cargo` / `npm` git dependency. See those repos for details.

## License

Apache License 2.0 — see [LICENSE](./LICENSE).

## Status

Pre-1.0. Schema may change before reaching stable. Each backward-incompatible change will be documented in `CHANGELOG.md`.
