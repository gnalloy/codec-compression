# Examples

[简体中文](examples.zh-CN.md) | [Docs Index](README.md)

## Example 1: Add the Module to an Application

```bash
mkdir gnalloy-app && cd gnalloy-app
go mod init example.com/gnalloy-app
go get gnalloy.org/codec-compression@dev
go doc gnalloy.org/codec-compression
```

## Example 2: Inspect Current Packages

The current source tree exposes these package import paths:
- `gnalloy.org/codec-compression`
- `gnalloy.org/codec-compression/brotli`
- `gnalloy.org/codec-compression/bzip2`
- `gnalloy.org/codec-compression/fastlz`
- `gnalloy.org/codec-compression/internal/stream`
- `gnalloy.org/codec-compression/internal/testutil`
- `gnalloy.org/codec-compression/lz4`
- `gnalloy.org/codec-compression/lzf`
- `gnalloy.org/codec-compression/lzma`
- `gnalloy.org/codec-compression/snappy`
- `gnalloy.org/codec-compression/zstd`

Use `go doc` against the package that matches the behavior you need:

```bash
go doc gnalloy.org/codec-compression
go doc gnalloy.org/codec-compression/brotli
go doc gnalloy.org/codec-compression/bzip2
go doc gnalloy.org/codec-compression/fastlz
go doc gnalloy.org/codec-compression/internal/stream
go doc gnalloy.org/codec-compression/internal/testutil
go doc gnalloy.org/codec-compression/lz4
go doc gnalloy.org/codec-compression/lzf
```

Selected current exported entry points:
- `const DefaultMaxDecodedBytes = 32 << 20`
- `const DefaultStreamChunkSize = 16 * 1024`
- `var ErrInvalidConfig = errors.New("gnalloy/codec/compression: invalid config") ...`
- `type ChunkedEncoderConfig struct{ ... }`
- `type CompressingChunkedInput struct{ ... }`
- `type Decoder struct{ ... }`
- `const BestSpeed = nativebrotli.BestSpeed ...`
- `type Decoder struct{ ... }`
- `type Encoder struct{ ... }`
- `const BestSpeed = nativebzip2.BestSpeed ...`
- `type Decoder struct{ ... }`
- `type Encoder struct{ ... }`
- `var ErrCorruptFrame = errors.New("gnalloy/codec/compression/fastlz: corrupt frame") ...`
- `type Config struct{ ... }`
- `type Decoder struct{ ... }`
- `type Encoder struct{ ... }`
- `type Level uint8`
- `func ByteBufFromBytes(alloc buffer.Allocator, data []byte) (buffer.ByteBuf, error)`

## Example 3: Use Executable Tests as Behavioral Examples

Repository tests are executable examples of supported behavior. Start with the selected names below, then read the matching `_test.go` files for complete setup and assertions. See [Testing and Performance](testing.md) for the complete discovered list.

```bash
GOWORK=off GOTOOLCHAIN=local go test ./... -run Test -count=1
```

Selected current test, benchmark, fuzz, and example entry points:
- `BenchmarkGzipDecoder`
- `BenchmarkGzipEncoderComposite`
- `BenchmarkZlibDecoder`
- `BenchmarkZlibEncoderComposite`
- `TestAlgorithmRoundTripSamples`
- `TestCompressingChunkedInputStreamsGzip`
- `TestDecoderAccumulatesPartialFrames`
- `TestDecoderEnforcesMaxDecodedBytes`
- `TestDecoderRejectsBadMagic`
- `TestDecoderRejectsChecksumMismatch`
- `TestEncoderRejectsInvalidLevel`
- `TestEncoderWritesNettyFastLZHeader`
- `TestEncoderWritesNettyLZFHeader`
- `TestFrameDecoderEnforcesMaxDecodedBytes`
- `TestFrameDecoderRejectsReservedUnskippableChunk`
- `TestFrameDecoderSkipsSkippableChunk`
- `TestFrameEncoderDecoderRoundTrip`
- `TestFrameEncoderWritesNettyUncompressedChunk`

## Example 4: Cross-Module Assembly

Direct Gnalloy dependencies for this module:
- `gnalloy.org/gnalloy`

Assembly guidance:
- Use this codec above a byte-oriented or datagram transport and below application handlers.
- The codec converts bytes or Gnalloy messages into protocol objects and converts outbound protocol objects back to bytes.
- It does not open sockets, own EventLoops, or define application lifecycle.

## Example 5: Pressure-Test Harness

For sustained load, wire this module into a scenario under `gnalloy.org/benchmarks` or a runnable client under `gnalloy.org/examples` when the module participates in network traffic. Record host, OS, CPU, Go version, protocol, payload, concurrency, warmup, repetitions, throughput, and p99 latency in the report.
