# k8s-esxi-monitoring-stack

A Kubernetes-based monitoring stack for collecting VMware ESXi metrics using Prometheus and visualizing them in Grafana.

---

## 🔧 Stack Components

This project uses the following components:

- **Prometheus** (via `kube-prometheus-stack` Helm chart) – to collect and store metrics
- **Grafana** – for data visualization
- **vmware_exporter** – an ESXi metrics exporter for Prometheus
- **ServiceMonitor** – custom configuration to let Prometheus scrape from the exporter

---

## 📁 Project Structure

```
.
├── grafana/                # Grafana dashboards (JSON)
├── manifests/              # Kubernetes manifests for ESXi exporter
├── .env.sample             # Sample environment file for sensitive data
└── README.md
```

---

## 🚀 Deployment Steps

> ⚠️ Assumes Prometheus and Grafana are already deployed on the Kubernetes cluster using the kube-prometheus-stack Helm chart.

### 1. Clone the repository

```bash
git clone https://github.com/amiirsadeghi/k8s-esxi-monitoring-stack.git
cd k8s-esxi-monitoring-stack
```

### 2. Fill in `.env.sample`

Rename and update it with your own ESXi credentials:

```bash
cp .env.sample .env
```

Edit `.env` with your values:

```
VSPHERE_HOST=192.168.X.X
VSPHERE_USER=administrator@vsphere.local
VSPHERE_PASSWORD=yourpassword
```

> ⚠️ Make sure you **do not commit** your `.env` file with real credentials!

### 3. Apply Kubernetes Manifests

```bash
kubectl apply -f manifests/
```

This will deploy:

- A `Deployment` running `vmware_exporter`
- A `Service` exposing metrics on port 9272
- A `ServiceMonitor` so Prometheus scrapes it automatically

---

## 📊 Grafana Dashboard

Import the dashboard from the `grafana/` folder or use the provided JSON manually:

- Go to **Grafana** → **Dashboards** → **Import**
- Paste the dashboard JSON
- Set the Prometheus datasource

---

## 🧪 Verify Metrics

- Visit Prometheus UI: `http://<prometheus-url>`
- Run query: `vmware_vm_power_state`
- You should see VMs listed with their power states

---

## 📌 Notes

- This exporter was tested with `pryorda/vmware_exporter:v0.18.3`
- Metric scrape interval is set to `60s` via `ServiceMonitor`

---

## 📄 License

This project is open-source and free to use under the MIT License.
