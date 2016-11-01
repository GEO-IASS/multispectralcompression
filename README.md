# multispectralcompression
These are brainstorming notes for requirements for an image format for lossless multispectral and hyperspectral images.

Use cases:
* Archiving satellite imagery
* Viewing satellite imagery in desktop GIS tools
* Rendering satellite imagery in web tools
* Processing satellite imagery in analysis tools

Required features:
* support for multiple spectral channels
* support for lossless compression
* support for 8 bit (uint8) and 16 bit (uint16) data.
* support for metadata:
  * georeferencing
  * XMP (as in geotiff files) and exif (as in jpeg files)
  * lossless metadata (converting from a GeoTiff and back preserves metadata)
* tile support (for fast viewing)
* interlacing support (like Adam7) AND/OR pyramid support (for fast viewing at lower resolutions)
* has to be "simple"
  * implies making elegant choices and writing clean code.
  * implies "needing as small as possible documentation to fully document the algorithm and the implementation"
* has to be "well documented"
  * means "not lacking any vital documentation"
  * implies documented code for the reference implementation


Desired features:
* support for a "no data" value (equivalent to an alpha channel with full transparency, but maybe enbeddable in the data itself
* support for different resolutions for different channels (hard!)
* support for different bit dephts for different channels (hard?)
* support for metadata for individual channels (bit depth, type of data)
* custom metadata
  * meta metadata - an embedded documentation of the custom metadata (no more undocumented "vendor tags")
* support for 32-bit floating point (float32) data
* support for signed integer data
* no intrinsic limits on number of bands
* compression at least in the same ballpark as JPEG2000 and hopefully [FLIF](https://github.com/FLIF-hub/FLIF)
* support for lossy compression without generation loss (as in [FLIF](https://github.com/FLIF-hub/FLIF))
* implementation of the "time" dimension (film, but with time tagged frames)
  * seek to time
  * intra frames compression
  * hyperspectral video

Potential use cases:
* Compressing remote sensing data before transmission
* Archiving medical imagery
* Archiving scientific imagery
