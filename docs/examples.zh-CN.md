# 案例

[English](examples.md) | [文档索引](README.zh-CN.md)

## 案例 1：将模块加入应用

```bash
mkdir gnalloy-app && cd gnalloy-app
go mod init example.com/gnalloy-app
go get gnalloy.org/codec-compression@dev
go doc gnalloy.org/codec-compression
```

## 案例 2：查看当前包

当前源码树暴露这些 package 导入路径：
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

按需要的行为对对应 package 执行 `go doc`：

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

精选当前导出入口：
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

## 案例 3：将可执行测试作为行为示例

仓库测试是受支持行为的可执行示例。先从下面的精选名称开始，再阅读对应 `_test.go` 文件中的完整 setup 和断言。完整发现列表见 [测试与性能](testing.zh-CN.md)。

```bash
GOWORK=off GOTOOLCHAIN=local go test ./... -run Test -count=1
```

精选当前 test、benchmark、fuzz 与 example 入口：
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

## 案例 4：跨模块装配

本模块的直接 Gnalloy 依赖：
- `gnalloy.org/gnalloy`

装配说明：
- codec 位于面向字节或 datagram 的 transport 之上、应用 handler 之下。
- 它负责把字节或 Gnalloy 消息转换成协议对象，并把出站协议对象转换回字节。
- 它不打开 socket，不拥有 EventLoop，也不定义应用生命周期。

## 案例 5：压测 Harness

持续负载测试时，如果该模块参与网络流量路径，将它接入 `gnalloy.org/benchmarks` 的场景，或接入 `gnalloy.org/examples` 的可运行客户端。报告中记录 host、OS、CPU、Go version、protocol、payload、concurrency、warmup、repetitions、throughput 和 p99 latency。
