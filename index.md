Open Workload is an effort initiated from desire to craft a standard for a modern High Performance Computing (HPC) workload management. Our project Sky Port is a prove of concept of tools that allows user facing software to have transparent access to multiple cloud compute resources with a single API.

In other words we try to work through and sharpen a universal bus between user software and cloud resources. But our final goal is to present a new standard that would describe a transportation layer between any workload producer (user software) and resource providers (cloud or HPC clusters).

We believe in zero trust approach and follow its principles in our experiments. We also use a shared copyright model that enables all contributors to maintain the copyright on their contributions. All the software we develop is licensed under the BSD-3-Clause license.

Sky Port project consists of the following code repositories:
* [Core daemon](https://github.com/openworkload/swm-core): the core component of Sky Port. This is a daemon that runs in background and serve all communications among terminals and gates.
* [Scheduler](https://github.com/openworkload/swm-sched): workload scheduler for the core daemon.
* [Cloud gate](https://github.com/openworkload/swm-cloud-gate): a cloud plugin for Sky Port that is in charge of all communications with cloud providers.
* [Jupyter terminal](https://github.com/openworkload/swm-jupyter-term): JupyterHub spawner to run Jupyter servers via Sky Port. 
* [Console terminal](https://github.com/openworkload/swm-console-term): console program that uses Sky Port python clinet libary to work with Sky Port workload and resources.
* [Python client library](https://github.com/openworkload/swm-python-client): wrapper around client REST API of the core component.

The following schema shows relationships among the Sky Port components.

![schema](./images/skyport_schema.png)
