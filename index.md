## Open Workload Project

Open Workload is an effort initiated by the desire to craft new possibilities for modern High Performance Computing (HPC). Our project Sky Port is a proof of concept of tools that allow user-facing software to have transparent access to multiple cloud computing resources via a single API. We call thus approach for the HPC resources management as Private HPC.

We are software developers and experts in HPC who try to work through and sharpen a universal bus that connects user software and cloud resources. Sky Port is the method, while our final goal is to present a new standard that describes a transportation layer that resides between a workload producer (user software) and multiple resource providers (cloud or HPC clusters).

We believe in:
* zero trust approach;
* highly heterogeneous and distributed future of HPC;
* eventual growth of demand for Private HPC.

## Private HPC

A private HPC refers to a practice of automatically aggregating compute power for a workload of a user who has full control over its lifecycle. The user runs a workload management software that offloads the computationally intensive workload to a remote on-premises compute cluster or to compute resources of a cloud provider. The user solely decides what compute resources her job should run on (or allows the workload manager to choose) and pays for those resources. 

The difference between the Private HPC and the usage of a manually configured HPC cluster in a public cloud is amount of workload and cluster management automation. The former allows a user or user-controlled software to submit a new workload to the private HPC management software without bothering about mechanisms behind the data transferring and the computational process. While the latter demands from the user additional knowledge and steps to create and configure an HPC cluster in the cloud, transmit the user’s data, run the workload, and download the workload results back to the user’s laptop. Those steps usually can be automated, but they are typically either not integrated into a single seamless user workflow or vendor locked. 

Sky Port is an open-source vendor-independent workload manager designed to show the power of Private HPC. We want to develop a new standard that simplifies the creation of seamlessly integrated components for Private HPC managers.

## Supported platforms

Sky Port targets support for the Linux operating system. A reasonable effort is made to support all major, modern Linux distributions on ARM64 and X86_64 architectures; however, validation is limited to the most recent releases of Ubuntu/X86_64 systems.

## Current status

The [source code](https://github.com/openworkload) can be considered as a reference and a proof of concept for future standard. The project started recently and requires some time for API stabilization. Thus one can consider the code for now as a highly experimental one.

The following video demostrates Sky Port functionality with JupyterHub spawner and Azure:
<video width="1280" controls>
  <source src="videos/jupyterhub.mp4" type="video/mp4">
  Your browser does not support the video tag.
</video>

## Source code

Sky Port consists of the following repositories:
* [Core](https://github.com/openworkload/swm-core): the main component of Sky Port (workload manager). This daemon runs in the background and serves all communications among terminals and gates.
* [Scheduler](https://github.com/openworkload/swm-sched): workload scheduler (a plugin for the core daemon). It creates timetables for job execution.
* [Gate](https://github.com/openworkload/swm-cloud-gate): a plugin for Sky Port that is in charge of all communications between the Core and cloud providers.
* [Jupyter terminal](https://github.com/openworkload/swm-jupyter-term): JupyterHub spawner that allows submission of Jupyter servers jobs to Sky Port. 
* [Console terminal](https://github.com/openworkload/swm-console-term): console program that uses Sky Port python client library to work with Sky Port workload and resources.
* [Python client library](https://github.com/openworkload/swm-python-client): wrapper around client REST API of the core component.

The following schema shows relationships among the Sky Port components.

![schema](./images/skyport_schema.png)

The idea of such components separation is the following: APIs of a Core and a Gate are well described. Thus they can be replaced to be more suitable for a user's problem. Terminals can be created by 3rd party software developers for specific user needs, like submission of Jupyter servers jobs. Cloud provider owners can create gates for their compute resources and share them among their users.

## Contributing

We appreciate all your contributions. If you are planning to contribute back bug fixes, please do so without any further discussion. If you plan to contribute new features, Sky Port improvements, or new gates and terminals, please open an issue and discuss the feature with us.

We use a shared copyright model that enables all contributors to maintain the copyright on their contributions. All the software we develop is licensed under the BSD-3-Clause license. Our code of conduct can be found [here](https://github.com/openworkload/swm-core/blob/master/CODE_OF_CONDUCT.md).
