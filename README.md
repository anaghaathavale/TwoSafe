# TwoSafe

TwoSafe verifies symmetric and asymmetric confidence-based global robustness of ReLU DNNs using differential halo zonotopes. It accompanies the paper "Differential Zonotopes for Verifying Global Robustness of DNNs" and is built on [VeryDiff](https://github.com/samysweb/VeryDiff).

## Installation

Requirements:
- Julia 1.10
- Gurobi (free academic license available at gurobi.com)

Clone this repository, start Julia in its directory, and run:

```julia
using Pkg
Pkg.activate(".")
Pkg.instantiate()
Pkg.build("VeryDiff")
```

## Running the tool

The binary is built to `./deps/VeryDiff/bin/VeryDiff` (called `<BINARY>` below).

```
usage: 

For asymmetric property:
<BINARY> [NETWORK] - [SPEC_FILE] [--robustness-delta DELTA] [--input-epsilon EPS] [--timeout TIMEOUT]

For symmetric property:
<BINARY> [NETWORK] - [SPEC_FILE] [--robustness-delta-symmetric DELTA] --robustness-delta-symmetric-N2 DELTA] [--input-epsilon EPS] [--timeout TIMEOUT]

NETWORK: NN file (onnx)
SPEC_FILE: Specification file (vnnlib)
```
### Absolute confidence gap
To specify the confidence as an absolute gap between the largest and second-largest output (instead of a probability), use --robustness-abs-delta:

```
julia --project cli.jl model_flat.onnx - test/examples/specs/mnist_global.vnnlib --robustness-abs-delta 13.815509558 --input-epsilon 0.1
```
Note that the hyphen (-) between [NETWORK] and [SPEC_FILE] is required

The benchmarks and specification files are under /experiments

## License

MIT, see LICENSE.
