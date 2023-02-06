# Go HLS Transcoder

[![GoDoc](https://godoc.org/github.com/azanium/go-transcoder?status.svg)](https://godoc.org/github.com/azanium/go-transcoder)

Golang transcoder using ffmpeg

## Supports
- [x] HTTP Live Streaming
- [ ] MPEG DASH

## Prerequisite

- Golang 1.14
- ffmpeg

## Examples

Generate HLS files + playlist from a mov file.

```go
package main

import (
	"os/exec"

	"github.com/azanium/go-transcode/hls"
)

func main() {
	srcPath := "./Love.mov"
	targetPath := "hls/"
	resOptions := []string{"480p", "720p"}
	ffmpeg, err := exec.LookPath("ffmpeg")
	if err != nil {
		panic(err)
	}

	variants, _ := hls.GenerateHLSVariant(resOptions, "")
	hls.GeneratePlaylist(variants, targetPath, "")

	for _, res := range resOptions {
		hls.GenerateHLS(ffmpeg, srcPath, targetPath, res)
	}
}
```

## License

MIT licensed. See the LICENSE.md file for details.
