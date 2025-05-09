# IMS Analog Deployment on Kubernetes (NGINX + MySQL + Prometheus + Grafana)

This project simulates a simplified IMS (IP Multimedia Subsystem) architecture using cloud-native components deployed on AWS EKS.

## Architecture Overview
  +-------------+         +-------------+
       |   Client    |  --->   |   NGINX     |  ---> Backend Services
       +-------------+         +-------------+
                                    |
                   +----------------+----------------+
                   |                                 |
              +--------+                       +-----------+
              | MySQL  |                       | Prometheus|
              +--------+                       +-----------+
                                                  |
                                              +---------+
                                              | Grafana |
                                              +---------+

## Components

| Component     | Description                                       |
|---------------|---------------------------------------------------|
| **NGINX**     | Simulated as a Proxy-CSCF (SIP-aware proxy)       |
| **MySQL**     | Serves as a basic HSS analog (user DB)            |
| **Prometheus**| Monitors the Kubernetes cluster and pods          |
| **Grafana**   | Visualizes performance metrics                    |
| **EKS**       | Managed Kubernetes cluster on AWS                 |

## Use Cases

- Practice deploying VoIP/IMS-like systems in Kubernetes
- Monitor "signaling" components using Prometheus
- Simulate alerting like CPU overload or pod failure
- Visualize system health with Grafana dashboards

## Deployment Steps

1. **Provision EKS Cluster**  
   You can use `eksctl` or Terraform.

2. **Deploy Components via Helm/Manifests**  
   - `nginx-deployment.yaml`  
   - `mysql-deployment.yaml`  
   - `prometheus-kube-stack` (via Helm)  
   - `grafana-service.yaml`

3. **Configure Prometheus Targets**  
   Make sure to label your deployments with `scrape=true`.

4. **Expose Grafana Dashboard**  
   Use NodePort or Ingress to access Grafana.

## Sample Commands

```bash
kubectl apply -f nginx-deployment.yaml
kubectl apply -f mysql-deployment.yaml
helm install kube-prometheus-stack prometheus-community/kube-prometheus-stack

![image](https://github.com/user-attachments/assets/9651bfae-a664-4ba8-bad0-8be0cc3c529f)

![image](https://github.com/user-attachments/assets/fde15afc-5d10-43d6-b382-1dcc4a93096e)

Future Improvements
Add SIP proxy like Kamailio or OpenSIPS for real signaling

Simulate traffic using sipp or custom scripts

Integrate alertmanager for incident simulation

Author
Eko Pradana

