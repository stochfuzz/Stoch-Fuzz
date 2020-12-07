# StochFuzz

StochFuzz will be open-sourced upon acceptance. For now, we provide a compiled binary for purposes of demonstration. 

## Download 

Simply download the provided executable [stoch-fuzz](https://github.com/stochfuzz/Stoch-Fuzz/raw/main/stoch-fuzz).

## How to use

`stoch-fuzz` can be used in the same way as `afl-fuzz`. It supports all arguments of afl-fuzz except QEMU and dumb mode.

The only difference is, what you need to provide is a stripped binary instead of an instrumented one.

For example, if you want to fuzz a stripped binary named "libpng-1.2.56", with seed inputs in "seeds/" and fuzzing outputs in "output/", you can use:
```c
stoch-fuzz -i seeds -o output -- ./libpng-1.2.56 @@
```

More information can be found in the document of [AFL](https://github.com/google/AFL#6-fuzzing-binaries).

Here is a demo that shows how to use stoch-fuzz.

[![asciicast](https://asciinema.org/a/377835.svg)](https://asciinema.org/a/377835)

## Notes

+ Currently, stoch-fuzz only supports x64 ELF files.

+ This verion of stoch-fuzz can only be executed in the same directory as the target binary. For example, if you want to fuzz `$HOME/demo/libpng-1.2.56`, please change your working directory into `$HOME/demo`. Additionally, please use `stoch-fuzz -i seeds -o output -- ./libpng-1.2.56 @@` instead of `stoch-fuzz -i seeds -o output -- libpng-1.2.56 @@`

+ Although stoch-fuzz does support Position-independent code (PIC), there are some implementation bugs which make fuzzing PIC binaries failed. Hence, we remove this part of the implementation temporally, and will fix it as soon as possible.

+ The provided stoch-fuzz has been tested on Ubuntu 16.04, 18.04, and 19.04.
