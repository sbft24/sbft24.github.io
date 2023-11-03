---
title: SBFT'24 Java Competition Instructions
layout: md
---
# Java Test Case Generation Tool Competition

## Timeline (AoE)
* **01 Dec'23**: Tool submission.
* 04 Jan'24: Notification of the results for structural metrics (code coverage and mutation score).
* 18 Jan'24: Notification of the **smell** results.
* **25 Jan'24**: Camera-ready tool paper (4 pages, references included) deadline.
* 14 Apr'24: Official competition results and tool presentation live at SBFT workshop.


## Benchmarking Platform

The infrastructure concerning the Java tool competition is available on GitHub and can also be tried using Docker: [https://github.com/JUnitContest/JUGE](https://github.com/JUnitContest/JUGE).  Please refer to the GitHub repository for instructions.

**Related publication:**

```
@article{Devroey2022,
  author = {Devroey, Xavier and Gambi, Alessio and Galeotti, Juan Pablo and Just, René and Kifetew, Fitsum and Panichella, Annibale and Panichella, Sebastiano},
  title = {JUGE: An infrastructure for benchmarking Java unit test generators},
  journal = {Software Testing, Verification and Reliability},
  pages = {e1838},
  doi = {https://doi.org/10.1002/stvr.1838},
}
```

## Competition Process

It has been reported in the literature that automatically generated test cases are often affected by test-specific bad programming practices, i.e., **test smells**, that may hinder the quality of the test's source code and, ultimately, the quality of the code under test.

In this edition of the Java Tool Competition we will evaluate the *smelliness* of the generated test cases.  Intuitively, on one hand, a test case would be *smell-free* if no test smell (i.e., Mystery Guest, Eager Test, Assertion Roulette, Indirect Testing, Sensitive Equality, or Resource Optimism) is present in the test case.  On the other hand, a test case would be *smelly*, on a scale from 1 up to 6.  1 if it only contains one test smell, 2 if it contains any two smells, etc.

The assessment on whether a test case contains 0, 1, 2, 3, 4, 5, or 6 smells will be done by conducting a study with human evaluators who will annotate whether each of the six smells is or is not present in a random sample of generated test cases.  In a nutshell, we will follow the guidelines and the annotation protocol defined in the paper [Test smells 20 years later: detectability, validity, and reliability (Section 3.5)](https://link.springer.com/article/10.1007/s10664-022-10207-5).

The average smelliness score across this sample will count for 20% of the final score (which is used to rank the tools).

### 1. Tool submission (by 01 Dec'23 AoE)

Fill the Google form [https://forms.gle/1dLeo1JCgYqim8AP9](https://forms.gle/1dLeo1JCgYqim8AP9) and send a zip file with your tool to the organisers (please find their contacts at the end of this page).

### 2. Notification of the results for structural metrics (code coverage and mutation score) (by 04 Jan'24 AoE)

We will run our tool with the benchmark and you will receive by email the results of the code coverage and mutation score.  You will need these data to write the report (see point 4).

### 3. Notification of the smells results (by 18 Jan'24 AoE)

We will conduct an evaluation on the smelliness of your test cases.  We will send you a report on that, which you should also discuss in your report.

### 4. Tool report deadline (by 25 Jan'24 AoE)

You will need to submit a short report, which will be included in the workshop proceedings.  The report must follow the [IEEE conference format](https://www.ieee.org/conferences/publishing/templates.html).  The page limit is 2 pages including references.  Please submit the PDF to the organisers by the deadline (please find their contacts at the end of this page).

### 5. Results

Finally, the winners will be announced live during the workshop in April.


## Prizes and awards

Will be announced later. Stay tuned!


## Organizers

The Java tool competition is organized jointly by:
* [Valerio Terragni](https://valerio-terragni.github.io) (The University of Auckland, New Zealand) -- v.terragni@auckland.ac.nz
* [José Campos](https://jose.github.io) (University of Porto, Portugal) -- jcmc@fe.up.pt
