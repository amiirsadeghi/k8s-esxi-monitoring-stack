# k8s-esxi-monitoring-stack

This project demonstrates how to monitor VMware ESXi virtual machines using Prometheus and Grafana on a Kubernetes cluster.

## Overview

- **Exporter**: [pryorda/vmware_exporter](https://github.com/pryorda/vmware_exporter) for collecting ESXi metrics.
- **Monitoring stack**: Uses Prometheus & Grafana (assumes already installed via `kube-prometheus-stack` Helm chart).
- **Visualizations**: Grafana dashboard for VM metrics.

## Requirements

- A running Kubernetes cluster
- Prometheus & Grafana installed (via kube-prometheus-stack)
- Access to an ESXi or vCenter endpoint

## Deployment Steps

1. Modify `.env` file with your own ESXi/vCenter credentials.
2. Apply Kubernetes manifests:

```bash
kubectl apply -f manifests/
```

3. Import the Grafana dashboard from `grafana/esxi-dashboard.json`.

## File Structure

- `manifests/`: Kubernetes manifests (Deployment, Service, ServiceMonitor)
- `grafana/`: Example Grafana dashboard JSON
- `.env.sample`: Template for environment variables