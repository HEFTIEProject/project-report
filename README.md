# HEFTIE final report

This is the final report for the [Handling Enourmous Files from Tomography Imaging Experiments (HEFTIE) project](https://oscars-project.eu/projects/heftie-handling-enormous-files-tomographic-imaging-experiments), an EU funded project to improve tools and educational resources for handling huge imaging datasets.
We hope these new resources will accelerate the analysis of 3D organ scans and unlock discoveries in the life sciences, benefiting also other fields, such as neuroscience, archaeology, and the earth sciences.

## Digital textbook

We created a new digital textbook, called [Handling Enormous Files from 3D Imaging Experiments](https://heftie-textbook.readthedocs.io/).
This textbook gives scientists:

- an introduction to the motivation and theory behind chunked datasets
- a practical introduction to creating chunked datasets, and the configuration options available
- a guide to designing parallel processing algorithms to work efficiently with chunked datasets
- a guide to exporting chunked datasets to other 'tradditional' datasets

## Benchmarking for Zarr

We created a set of benchmarks for writing data to Zarr with a range of different configurations as guidance for the options available when reading and writing 3D imaging data.
The different parameters were:

- Type of image
  - Heart: HiP-CT scan of a heart from the Human Organ Atlas
  - Dense: segmented neurons from electron microscopy
  - Sparse: A few select segmented neurons from electron microscopy
- Software libraries
  - Tensorstore (fastest for both reading and writing data)
  - zarr-python version 3
  - zarr-python version 2 (slowest for both reading and writing data)
- Compressor
  - blosc-zstd provides the best compression ratio, for image and segmentation data. (options were blosc-blosclz, blosc-lz4, blosc-lz4hc, blosc-zlib, blosc-zstd as well as gzip and zstd)
- Compression level
  - Setting compression levels beyond ~3 results in slightly better data compression but much longer write times. Compression level does not affect read time.
- Shuffle
  - Setting the shuffle option increases data compression with no adverse effect on read/write times (shuffle, bitshuffle and noshuffle were the 3 options)
- Zarr format version
  - There was no noticeable difference between Zarr format 2 and Zarr format 3 data
- Chunk size
  - Setting a low chunk size (below around 90) has an adverse effect on read and write times.

## Tools for working with chunked datasets

Contributions have been made to the zarr-python repository:

- [Add CLI for converting v2 metadata to v3](https://github.com/zarr-developers/zarr-python/pull/3257)
- [Added ArrayNotFoundError](https://github.com/zarr-developers/zarr-python/pull/3367)

PRs have been opened in the zarr-python repository:

- [Prevent creation of arrays/groups under a parent array](https://github.com/zarr-developers/zarr-python/pull/3407)
- [Holding space - Better document acceptable values for StoreLike]
- [Holding space - LRUStoreCache]

PRs have also been opened for:

- [Document supported file formats for dask_image.imread](https://github.com/dask/dask-image/issues/407)
- [Document supported file formats for skimage.io](https://github.com/scikit-image/scikit-image/issues/7879)

## Improvements to cloud visualisation

## Acknowledgements
