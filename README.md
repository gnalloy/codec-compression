# codec-compression

[简体中文](README.zh-CN.md) | [Documentation](docs/README.md)

Compression codecs for Gnalloy pipelines, including gzip, zlib, brotli, snappy, lz4, zstd, bzip2, lzma, FastLZ, and LZF.

This module sits above transports and below application handlers. It translates bytes or Gnalloy messages into protocol objects, and translates outbound protocol objects back to bytes. It does not open sockets or own EventLoops.

## Status

- Import path: `gnalloy.org/codec-compression`
- Repository: `github.com/gnalloy/codec-compression`
- Default branch: `dev`
- Preview install: `go get gnalloy.org/codec-compression@dev`
- License: Apache-2.0

## Install
```bash
go get gnalloy.org/codec-compression@dev
go doc gnalloy.org/codec-compression
GOWORK=off GOTOOLCHAIN=local go test ./... -count=1
```

## Documentation
- [Overview](docs/overview.md) ([中文](docs/overview.zh-CN.md))
- [Usage](docs/usage.md) ([中文](docs/usage.zh-CN.md))
- [Examples](docs/examples.md) ([中文](docs/examples.zh-CN.md))
- [Configuration](docs/configuration.md) ([中文](docs/configuration.zh-CN.md))
- [Testing and Performance](docs/testing.md) ([中文](docs/testing.zh-CN.md))
- [API Reference](docs/api.md) ([中文](docs/api.zh-CN.md))
- [Notes and Caveats](docs/notes.md) ([中文](docs/notes.zh-CN.md))
- [ADR-001 Module Boundary](docs/decisions/0001-module-boundary.md) ([中文](docs/decisions/0001-module-boundary.zh-CN.md))

## Module Boundary

This repository owns: Compression codecs for Gnalloy pipelines, including gzip, zlib, brotli, snappy, lz4, zstd, bzip2, lzma, FastLZ, and LZF.

It does not absorb neighboring module responsibilities. Core primitives stay in `gnalloy.org/gnalloy`; protocol codecs, transports, handlers, resolvers, examples, and benchmarks stay in their own repositories.

## Packages
- `gnalloy.org/codec-compression` (`compression`)
- `gnalloy.org/codec-compression/brotli` (`brotli`)
- `gnalloy.org/codec-compression/bzip2` (`bzip2`)
- `gnalloy.org/codec-compression/fastlz` (`fastlz`)
- `gnalloy.org/codec-compression/internal/stream` (`stream`)
- `gnalloy.org/codec-compression/internal/testutil` (`testutil`)
- `gnalloy.org/codec-compression/lz4` (`lz4`)
- `gnalloy.org/codec-compression/lzf` (`lzf`)
- `gnalloy.org/codec-compression/lzma` (`lzma`)
- `gnalloy.org/codec-compression/snappy` (`snappy`)
- `gnalloy.org/codec-compression/zstd` (`zstd`)

## Gnalloy Dependencies

- `gnalloy.org/gnalloy`

## Common Integration Pattern
- Frame, header, body, and decoded-content limits must be selected from the trusted boundary of the service.
- Streaming or chunked modes should be used for large payloads instead of materializing unbounded bodies.
- Compression modules must set decoded-size limits to defend against expansion attacks.
- ByteBuf ownership follows Gnalloy message rules: release only after the current component consumes the message.

## Current Public Entry Points

The generated API reference lists the full public surface. Common constructors or option types currently include:
- `const DefaultMaxDecodedBytes = 32 << 20`
- `const DefaultStreamChunkSize = 16 * 1024`
- `var ErrInvalidConfig = errors.New("gnalloy/codec/compression: invalid config") ...`
- `type ChunkedEncoderConfig struct{ ... }`
- `const BestSpeed = nativebrotli.BestSpeed ...`
- `const BestSpeed = nativebzip2.BestSpeed ...`
- `var ErrCorruptFrame = errors.New("gnalloy/codec/compression/fastlz: corrupt frame") ...`
- `type Config struct{ ... }`
- `func NewByteBufReader(src buffer.ByteBuf) io.Reader`
- `const Fast = nativelz4.Fast ...`
- `var ErrCorruptFrame = errors.New("gnalloy/codec/compression/lzf: corrupt frame") ...`
- `type Config struct{ ... }`
- `const DefaultDictCap = 1 << 20 ...`
- `type Config struct{ ... }`
- `var ErrInvalidFrame = errors.New("gnalloy/codec/compression/snappy: invalid framed chunk") ...`
- `type FrameDecoderConfig struct{ ... }`

## Verification

```bash
GOWORK=off GOTOOLCHAIN=local go test ./... -count=1
GOWORK=off GOTOOLCHAIN=local go vet ./...
GOWORK=off GOTOOLCHAIN=local go test ./... -run '^$' -bench . -benchmem -count=1
```

For pressure tests, assemble this module with the relevant transport, codec, and handler stack and run the scenario from `gnalloy.org/benchmarks` or `gnalloy.org/examples`. Keep host, operating system, payload, concurrency, warmup, and repetitions in the report.

## Caveats
- This repository is intentionally narrow. Cross-module behavior should be assembled in applications, recipes, examples, or benchmark harnesses.
- Public APIs should remain Go-native and explicit; avoid runtime scanning, hidden global registries, and reflection-heavy behavior in hot paths.
- Treat network input as untrusted. Configure parser limits and return typed errors instead of panics.
- Keep benchmark claims tied to a concrete host, operating system, protocol, payload, concurrency, warmup, and repetition count.
- Codec modules do not provide a network server by themselves; combine them with a transport module and application handlers.
