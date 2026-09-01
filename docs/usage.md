# Usage

[简体中文](usage.zh-CN.md) | [Docs Index](README.md)

## Requirements

- Go 1.25 or newer, matching the module `go` directive.
- A Gnalloy application, recipe, example, or benchmark harness that owns lifecycle and deployment configuration.
- Standalone module verification should set `GOWORK=off` so the module is tested through its published dependency graph.

## Install
```bash
go get gnalloy.org/codec-compression@dev
```

## Import
```go
import "gnalloy.org/codec-compression"
```

## Integration Pattern
- Frame, header, body, and decoded-content limits must be selected from the trusted boundary of the service.
- Streaming or chunked modes should be used for large payloads instead of materializing unbounded bodies.
- Compression modules must set decoded-size limits to defend against expansion attacks.
- ByteBuf ownership follows Gnalloy message rules: release only after the current component consumes the message.

## API Selection

Use the API inventory to choose the exact constructor or option type for your protocol path:

```bash
go doc gnalloy.org/codec-compression
```

Common current entry points:
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

## Cross-Module Assembly

When multiple Gnalloy repositories are developed together, create a local `go.work` file in your chosen workspace. Keep application-local `replace` directives out of published library modules unless the change is intentionally temporary and never committed.

## Error Handling

Network input, peer behavior, platform capability, and timeout failures must be handled as normal errors. Do not recover protocol correctness by panicking. Return or propagate the module error and close the affected Channel when ownership requires it.
