## Open Workload Project

Open Workload is an effort initiated from desire to craft new possibilities for a modern High Performance Computing (HPC). Our project Sky Port is a prove of concept of tools that allow user facing software to have transparent access to multiple cloud compute resources via a single API. We call this Private HPC.

We are software developers and experts in HPC who try to work through and sharpen a universal bus between a user software and cloud resources. Sky Port is the method, while our final goal is to present a new standard that describes a transportation layer between a workload producer (user software) and multiple resource providers (cloud or HPC clusters).

We believe in:
* zero trust approach;
* highly heterogeneous and distributed future of HPC;
* eventual grows of demand of Private HPC.

## Private HPC

A private HPC refers to a practice of automatically aggregating compute power for workload of a user who has full control over its lifecycle. The user runs a workload management software that offloads the computational intensive workload to a remote on premises compute cluster or to compute resources of a cloud provider. The user solely decides what compute resources her job should run on (or allows the workload manager to decide) and pays for those resources. 

The difference between the Private HPC and a usage of a manually configured HPC cluster in public cloud is a level of workload and cluster management automation. The former allows a user or user controlled software to submit a new workload to the private HPC management software without a need of bothering about mechanisms behind the data transferring and the computational process. While the latter demands from the user additional knowledge and steps to create and configure HPC cluster in cloud, to transfer the user’s data, to run the workload, and to download the workload results back to the user's laptop. Those steps usually can be automated, but they are typically either not integrated in a single seamless user workflow, or vendor locked. 

Sky Port is an open source vendor-independent workload manager that is summoned to show the power of Private HPC. We want to develop a new standard that simplifies a creation of seamlessly integrated components for Private HPC managers.

## Supported platforms

Sky Port targets support for the Linux operating system. A reasonable effort is made to support all major, modern Linux distributions on ARM64 and X86_64 architectures; however, validation is limited to the most recent releases of Ubuntu/X86_64 systems.

## Current status

The [source code](https://github.com/openworkload) of can be considered as a reference and a prove of concept for a future standard. The project is started recently and requires some time for the API stabilization. Thus one can consider the code for now as a highly experimental one.

## Source code

Sky Port consists of the following repositories:
* [Core](https://github.com/openworkload/swm-core): the main component of Sky Port (workload manager). This is a daemon that runs in a background and serves all communications among terminals and gates.
* [Scheduler](https://github.com/openworkload/swm-sched): workload scheduler (a plugin for the core daemon). It creates timetables of the jobs execution.
* [Gate](https://github.com/openworkload/swm-cloud-gate): a plugin for Sky Port that is in charge of all communications between the Core and cloud providers.
* [Jupyter terminal](https://github.com/openworkload/swm-jupyter-term): JupyterHub spawner that allows to submit Jupyter servers jobs to Sky Port. 
* [Console terminal](https://github.com/openworkload/swm-console-term): console program that uses Sky Port python clinet libary to work with Sky Port workload and resources.
* [Python client library](https://github.com/openworkload/swm-python-client): wrapper around client REST API of the core component.

The following schema shows relationships among the Sky Port components.

![schema](./images/skyport_schema.png)

The idea of such components separation is the following: APIs of a Core and a Gate are well described. Thus they can be replaced to more suitable for a user problem ones. Terminals can be created by 3rd party software developres for specific user needs, like a submittion of Jupyter servers jobs. Cloud provider owners can create gates for their compute resources and share among their users.

## Contributing

We appreciate all contributions. If you are planning to contribute back bug-fixes, please do so without any further discussion. If you plan to contribute new features, Sky Port improvements or new gates and terminals, please first open an issue and discuss the feature with us.

We use a shared copyright model that enables all contributors to maintain the copyright on their contributions. All the software we develop is licensed under the BSD-3-Clause license.
