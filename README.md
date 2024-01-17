# From Zero to Hero: Conquering the Arm Neoverse

--- 

#### Scope 

This hands-on tutorial aims to teach high-level participants how to compile, execute, profile and optimize scientific and technical computing workloads on modern and capable Arm Neoverse CPUs, in particular AWS Graviton 3/3E. The presenters will cover various materials aiming to demonstrate how to go from “Zero” to “Hero” in the smoothest way possible. The original plan was for a full day with extra guided examples but, as we are limited to only half-day activity, we put on emphasis on direct hands-on using real codes. Presentations are kept minimal on purpose, the main goal is _doing_ and interact with the experts who are here to support.

#### Table of Content

* Introduction and System access
  * [Arm-based AWS Virtual Cluster](guides/cluster.md)
* COMPILE and EXECUTE
  * [Pre-installed software](guides/modules.md)
* PROFILE and OPTIMISE
  * [Short guide to Linux perf](guides/perf.md)
  * [Short guide to Perf Libs Tools](guides/perf-libs-tools.md)
  * [Short guide to mpiP](guides/mpip.md)
  * [Linaro MAP documentation](https://docs.linaroforge.com/23.0.4/html/forge/index.html)

#### Repository 

This repository provides additional resources and examples participants can follow but the core goal of the tutorial is to allow participants to try their own code or anu HPC code they are very familiar with. It is composed by 3 main folders:
 * `guides`: contains mini self-contained short guides on various sub-topics and tools (all referenced in the table of content below)
 * `slides`: contains all slides presented during the tutorial (plus any errata), conveniently split in several PDF. 

#### Resources

###### For those who use their own code...

You ready to start, conect on the machine and start builfing and experimenting.

###### For those who look for inspiration of what code to use..._

We are going to provide a walk-though example based on [`Code_Saturne`](https://github.com/code-saturne). We strongly suggest to use version 7.2.0 available here: https://github.com/code-saturne/code_saturne/archive/refs/tags/v7.2.0.tar.gz

Otherwise you can draw inspiration by following one of these two links:
- https://github.com/aws/aws-graviton-getting-started/tree/main/HPC
- https://github.com/arm-hpc-devkit/nvidia-arm-hpc-devkit-users-guide

We suggest to pick a community code you are familiar with because you are a contributor or a user. In doubt, ask. We will be happy to guide you and provide few suggestions (either full domain apps or mini-apps).

#### Acknowledgments 

This tutorial was made possible thanks to Arm Ltd, AWS, NVIDIA Cornporation with the support of the Arm HPC User Group.

#### Contributing 

If you would like to contribute something back to the Arm HPC community, either by adding example or extending a short guide, just put a pull request against this repo. Open source licenses only, please!

**[Join Arm HPC Slack](https://join.slack.com/t/a-hug/shared_invite/zt-25r69qm2u-hhEkbN7terYpw7K3W2k6Eg)**
