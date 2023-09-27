---
title: SBFT'24 Fuzzing Competition Instructions
layout: md
---

# Fuzzing Competition (C/C++ Programs)

## tl;dr

* Express your interest [here](https://forms.gle/bzbro1zAXoCxLBHd8) (Deadline: **AoE Friday 20 Jan 2023**).
* Write a fuzzer for C/C++ programs (or choose an existing fuzzer and _make your own novel modifications_).
* Maximize the number of bugs found and coverage achieved in 23 hours.
* Integrate fuzzer into [FuzzBench](https://google.github.io/fuzzbench/getting-started/adding-a-new-fuzzer/) (Deadline: **AoE Friday 17 Feb 2023**).
* Competition results will be reported live at SBST'23.


## Timeline
* 20 Jan'23: Registration deadline.
* 23 Jan'23: Notification of acceptance.
* 17 Feb'23: First Pull Request deadline (PR must be accepted at FuzzBench).
* 24 Mar'23: Preliminary results on public benchmarks.
* 03 Mar'23: Second Pull Request deadline.
* 10 Mar'23: Communicate final evaluation results to participants.
* 15 Mar'23: Camera-ready tool paper (4 pages, references included) deadline.
* May'23: Official competition results and tool presentation live at SBFT workshop.

## Benchmarking Platform
**Fuzzer**. The competing fuzzer must link against a [libFuzzer-style function](https://llvm.org/docs/LibFuzzer.html#fuzz-target) called
```C
int LLVMFuzzerTestOneInput(const uint8_t *Data, size_t Size);
```
which accepts an array `Data` of size `Size`. The objective of the fuzzer is to generate as many unique crashes as possible. The fuzzer can leverage any type of feedback from the executed program as guidance toward this objective.

For our competition, we use Google's [FuzzBench](https://google.github.io/fuzzbench) fuzzer evaluation platform [[ESEC/FSE'21]](https://research.google/pubs/pub50600/). FuzzBench provides an easy API for [integrating fuzzers](https://google.github.io/fuzzbench/getting-started/adding-a-new-fuzzer/) to contribute to painless, rigorous fuzzing research evaluations against a set of [benchmark programs](https://github.com/google/fuzzbench/tree/master/benchmarks) selected from real-world open-source projects and a set of [state-of-the-art fuzzers](https://github.com/google/fuzzbench/tree/master/fuzzers). FuzzBench allows conducting experiments locally and publicly. Once an experiment is concluded, it generates an [evaluation report](https://www.fuzzbench.com/reports/sample/index.html) with graphs and statistical tests to measure and visualize the effect size and statistical significance of the comparison across the chosen fuzzers and benchmark programs.

**Fuzzer Integration**. From the perspective of the fuzzer, FuzzBench provides generic access to:
* The *source code*, the *build process*, and the *executable* of the available benchmark programs.
* The *fuzz harnesses* which translate the fuzz inputs via `LLVMFuzzerTestOneInput` into executions of the programs,
* The *sanitizers* (i.e., detectors or oracles) that turn a buggy execution into a program crash. Bugs found by custom participant-specific sanitizers will be ignored.
* The *docker infrastructure* which
  * builds an arbitrary program with (your) fuzzer-specific instrumentation,
  * runs a specified set of fuzzers on a specified set of programs for a specified time,
  * collects code coverage and bug-finding information.

**Related work**
* [ESEC/FSE'21] "[FuzzBench: An Open Fuzzer Benchmarking Platform and Service](https://research.google/pubs/pub50600.pdf)",<br/> J. Metzman, L. Szekeres, L.M.R. Simon, R.T. Sprabery, and A. Arya.
* [ICSE'22] "[On the Reliability of Coverage-Based Fuzzer Benchmarking](https://mboehme.github.io/paper/ICSE22.pdf)"<br/> M. B&ouml;hme, L. Szekeres, and J. Metzman.
* [CCS'18] "[Evaluating Fuzz Testing](https://dl.acm.org/doi/10.1145/3243734.3243804)"<br/> G. Klees, A. Ruef, B. Cooper, S. Wei, M. Hicks



## Competition Process
**Registration** (by 20 January).
1. Please prepare a short "tool report" (up to 2 pages in [IEEE conference format](https://www.ieee.org/conferences/publishing/templates.html); `\documentclass[10pt,conference]{IEEEtran}` without including the compsoc or compsocconf options) describing the technology and ideas behind the fuzzer you want to submit to the competition. The tool report should be sent to sbft23fuzzcomp@googlegroups.com as part of the registration. Please format your email subject as '[Report submission] {Fuzzer Name}'.
2. Please open a pull request (PR) by [forking FuzzBench](https://github.com/google/fuzzbench/fork) and [submitting a PR](https://github.com/google/fuzzbench/compare). We encourage you to start early and check your code with our CI tests, but you can edit your PR at any time before the pull request deadline (17 Feb). Feel free to push the fuzzer implementation itself just right before the deadline. If there is any question regarding your PR, please let us know via sbft23fuzzcomp@googlegroups.com and format your email subject as '[PR Query] {Fuzzer Name}'.
3. Register [here](https://forms.gle/bzbro1zAXoCxLBHd8). For registration questions, please let us know via sbft23fuzzcomp@googlegroups.com and format your email subject as '[Registration query] {Fuzzer Name}'.


**Preliminaries**. First, we encourage every participant to get familiar with the [FuzzBench](https://github.com/google/fuzzbench) infrastructure. Create a [private fork](https://github.com/new/import) of the FuzzBench repository. Install [prerequisites](https://google.github.io/fuzzbench/getting-started/prerequisites/). You can now run one fuzzer (e.g., [`AFL`](https://github.com/google/fuzzbench/tree/master/fuzzers/afl)) on one program (e.g., [`libpng-1.2.56`](https://github.com/google/fuzzbench/tree/master/benchmarks/libpng-1.2.56)) using [`make run-afl-libpng-1.2.56`](https://google.github.io/fuzzbench/getting-started/adding-a-new-fuzzer/#testing-it-out). Get familiar with [fuzzer integration](https://google.github.io/fuzzbench/getting-started/adding-a-new-fuzzer/) to integrate your own fuzzer into FuzzBench. Get familiar with the [local setup](https://google.github.io/fuzzbench/running-a-local-experiment) to run multiple fuzzers, including yours, on multiple programs and get coverage and bug-finding reports.

**Preparation**. The participants are encouraged to use the [programs](https://github.com/google/fuzzbench/tree/master/benchmarks) and infrastructure available at FuzzBench for their [local evaluation](https://google.github.io/fuzzbench/running-a-local-experiment). The participants can submit new fuzzers, or extend existing fuzzers with their own novel ideas. The participants are allowed to modify the compilation of the programs to inject execution feedback for the fuzzer. During development, regularly make sure that [`make presubmit`](https://google.github.io/fuzzbench/getting-started/contributing-code/#running-unit-tests) succeeds and it can [build on benchmark programs](https://google.github.io/fuzzbench/getting-started/adding-a-new-fuzzer/#testing-it-out). It can be quite pedantic and you don't want to be failed due to trivial errors.

**Pull Request Deadline** (on 17 February 2023).
* The participants publicly integrate their fuzzers into FuzzBench by submitting a [Pull Request](https://github.com/google/fuzzbench/pulls) and getting it approved for integration. We will only consider fuzzers that passed all CI tests in the PR and that run for at least 30 minutes.

* The primary contact of the participants' team submits a short tool report (up to 2 pages in [IEEE conference format](https://www.ieee.org/conferences/publishing/templates.html); `\documentclass[10pt,conference]{IEEEtran}` without including the compsoc or compsocconf options) describing the technology and ideas behind the submitted fuzzer and the experience of integrating into FuzzBench.


**Results**. Finally, the winners will be announced live during the workshop in May.

## Prizes and awards
Top-performing participants will be eligible to be considered for a new OSS-Fuzz [**_FuzzBench integration reward_**](https://bughunters.google.com/about/rules/5097259337383936/oss-fuzz-reward-program-rules) (up to $11,337, depending on impact).

## Organizers
The fuzzing competition is organized jointly by Abhishek Arya (Google), Oliver Chang (Google), Jonathan Metzman (Google), Dongge Liu (Google), and Marcel Böhme (MPI-SP).

### Google Open Source Security Team (GOSST)
[Abhishek Arya](https://twitter.com/infernosec), [Oliver Chang](https://twitter.com/halbecaf), [Jonathan Metzman](https://twitter.com/metzmanj?lang=en), and [Dongge Liu](https://twitter.com/Alan32Liu) are with the Google Open Source Security Team (GOSST). The team works to improve the security of open-source software that Google and the world rely on. The team's [FuzzBench](https://google.github.io/fuzzbench/) provides a free service for researchers to [rigorously evaluate fuzzers](https://www.fuzzbench.com/reports/sample/index.html) on a wide variety of [real-world benchmarks](https://github.com/google/fuzzbench/tree/master/benchmarks) at Google's scale. The team's [ClusterFuzz](https://google.github.io/clusterfuzz/) and [OSS-Fuzz](https://google.github.io/oss-fuzz/) projects combine modern fuzzing techniques with scalable, distributed execution to make widely used open source software more secure and stable. GOSST also contributes to hardening the open-source supply chain with [SLSA](https://slsa.dev/), [Sigstore](https://www.sigstore.dev/), and projects in collaboration with the [Open Source Security Foundation](https://openssf.org/).

### Marcel Böhme (MPI-SP)
Marcel Böhme leads the Software Security research group at the Max Planck Institute for Security and Privacy (MPI-SP) in Germany. His current research interest is the automatic discovery of security flaws at a very large scale. One part of his group develops the probabilistic foundations of automatic software testing (i.e., finding bugs by generating executions) to elucidate fundamental limitations of existing techniques and to explore the assurances that software testing provides when no bugs are found. The other part of his group develops practical vulnerability discovery tools that are widely used in software security practice.
