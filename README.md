[![GitHub Release][release-img]][release]
[![Downloads][download]][release]
[![License](https://img.shields.io/badge/License-Apache%202.0-blue.svg)](https://github.com/SysCraft820/aquasecurity-kube-bench/blob/main/LICENSE)

[download]: https://img.shields.io/github/downloads/SysCraft820/aquasecurity-kube-bench/total?logo=github
[release-img]: https://img.shields.io/github/release/SysCraft820/aquasecurity-kube-bench.svg?logo=github
[release]: https://github.com/SysCraft820/aquasecurity-kube-bench/releases

<img src="docs/images/kube-bench.png" width="200" alt="kube-bench logo">

kube-bench is a tool that checks whether Kubernetes is deployed securely by running the checks documented in the [CIS Kubernetes Benchmark](https://www.cisecurity.org/benchmark/kubernetes/).

Tests are configured with YAML files, making this tool easy to update as test specifications evolve.

![Kubernetes Bench for Security](/docs/images/output.png "Kubernetes Bench for Security")

## Quick start

There are multiple ways to run kube-bench.
You can run kube-bench inside a pod, but it will need access to the host's PID namespace in order to check the running processes, as well as access to some directories on the host where config files and other files are stored.

The supplied `job.yaml` [file](job.yaml) can be applied to run the tests as a job. For example:

```bash
$ kubectl apply -f job.yaml
job.batch/kube-bench created

$ kubectl get pods
NAME                      READY   STATUS              RESTARTS   AGE
kube-bench-j76s9   0/1     ContainerCreating   0          3s

# Wait for a few seconds for the job to complete
$ kubectl get pods
NAME                      READY   STATUS      RESTARTS   AGE
kube-bench-j76s9   0/1     Completed   0          11s

# The results are held in the pod's logs
kubectl logs kube-bench-j76s9
[INFO] 1 Master Node Security Configuration
[INFO] 1.1 API Server
...
