# API 参考

[English](api.md) | [文档索引](README.zh-CN.md)

本清单由本仓库 package 的 `go doc -short` 生成，用于快速查看公共面。精确语义以源码和测试为准。

## 包

### `gnalloy.org/codec-compression`

包名：`compression`

```text
const DefaultMaxDecodedBytes = 32 << 20
const DefaultStreamChunkSize = 16 * 1024
var ErrInvalidConfig = errors.New("gnalloy/codec/compression: invalid config") ...
type ChunkedEncoderConfig struct{ ... }
type CompressingChunkedInput struct{ ... }
    func NewCompressingChunkedInput(input codec.ChunkedInput, cfg ChunkedEncoderConfig) (*CompressingChunkedInput, error)
type Decoder struct{ ... }
    func NewGzipDecoder(maxDecodedBytes int) (*Decoder, error)
    func NewZlibDecoder(maxDecodedBytes int) (*Decoder, error)
type Encoder struct{ ... }
    func NewGzipEncoder(level int) (*Encoder, error)
    func NewZlibEncoder(level int) (*Encoder, error)
type Format uint8
    const FormatGzip Format = iota + 1 ...
```

### `gnalloy.org/codec-compression/brotli`

包名：`brotli`

```text
const BestSpeed = nativebrotli.BestSpeed ...
type Decoder struct{ ... }
    func NewDecoder(maxDecodedBytes int) *Decoder
type Encoder struct{ ... }
    func NewEncoder(level int) (*Encoder, error)
```

### `gnalloy.org/codec-compression/bzip2`

包名：`bzip2`

```text
const BestSpeed = nativebzip2.BestSpeed ...
type Decoder struct{ ... }
    func NewDecoder(maxDecodedBytes int) *Decoder
type Encoder struct{ ... }
    func NewEncoder(level int) (*Encoder, error)
```

### `gnalloy.org/codec-compression/fastlz`

包名：`fastlz`

```text
var ErrCorruptFrame = errors.New("gnalloy/codec/compression/fastlz: corrupt frame") ...
type Config struct{ ... }
type Decoder struct{ ... }
    func NewDecoder(config Config) (*Decoder, error)
type Encoder struct{ ... }
    func NewEncoder(config Config) (*Encoder, error)
type Level uint8
    const LevelAuto Level = iota ...
```

### `gnalloy.org/codec-compression/internal/stream`

包名：`stream`

```text
func ByteBufFromBytes(alloc buffer.Allocator, data []byte) (buffer.ByteBuf, error)
func DecodeAll(alloc buffer.Allocator, reader io.Reader, maxDecodedBytes int) (buffer.ByteBuf, error)
func NewByteBufReader(src buffer.ByteBuf) io.Reader
func WriteByteBuf(writer io.Writer, src buffer.ByteBuf) error
```

### `gnalloy.org/codec-compression/internal/testutil`

包名：`testutil`

```text
func Buffer(data []byte) buffer.ByteBuf
func DecodeWithHandler(t *testing.T, decoder readHandler, compressed buffer.ByteBuf) buffer.ByteBuf
func EncodeWithHandler(t testing.TB, encoder writeHandler, payload []byte) buffer.ByteBuf
type Collector struct{ ... }
    func DecodeWithCollector(t testing.TB, decoder readHandler, compressed buffer.ByteBuf) *Collector
type Sink struct{ ... }
```

### `gnalloy.org/codec-compression/lz4`

包名：`lz4`

```text
const Fast = nativelz4.Fast ...
type CompressionLevel = nativelz4.CompressionLevel
type Decoder struct{ ... }
    func NewDecoder(maxDecodedBytes int) *Decoder
type Encoder struct{ ... }
    func NewEncoder(level CompressionLevel) (*Encoder, error)
```

### `gnalloy.org/codec-compression/lzf`

包名：`lzf`

```text
var ErrCorruptFrame = errors.New("gnalloy/codec/compression/lzf: corrupt frame") ...
type Config struct{ ... }
type Decoder struct{ ... }
    func NewDecoder(config Config) (*Decoder, error)
type Encoder struct{ ... }
    func NewEncoder(config Config) (*Encoder, error)
```

### `gnalloy.org/codec-compression/lzma`

包名：`lzma`

```text
const DefaultDictCap = 1 << 20 ...
type Config struct{ ... }
type Decoder struct{ ... }
    func NewDecoder(maxDecodedBytes int, cfg Config) (*Decoder, error)
type Encoder struct{ ... }
    func NewEncoder(cfg Config) (*Encoder, error)
```

### `gnalloy.org/codec-compression/snappy`

包名：`snappy`

```text
var ErrInvalidFrame = errors.New("gnalloy/codec/compression/snappy: invalid framed chunk") ...
type Decoder struct{ ... }
    func NewDecoder(maxDecodedBytes int) *Decoder
type Encoder struct{ ... }
    func NewEncoder() *Encoder
type FrameDecoder struct{ ... }
    func NewFrameDecoder(cfg FrameDecoderConfig) *FrameDecoder
    func NewFramedDecoder(cfg FrameDecoderConfig) *FrameDecoder
type FrameDecoderConfig struct{ ... }
type FrameEncoder struct{ ... }
    func NewFrameEncoder() *FrameEncoder
    func NewFrameEncoderWithConfig(cfg FrameEncoderConfig) *FrameEncoder
    func NewFramedEncoder() *FrameEncoder
type FrameEncoderConfig struct{ ... }
```

### `gnalloy.org/codec-compression/zstd`

包名：`zstd`

```text
const SpeedFastest = nativezstd.SpeedFastest ...
type Decoder struct{ ... }
    func NewDecoder(maxDecodedBytes int) *Decoder
type Encoder struct{ ... }
    func NewEncoder(level EncoderLevel) (*Encoder, error)
type EncoderLevel = nativezstd.EncoderLevel
```
