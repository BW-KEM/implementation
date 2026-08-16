# BW-KEM Reference Implementation

This repository contains the reference C implementation of **BW-KEM**, an
MLWE-based key encapsulation mechanism using Barnes--Wall lattice coding for
error correction. It accompanies the submission and provides the implementation
used for the performance evaluation reported in the paper.

The implementation includes the three recommended parameter sets:

- BW-KEM-512,
- BW-KEM-768,
- BW-KEM-1024.

The main implementation of the Barnes--Wall lattice coding layer is contained
in `ref/BWcoding.c`.

## Repository Structure

```text
.
├── ref/
│   ├── BWcoding.c              # Barnes--Wall lattice encoding and decoding
│   ├── BWcoding.h
│   ├── kem.c                   # KEM implementation
│   ├── indcpa.c                # Underlying IND-CPA-secure PKE
│   ├── params.h                # Parameter definitions
│   ├── test/                   # Correctness and cycle-counting benchmarks
│   ├── nistkat/                # NIST-style known-answer tests
│   └── Makefile
├── README.md
└── LICENSE
```

## Requirements

The reference implementation requires:

- a C compiler such as GCC;
- GNU Make.

Building the NIST-style known-answer tests additionally requires OpenSSL.

## Building

Clone the repository and enter the reference implementation directory:

```bash
git clone https://github.com/BW-KEM/implementation.git
cd implementation/ref
```

Build all tests, benchmarks, shared libraries, and known-answer-test programs:

```bash
make
```

Individual targets can also be built using:

```bash
make test
make speed
make shared
make nistkat
```

To remove generated files:

```bash
make clean
```

## Correctness Tests

Build the correctness tests using:

```bash
make test
```

and run:

```bash
./test/test_kyber512
./test/test_kyber768
./test/test_kyber1024
```

The three executables correspond to BW-KEM-512, BW-KEM-768, and
BW-KEM-1024, respectively.

The `kyber` naming of several source files and test binaries is inherited from
the underlying Kyber/ML-KEM reference implementation.

## Benchmarking

Build the cycle-counting benchmarks using:

```bash
make speed
```

and run:

```bash
./test/test_speed512
./test/test_speed768
./test/test_speed1024
```

The benchmark programs report median CPU cycle counts over 10,000 executions
for the main polynomial operations and the complete KEM operations, including
key generation, encapsulation, and decapsulation.

The benchmark results reported in the paper were obtained on an
Intel(R) Core(TM) i7-11700F @ 2.50 GHz with Hyperthreading and TurboBoost
disabled. The code was compiled using GCC 11.4.0 with optimization level `-O3`.

## Security and DFR Evaluation

Scripts used to estimate the concrete MLWE security and decryption-failure
rates of the BW-KEM parameter sets are provided in the companion repository:

```text
https://github.com/BW-KEM/evaluation
```

## Third-Party Acknowledgment

This implementation is based on the reference implementation of
CRYSTALS-Kyber:

```text
https://github.com/pq-crystals/kyber
```

The original codebase was adapted to incorporate the Barnes--Wall lattice
coding mechanism and the parameter sets used in BW-KEM. The original authors
and contributors retain attribution for the portions derived from their work.

## Citation

When referring specifically to the reference implementation, please cite this
repository:

```text
https://github.com/BW-KEM/implementation
```
