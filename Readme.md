# Multi-Node Kubernetes Cluster Setup

Deploy a three-node Kubernetes cluster using Kind for production-like environment.

## Cluster Architecture

Three nodes with specific purposes:
- **Node A**: Application workloads
- **Node B**: Database workloads
- **Node C**: Dependent services (observability, vault, etc.)

## Prerequisites

- Docker
- Kind
- Kubectl

## Quick Start

1) Install Kind (if not installed):
```bash
# Refer to documentation
https://kind.sigs.k8s.io/docs/user/quick-start/
```

2) Install Kubectl, refer to the documentation provided below for installation instructions.
```bash
  https://kubernetes.io/docs/tasks/tools/
```


3) Clone the repository and Navigate to directory:

```bash
  git clone https://github.com/venk404/Assignment-5-ClustercCreation-in-kind.git
```

4) Let's set up a three-node cluster using Kind.
```bash
  kind create cluster --name multinode-cluster  --config .\clusters.yml 

  kubectl cluster-info --context kind-multinode-cluster

  #Check if the nodes are properly created and confirm that the volume exists by inspecting the folder on the local machine.
  kubectl get nodes 
```


5) Let's set type/label the nodes according to their respective roles.
```bash
  kubectl label node multinode-cluster-worker type=application
  kubectl label node multinode-cluster-worker2 type=database
  kubectl label node multinode-cluster-worker3 type=dependent_services
```

6) Let's check if the label is associated with the node.
```bash
  kubectl get nodes --show-labels
```

7) Deleting the Kind Cluster
```bash
kind delete cluster --name multinode-cluster
```