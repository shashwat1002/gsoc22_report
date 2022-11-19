# Introduction

The project was to port the hardsubx module of ccextractor. Hardsubx is a Tesseract based OCR module that extracts subtitles that are burnt-in the frames. 

I was tasked with porting the whole module to Rust. My contributions can be summarized as the following components:

- Making memory safe versions of utility functions in Rust
- Compatibility with FFMPEG 5
  - Dealing with depercated and outdated struct definitions
  - Replacing depercated functions with code that gives equivalent functioning
- Fixing bugs in the original module
- Rewriting structs to use more Rust native features for better safety 

I will be talking about the work involved in each of the divisions on a section by section basis.

All PR's for ccextractor: https://github.com/CCExtractor/ccextractor/pulls?q=is%3Apr+author%3A%40me

# Contributions

## Performance improvement

There has been a slight improvement in the performance of the hardsubx module because some image transformation functions have been corrected.

## Memory safe utility functions in Rust

Algorithms like Levanstein distance and other utility algorithms were re-written in Rust. 

 

## Compatibility with FFMPEG5

FFMPEG is a rapidly changing library and between the version of FFMPEG version being used by Hardsubx originally and FFMPEG 5 there had been a lot of breaking changes. 

Notably, the definition of the struct `AVPacket`. This led to several insidious bugs when my Rust re-write was expecting a different memory allocation than the one it was receiving.

Furthermore, a few functions being used by the Hardsubx were depercated with no obvious way to replace them. 

## Rewriting structs in Rust

A lot of safety issues could only be resolved if all the structs of the hardsubx module were re-written. 

# Challenges

The biggest challenge was dealing with the version change of FFMPEG.

FFMPEG has made a lot of breaking changes since the original hardsubx, depercated functions do not often have direct replacements and the documentation is not always clear on how the depercated function should be replaced.

Other than that, during the course development, I had to deal with C strings in Rust and general memory safety problems that come packaged with it.

Other challenges included memory safety related code with C strings. A lot of the work involved sending to and receiving strings from C functions.





