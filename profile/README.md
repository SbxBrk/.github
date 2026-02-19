## SbxBrk

**SbxBrk** is an academic prototype for fuzzing the [V8 heap sandbox](https://v8.dev/blog/sandbox) through controlled fault injection. Built on [LibAFL](https://github.com/AFLplusplus/LibAFL), it instruments all memory loads crossing the security boundary between trusted and untrusted domains and injects faults via bitmasks before data from the heap sandbox reaches trusted code. Using SbxBrk, we discovered **19 security bugs** in V8's heap sandbox.

For the full details, see the paper: [SbxBrk](https://mschloegel.me/paper/bars2025sbxbrk.pdf).

### Repositories

| Repository | Description |
|---|---|
| [**SbxBrk**](https://github.com/SbxBrk/SbxBrk) | Main artifact — setup instructions, Docker environment, and orchestration for all components. Start here. |
| [**fuzzer**](https://github.com/SbxBrk/fuzzer) | The core fuzzer runtime written in Rust (built on LibAFL). Implements fault injection, mutation strategy, input scheduling, and sandbox-aware instrumentation. |
| [**V8**](https://github.com/SbxBrk/V8) | V8 build configuration and patches for compiling V8 with coverage instrumentation and sandbox-fuzzing support. |
| [**AFLplusplus**](https://github.com/SbxBrk/AFLplusplus) | Custom AFL++ fork with LLVM 21 support, used as the compiler for coverage instrumentation of the V8 target. |
| [**FuzzilliSbx**](https://github.com/SbxBrk/FuzzilliSbx) | Modified [Fuzzilli](https://github.com/googleprojectzero/fuzzilli) used as the baseline fuzzer for comparison in the paper's evaluation. |
| [**evaluation**](https://github.com/SbxBrk/evaluation) | Scripts and seed files for reproducing the bug-finding and coverage experiments from the paper. |

### Quick Start

The entire toolchain runs inside a Docker container (Ubuntu 24.04, x86_64). See the [main repository](https://github.com/SbxBrk/SbxBrk) for full setup and usage instructions.

```bash
git clone --recurse-submodules git@github.com:SbxBrk/SbxBrk.git
cd SbxBrk
./env/build.sh   # build the Docker environment
./env/start.sh   # enter the container
```

### Artifact

The version that received all three badges during artifact evaluation is also available on [Zenodo](https://zenodo.org/records/16994701).
