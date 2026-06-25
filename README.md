# GitOps Infrastructure State Repository (ArgoCD & Kubernetes)

This repository acts as the **Single Source of Truth** for the entire deployment state of our multi-node Kubernetes cluster. It drives the **Continuous Delivery (CD)** leg of our automated software deployment lifecycle using declarative GitOps models.

## Infrastructure Lifecycle
Instead of operators running manual `kubectl apply` shell commands, **ArgoCD** continuously polls this repository. 

Whenever the upstream CI engine (Jenkins) alters the version hash tags inside `templates/deployment.yaml`, ArgoCD detects a state mismatch ("OutOfSync"), calculates the configuration delta, and automatically synchronizes the running Kubernetes objects safely to match this file.

---

## Deployed Cluster Topology
* **Target Cluster System:** Local multi-node `Kind` (Kubernetes in Docker) sandbox engine.
* **Nodes Cluster Strategy:** 1 Dedicated Control Plane Node, 2 High-Availability Worker Scaling Nodes.
* **Deployment Target Namespace:** `default`
* **Replica Footprint:** 2 High-Availability Load-Balanced Application Pods.

---

## Tech Stack & Tooling
* **GitOps Automation Engine:** ArgoCD (Declarative continuous tracking engine)
* **Orchestration Platform Engine:** Kubernetes (`Kind` distribution)
* **Configuration Syntax:** Declarative Kubernetes YAML Schema Specifications
