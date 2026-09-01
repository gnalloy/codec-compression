# API Reference

[简体中文](api.zh-CN.md) | [Docs Index](README.md)

This inventory is generated from `go doc -short` for the packages in this repository. It is a quick public-surface map; source files and tests remain the authority for exact semantics.

## Packages

### `gnalloy.org/codec-compression`

Package name: `compression`

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

Package name: `brotli`

```text
const BestSpeed = nativebrotli.BestSpeed ...
type Decoder struct{ ... }
    func NewDecoder(maxDecodedBytes int) *Decoder
type Encoder struct{ ... }
    func NewEncoder(level int) (*Encoder, error)
```

### `gnalloy.org/codec-compression/bzip2`

Package name: `bzip2`

```text
const BestSpeed = nativebzip2.BestSpeed ...
type Decoder struct{ ... }
    func NewDecoder(maxDecodedBytes int) *Decoder
type Encoder struct{ ... }
    func NewEncoder(level int) (*Encoder, error)
```

### `gnalloy.org/codec-compression/fastlz`

Package name: `fastlz`

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

Package name: `stream`

```text
func ByteBufFromBytes(alloc buffer.Allocator, data []byte) (buffer.ByteBuf, error)
func DecodeAll(alloc buffer.Allocator, reader io.Reader, maxDecodedBytes int) (buffer.ByteBuf, error)
func NewByteBufReader(src buffer.ByteBuf) io.Reader
func WriteByteBuf(writer io.Writer, src buffer.ByteBuf) error
```

### `gnalloy.org/codec-compression/internal/testutil`

Package name: `testutil`

```text
func Buffer(data []byte) buffer.ByteBuf
func DecodeWithHandler(t *testing.T, decoder readHandler, compressed buffer.ByteBuf) buffer.ByteBuf
func EncodeWithHandler(t testing.TB, encoder writeHandler, payload []byte) buffer.ByteBuf
type Collector struct{ ... }
    func DecodeWithCollector(t testing.TB, decoder readHandler, compressed buffer.ByteBuf) *Collector
type Sink struct{ ... }
```

### `gnalloy.org/codec-compression/lz4`

Package name: `lz4`

```text
const Fast = nativelz4.Fast ...
type CompressionLevel = nativelz4.CompressionLevel
type Decoder struct{ ... }
    func NewDecoder(maxDecodedBytes int) *Decoder
type Encoder struct{ ... }
    func NewEncoder(level CompressionLevel) (*Encoder, error)
```

### `gnalloy.org/codec-compression/lzf`

Package name: `lzf`

```text
var ErrCorruptFrame = errors.New("gnalloy/codec/compression/lzf: corrupt frame") ...
type Config struct{ ... }
type Decoder struct{ ... }
    func NewDecoder(config Config) (*Decoder, error)
type Encoder struct{ ... }
    func NewEncoder(config Config) (*Encoder, error)
```

### `gnalloy.org/codec-compression/lzma`

Package name: `lzma`

```text
const DefaultDictCap = 1 << 20 ...
type Config struct{ ... }
type Decoder struct{ ... }
    func NewDecoder(maxDecodedBytes int, cfg Config) (*Decoder, error)
type Encoder struct{ ... }
    func NewEncoder(cfg Config) (*Encoder, error)
```

### `gnalloy.org/codec-compression/snappy`

Package name: `snappy`

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

Package name: `zstd`

```text
const SpeedFastest = nativezstd.SpeedFastest ...
type Decoder struct{ ... }
    func NewDecoder(maxDecodedBytes int) *Decoder
type Encoder struct{ ... }
    func NewEncoder(level EncoderLevel) (*Encoder, error)
type EncoderLevel = nativezstd.EncoderLevel
```
