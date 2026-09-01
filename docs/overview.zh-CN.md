# 概览

[English](overview.md) | [文档索引](README.zh-CN.md)

## 目标

Gnalloy Pipeline 的压缩/解压编解码器，覆盖 gzip、zlib、brotli、snappy、lz4、zstd、bzip2、lzma、FastLZ 与 LZF。

该模块位于 transport 之上、业务 handler 之下，负责把字节或 Gnalloy 消息转换成协议对象，并把出站协议对象转换回字节。它不打开 socket，也不拥有 EventLoop。

## 仓库身份

- 模块路径：`gnalloy.org/codec-compression`
- GitHub 仓库：`github.com/gnalloy/codec-compression`
- 默认分支：`dev`
- 许可证：Apache-2.0

## 包结构
- `gnalloy.org/codec-compression`（`compression`）
- `gnalloy.org/codec-compression/brotli`（`brotli`）
- `gnalloy.org/codec-compression/bzip2`（`bzip2`）
- `gnalloy.org/codec-compression/fastlz`（`fastlz`）
- `gnalloy.org/codec-compression/internal/stream`（`stream`）
- `gnalloy.org/codec-compression/internal/testutil`（`testutil`）
- `gnalloy.org/codec-compression/lz4`（`lz4`）
- `gnalloy.org/codec-compression/lzf`（`lzf`）
- `gnalloy.org/codec-compression/lzma`（`lzma`）
- `gnalloy.org/codec-compression/snappy`（`snappy`）
- `gnalloy.org/codec-compression/zstd`（`zstd`）

## 直接 Gnalloy 依赖
- `gnalloy.org/gnalloy`

## 当前模块规划中的直接下游
- `gnalloy.org/codec-http1`
- `gnalloy.org/codec-http2`

## 架构位置

Gnalloy 保持核心小而轻依赖。本仓库围绕单一职责形成可替换模块，通过显式 Go package 连接，而不是依靠运行时发现。

## 兼容性

公共导入路径是 `gnalloy.org/codec-compression`。首个稳定 tag 发布前，请按依赖策略使用 `@dev` 或明确的 pseudo-version。
