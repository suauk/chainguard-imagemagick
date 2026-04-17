# Chainguard ImageMagick

A multi-stage Docker build for ImageMagick 7 using Chainguard's secure base images.

## Overview

This repository provides a Dockerfile that builds ImageMagick 7 from source using `cgr.dev/chainguard/jre:latest-dev` as the base image. The multi-stage build ensures the final image only contains runtime dependencies, not build tools.

## Features

ImageMagick is configured with the following delegates:

| Feature | Description |
|---------|-------------|
| bzlib | BZip2 compression |
| fontconfig | Font configuration |
| freetype | Font rendering |
| heic | HEIF/HEIC image format |
| gslib | Ghostscript library |
| gvc | GraphViz support |
| jpeg | JPEG image format |
| openjp2 | JPEG 2000 support |
| png | PNG image format |
| tiff | TIFF image format |
| xml | XML support |
| lcms | Color management |
| webp | WebP image format |
| fftw | Fourier transforms |
| pango/cairo | Text rendering |
| openexr | OpenEXR HDR format |

## Build

```bash
docker build -t imagemagick:latest .
```

## Usage

### Check version

```bash
docker run --rm imagemagick:latest -version
```

### Convert an image

```bash
docker run --rm -v $(pwd):/work -w /work imagemagick:latest convert input.png output.jpg
```

### Resize an image

```bash
docker run --rm -v $(pwd):/work -w /work imagemagick:latest convert input.jpg -resize 50% output.jpg
```

### Create a thumbnail

```bash
docker run --rm -v $(pwd):/work -w /work imagemagick:latest convert input.jpg -thumbnail 100x100^ -gravity center -extent 100x100 thumbnail.jpg
```

### Convert to WebP

```bash
docker run --rm -v $(pwd):/work -w /work imagemagick:latest convert input.png -quality 80 output.webp
```

### List supported formats

```bash
docker run --rm imagemagick:latest identify -list format
```

### List delegates

```bash
docker run --rm imagemagick:latest identify -list delegate
```

## Security

- Built on Chainguard's hardened base images
- Multi-stage build minimizes attack surface
- Runs as non-root user (UID 65532) by default
- All package versions are pinned for reproducibility

## Package Versions

All packages are pinned to specific versions for reproducible builds. See the [Dockerfile](Dockerfile) for the complete list of pinned versions.

## License

This Dockerfile and associated documentation are provided under the MIT License.

ImageMagick itself is distributed under the [ImageMagick License](https://imagemagick.org/script/license.php).
