# Overview

[简体中文](overview.zh-CN.md) | [Docs Index](README.md)

## Purpose

Compression codecs for Gnalloy pipelines, including gzip, zlib, brotli, snappy, lz4, zstd, bzip2, lzma, FastLZ, and LZF.

This module sits above transports and below application handlers. It translates bytes or Gnalloy messages into protocol objects, and translates outbound protocol objects back to bytes. It does not open sockets or own EventLoops.

## Repository Identity

- Module path: `gnalloy.org/codec-compression`
- GitHub repository: `github.com/gnalloy/codec-compression`
- Default branch: `dev`
- License: Apache-2.0

## Package Map
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

## Direct Gnalloy Dependencies
- `gnalloy.org/gnalloy`

## Direct Dependents in the Current Module Plan
- `gnalloy.org/codec-http1`
- `gnalloy.org/codec-http2`

## Architecture Position

Gnalloy keeps the core small and dependency-light. This repository is a replaceable module around one responsibility, connected through explicit Go packages instead of runtime discovery.

## Compatibility

The public import path is `gnalloy.org/codec-compression`. Until the first stable tag is published, use `@dev` or an explicit pseudo-version selected by your dependency policy.
