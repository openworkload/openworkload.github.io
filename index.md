## Sky Port

**Sky Port** is an open-source, vendor-independent workload manager for [HPC workload](https://en.wikipedia.org/wiki/High-performance_computing). It connects user software to cloud compute: submit a job, and Sky Port provisions the cluster, configures port forwarding, pulls containers, uploads data, runs containerized job, monitors progress, download result data, and tears resources down when the work is done.

Open Workload is the community behind Sky Port.

[Quick start](#quick-start) · [Try Jupyter](https://github.com/openworkload/swm-jupyter-term) · [Source on GitHub](https://github.com/openworkload)

### Why Sky Port

* **One workflow**: no separate steps to create VMs, forward ports, sync files, and clean up afterward.
* **You choose the resources**: pick node flavors and images (you pay the cloud provider directly).
* **Replaceable components**: Terminals (clients) and Gates (cloud connectors) speak documented REST APIs, so third parties can add user interfaces or cloud backends without forking the core.
* **Certificate-based trust**: Terminals, Core, and Gates authenticate with mutual TLS, not shared passwords.

## Quick start

Pull the release container with pre-installed Core + Gate:

```bash
docker pull openworkload/skyport:latest
```

From a [swm-core](https://github.com/openworkload/swm-core) checkout, bootstrap and start:

```bash
docker start skyport
```

Talk to a running Core with the console terminal:

```bash
pip install swmconsole
swm-console --help
swm-console --job-list
```

## How you use it

1. **Interactive Jupyter notebooks**: [Jupyter terminal](https://github.com/openworkload/swm-jupyter-term) (`swmjupyter` on PyPI) spawns JupyterLab on cloud VMs through Sky Port.
2. **Batch / scripted jobs**: write a `#SWM` job script and submit with [swm-console](https://github.com/openworkload/swm-console-term).
3. **Custom terminals**: build against the [Python client](https://github.com/openworkload/swm-python-client) (`swmclient` on PyPI) and the Core REST API.
4. **Your own cloud gate**: implement a Gate for your compute resources (Azure is the reference integration today).

### Job script sketch

```bash
#!/bin/bash
#SWM name example-job
#SWM nodes 3
#SWM flavor Standard_D2_v4
#SWM cloud-image ubuntu-22.04
#SWM container-image ubuntu:22.04
#SWM input-files data.dat
#SWM output-files results.out

./run_my_workload.sh
```

Directives cover nodes, GPUs, flavors, images, file transfer, and port forwarding. Full reference: [JOB_DIRECTIVES.md](https://github.com/openworkload/swm-core/blob/master/HOWTO/JOB_DIRECTIVES.md).

## Current status

Sky Port is **alpha**. APIs are still stabilizing.

**Available today**

* Full cloud job lifecycle (submit, schedule, provision, transfer, run, monitor, tear down).
* Microsoft Azure as the remote site.
* Multi-node and GPU job directives.
* Containerized jobs.
* Console and Jupyter terminals.
* Python client library.

## Software stack

| Component | Repository | Role |
|-----------|------------|------|
| Core | [swm-core](https://github.com/openworkload/swm-core) | Workload manager daemon; Terminal ↔ Gate orchestration |
| Scheduler | [swm-sched](https://github.com/openworkload/swm-sched) | Scheduler plugin; builds execution timetables |
| Gate | [swm-cloud-gate](https://github.com/openworkload/swm-cloud-gate) | Cloud provider integration (Azure) |
| Jupyter terminal | [swm-jupyter-term](https://github.com/openworkload/swm-jupyter-term) | JupyterHub spawner for Sky Port jobs |
| Console terminal | [swm-console-term](https://github.com/openworkload/swm-console-term) | CLI for jobs, flavors, images, and remotes |
| Python client | [swm-python-client](https://github.com/openworkload/swm-python-client) | Wrapper around the Core REST API |

## Design

Network connections between terminal, core, gate, and cloud provider:

![Networking](./images/networking.png)

## Supported platforms

Sky Port targets Linux on ARM64 and x86_64. A reasonable effort is made across major modern distributions, but validation is currently limited to recent Ubuntu on x86_64.

## Docs and contributing

* [Install / Docker](https://github.com/openworkload/swm-core/blob/master/HOWTO/INSTALL.md)
* [Azure setup](https://github.com/openworkload/swm-cloud-gate/blob/master/HOWTO/AZURE.md)
* [Build from source](https://github.com/openworkload/swm-core/blob/master/HOWTO/BUILD.md)
* [Job directives](https://github.com/openworkload/swm-core/blob/master/HOWTO/JOB_DIRECTIVES.md)

Bug fixes are welcome without prior discussion. For new features, gates, or terminals, [open an issue](https://github.com/openworkload/swm-core/issues) first.

Software is licensed under BSD-3-Clause. [Code of conduct](https://github.com/openworkload/swm-core/blob/master/CODE_OF_CONDUCT.md).
