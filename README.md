# Multispectral and hyperspectral imagery compression

These are brainstorming notes for requirements for an image format for lossless compression of multispectral and hyperspectral images.
See [references.md](references.md) for a list of articles and sample data.

## Use cases
* Archiving satellite imagery
* Viewing satellite imagery in desktop GIS tools
* Rendering satellite imagery in web tools
* Processing satellite imagery in analysis tools

### Other potential use cases
* Compressing remote sensing data before transmission
* Archiving, viewing and processing medical imagery
* Archiving, viewing and processing scientific imagery

## Requirements

### Required features for the algorithm and the file format
* support for multiple channels
* support for lossless compression
* support for 8 bit (uint8) and 16 bit (uint16) data.
* support for metadata:
  * georeferencing
  * XMP (as in geotiff files) and exif (as in jpeg files)
  * lossless metadata (converting from a GeoTiff and back preserves metadata)
* tile support (for fast viewing)
* interlacing support (like Adam7) AND/OR pyramid support (for fast viewing at lower resolutions)

### General requirements
* has to be "free"
  * not patent encumbered
  * OSI approved open source license
* has to be "simple"
  * means "design the algorithm and the implementation such that as little as possible documentation is needed to fully document the algorithm and the implementation", in other words, "if it is fundamentally hard to explain it's not simple"
  * implies making elegant choices and writing clean code.
* has to be "well documented"
  * means "not lacking any vital documentation"
  * implies documented code for the reference implementation
* has to be "reliable"
  * needs complete test suite including fuzzying
  * needs real world testing


### Desired features
* reuse open formats and standards as much as possible.
  * do not reinvent the wheel where a good solution already exists.
* use an open container like [Matroska](https://github.com/Matroska-Org/libmatroska) or RIFF (like [webp](https://developers.google.com/speed/webp/docs/riff_container)) and take advantage of the metadata infrastructure that those containers provide.
* support for a "no data" value (equivalent to an alpha channel with full transparency, but maybe embeddable in the data itself
* support for different resolutions for different channels (hard!)
* support for different bit dephts for different channels (hard)
* support for metadata for individual channels (bit depth, type of data)
* custom metadata
  * meta metadata - an embedded documentation of the custom metadata (no more undocumented "vendor tags")
* support for 32-bit floating point (float32) data
* support for signed integer data
* no intrinsic limits on number of bands
* compression at least in the same ballpark as JPEG2000 and hopefully [FLIF](https://github.com/FLIF-hub/FLIF)
* support for lossy compression without generation loss (as in [FLIF](https://github.com/FLIF-hub/FLIF))
* implementation of the "time" dimension (animation/movie, but with time tagged frames)
  * seek to time
  * intra frames compression
  * hyperspectral video



### Random notes
* take a look into video codecs. will not meed all requirements but may provide insights into compressing hyperspectral images (original idea sprouted from [a discussion in the FLIF repository](https://github.com/FLIF-hub/FLIF/issues/312), Jon suggested using an animation to encode multiple bands, I wonder why not use a video codec then?)
* take a look into other image formats
  * jpeg2000 has great implementations, but is not free
  * FLIF supports only three spectral channels plus an alpha channel (RGBA)
  * WebP also supports only RGBA
  * Geotiff has poor compression (check again, maybe it has other options).
