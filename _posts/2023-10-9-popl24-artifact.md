---
layout: simple
title:  "POPL-24 Artifact Evalation - Yuantian Ding"
---

# POPL-24 Artifact Evaluation - Yuantian Ding

## Claims in the paper

* Biten outperforms CVC4, Probe, Duet, and Simba on all the 3 benchmark sets.
* Biten generated smaller solution for Case-splitting and Deobfuscation Benchmark
* Ablation Studies:
    * LLM-guidance and Bottom-up Deduction can effectively increase the solving rate of Hacker's Delight Benchmark.
    * Bottom-up Deduction and Graph-based enumeration can increase the performance for Case-splitting Benchmark.
    * Bottom-up Deduction can increase the solving rate for Deobfuscation Benchmark.

Note: Biten is a name for our anonymous submission. Biten is actually part of our general SyGuS solver DryadSynth.

## Download, and installation

The only file you need to download is `BitenArifact.ova`, you can download this file from [OneDrive](https://purdue0-my.sharepoint.com/:u:/g/personal/ding360_purdue_edu/EeAL4PYsLThDkEdLB_iLOLsBS0_6oVxFqA659VS0RPz89g?e=eTOsw1).

The image can be loaded by VirtualBox 7. We recommend using at least 4 CPUs and at least 8 GB memory. 

Once the VM starts, it can be logged in with `username: virtualbox` and `password: changeme` via SSH at localhost:2222. You can also use [VS Code Remote SSH](https://code.visualstudio.com/docs/remote/ssh) to connect to the VM.

All related files are under the directory `/home/virtualbox/artifact`. Everything is installed in the VM, no need to run any compilation.

Here is the structure of `/home/virtualbox/artifact` Directory:

```
artifact/
    scripts/    all scripts you need to run the test
    benchmarks/     All 3 benchmark sets
    solvers/    4 solvers used in the test
    clean.sh    remove all files generated during testing 
    README.md   a copy this file (without OneDrive link)
```

## Evaluation instructions

### Hacker's Delight Benchmark

Solving hacker's delight benchmarks involves interaction with a large language model. So please set up your openai api key for `gpt-turbo-3.5`. To test the effectiveness of LLM-guided enumeration, please set OPENAI_API_KEY in the environment variable:

```bash
export OPENAI_API_KEY=<your key>
```

Use the following to run all the Hacker's Delight Benchmark (Ablation Study included) for all solvers and all configurations. It will be pretty slow because OpenAI have rate limits about 150,000 token per minutes. If we run Biten multiple times continueously, ChatGPT will reach its limit. So the testing program will `sleep` some time to work around this limit.

```bash
python3 scripts/bench.py hd-run
```

All results are generated in `json` file under `results/`. The process can be interruped in the middle, all tested results will be saved in `results` directory. You can restart the process by running `scripts/bench.py hd-run` again. All tested results will be skipped. To rerun the whole test, please `rm -r results` and run `scripts/bench.py hd-run` again.

Generate figures for each configuration:

```bash
python3 scripts/bench.py hd-draw
```

`hd-1.png`, `hd-2.png`, `hd-dc-1.png`, `hd-dc-2.png` will be created in the working deriectory.

### Case-splitting PBE Benchmark


Run all the Case-splitting PBE Benchmark Benchmark for all solvers and all configurations:

```
python3 scripts/runbench.py run
```

All results are generated in `json` file under `result0/`. 

Generate all data in CSV using the following command:

```
python3 scripts/bench.py to-csv
```

It will compose all json data into `results.csv`. It will also generate figure `sygus-time.png`, `sygus-size.png` which compare each solver on time and size.

### Deobfuscation Benchmark

Run all the Deobfuscation Benchmark Benchmark for all solvers and all configurations:

```
python3 scripts/runbench.py run-deobfusc
```

All results are generated in `json` file under `result1/`. 

Generate all data in CSV with the following command:

```
python3 scripts/runbench.py to-csv-2
```

It will compose all json data into `results1.csv`. It will also generate figure `deobfusc-time.png`, `deobfusc-size.png` which compare each solver on time and size.


`python3 scripts/runbench.py draw-scatter` will draw ablation study figures for Bottom-up deduction and Expedited enumeration. There are 4 figures generated from this command:

* `sygus-deduct.png`: Case-splitting benchmark W/ and W/o Bottom-up Deduction
* `sygus-graph.png`: Case-splitting benchmark W/ and W/o Graph-based Enumeration
* `deobfusc-deduct.png`: Deobfuscation benchmark W/ and W/o Bottom-up Deduction
* `deobfusc-graph.png`: Deobfuscation benchmark W/ and W/o Graph-based Enumeration

### Testting a Single Benchmark Manuelly

Biten's executable is located at `solvers/biten/biten`. A TOML file can be passed into `biten` for configuration using the following command:

```bash
biten -c <config-file> <sygus-if-file>
```

In `solvers/biten/config`, there are a lot of commonly used configuration files. Here is the default configuration file for PBE problems with explanation of each parameters:

```toml
random_example = 10 # How many additional random examples are generated from reference implementation 
limited_ite = false # Limit ITE condition search size to 10000 
ite_tree_limit = 30 # Limit the size of decition tree
chatgpt = true # Disable/Enable ChatGPT
smt_solver = "bitwuzla" # Using command bitwuzla as SMT-Solver. Require `bitwuzla` command installed

[expr_search]
sample = 64 # The number of sampling
dag_size = true # Enable Graph-Based Enumeration
filter = {
    deductive_combine = true, # Enable/Disable deduction for AND and OR
    deductive_reverse = true  # Enable/Disable deduction for XOR and ADD
} 
```

`-v` flag can be passed into `biten` command to display log information.


## Additional Information

* Testing all Deobfuscation benchmarks for all solver set and all configurations will cost 6 hours or more.
* To check if the benchmarks run as expected, we provide a list of our experimental results in our [Appendix](https://dnailz.github.io/assets/appendix.pdf).
* You can lookup any specific result in the results/ folder, each json file is in the following format:
    ```
    {
        "status": <"success" if the command returns 0, otherwise it could be "error" and "timeout">
        "stdout": <STDOUT>,
        "stderr": <STDERR>,
        "time": <time for the execution>
        "command": <command for the execution>,
    }
    ```
* For questions, please email me at ding360@purdue.edu. I will be happy to help you with any problems.
