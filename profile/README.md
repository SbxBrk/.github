## SbxBrk

<p><a href="https://mschloegel.me/paper/bars2025sbxbrk.pdf"><img alt="SbxBrk Paper" align="right" width="320" src="paper_preview.png"></a></p>

**SbxBrk** is an academic prototype for fuzzing the [V8 heap sandbox](https://v8.dev/blog/sandbox) through controlled fault injection. Built on [LibAFL](https://github.com/AFLplusplus/LibAFL), it instruments all memory loads crossing the security boundary between trusted and untrusted domains and injects faults via bitmasks before data from the heap sandbox reaches trusted code. Using SbxBrk, we discovered **19 security bugs** in V8's heap sandbox.

For the full details, see the paper: [SbxBrk](https://mschloegel.me/paper/bars2025sbxbrk.pdf).

<br clear="right"/>

### Citation
If you use SbxBrk in your research, please cite our paper:
```bibtex
@inproceedings{10.1145/3719027.3765027,
  author = {Bars, Nils and Bernhard, Lukas and Schloegel, Moritz and Holz, Thorsten},
  title = {Empirical Security Analysis of Software-based Fault Isolation through Controlled Fault Injection},
  year = {2025},
  isbn = {9798400715259},
  publisher = {Association for Computing Machinery},
  address = {New York, NY, USA},
  url = {https://doi.org/10.1145/3719027.3765027},
  doi = {10.1145/3719027.3765027},
  booktitle = {Proceedings of the 2025 ACM SIGSAC Conference on Computer and Communications Security},
  pages = {2639–2652},
  numpages = {14},
  keywords = {browser security, fuzzing, software-based fault isolation},
  location = {Taipei, Taiwan},
  series = {CCS '25}
}
```

### Repositories

| Repository | Description |
|---|---|
| [**SbxBrk**](https://github.com/SbxBrk/SbxBrk) | Main artifact — setup instructions, Docker environment, and orchestration for all components. Start here. |
| [**fuzzer**](https://github.com/SbxBrk/fuzzer) | The core fuzzer runtime written in Rust (built on LibAFL). Implements fault injection, mutation strategy, input scheduling, and sandbox-aware instrumentation. |
| [**V8**](https://github.com/SbxBrk/V8) | V8 fork with build configuration and the [`heap_sandbox_fuzzing_pass`](https://github.com/SbxBrk/V8/tree/main/heap_sandbox_fuzzing_pass) — a custom LLVM pass that instruments heap sandbox memory loads for fault injection. |
| [**AFLplusplus**](https://github.com/SbxBrk/AFLplusplus) | Custom AFL++ fork with LLVM 21 support, used as the compiler for coverage instrumentation of the V8 target. |
| [**FuzzilliSbx**](https://github.com/SbxBrk/FuzzilliSbx) | Modified [Fuzzilli](https://github.com/googleprojectzero/fuzzilli) used as the baseline fuzzer for comparison in the paper's evaluation. |
| [**evaluation**](https://github.com/SbxBrk/evaluation) | Scripts and seed files for reproducing the bug-finding and coverage experiments from the paper. |

### Quick Start

The entire toolchain runs inside a Docker container (Ubuntu 24.04, x86_64). See the [main repository](https://github.com/SbxBrk/SbxBrk) for full setup and usage instructions.

```bash
git clone --recurse-submodules https://github.com/SbxBrk/SbxBrk.git
cd SbxBrk
./env/build.sh   # build the Docker environment
./env/start.sh   # enter the container
```

### Artifact

The version that received all three badges during artifact evaluation is also available on [Zenodo](https://zenodo.org/records/16994701).
