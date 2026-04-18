# My ArgoCD App

## Overview

This repository contains Kubernetes manifests and Helm charts for deploying a collection of microservices applications using ArgoCD. It demonstrates various deployment patterns including Kustomize-based configurations and Helm charts for backend services, frontend applications, and supporting infrastructure like NGINX.

## Repository Structure

- **`multi-app/`**: Kustomize configurations for a multi-application setup featuring:
  - Backend deployment and service
  - Frontend deployment and service

- **`multi-tier-app/`**: Kustomize configurations for a multi-tier application including:
  - Backend API deployment and service
  - Frontend deployment, service, ConfigMap, and NGINX configuration

- **`nginx/`**: Standalone Kubernetes manifests for deploying an NGINX server.

- **`notes-helm-app/`**: A Helm chart that packages:
  - Backend deployment and service
  - Frontend deployment, service, ConfigMap, and NGINX configuration

## Prerequisites

- A running Kubernetes cluster
- ArgoCD installed and configured on your cluster
- `kubectl` configured to access your cluster
- Git (for cloning the repository)

## Deployment Instructions

1. **Clone the Repository**:
   ```bash
   git clone https://github.com/sriramch163/my-argocd-app.git
   cd my-argocd-app
   ```

2. **Create ArgoCD Application**:
   - Open the ArgoCD UI or use the CLI
   - Create a new Application with the following settings:
     - **Repository URL**: `https://github.com/sriramch163/my-argocd-app`
     - **Path**: Select the desired application path (e.g., `multi-app`, `notes-helm-app`)
     - **Target Revision**: `main` (or your preferred branch)
     - **Destination Cluster**: Your Kubernetes cluster
     - **Destination Namespace**: Choose an appropriate namespace (e.g., `default` or create a new one)
   - For Helm-based deployments (`notes-helm-app`), ensure Helm is enabled in ArgoCD

3. **Sync the Application**:
   - In ArgoCD, click "Sync" to deploy the manifests to your cluster

4. **Verify Deployment**:
   ```bash
   kubectl get pods -n <your-namespace>
   kubectl get services -n <your-namespace>
   ```

## Usage

Once deployed, the applications will be accessible via their respective services. Check the service manifests for port configurations and external access methods (e.g., LoadBalancer, NodePort, or Ingress).

For example, to access the frontend service:
```bash
kubectl port-forward svc/frontend 8080:80 -n <your-namespace>
```
Then visit `http://localhost:8080` in your browser.

## Customization

- **Kustomize Apps**: Modify the `kustomization.yaml` files and overlay configurations to customize deployments.
- **Helm App**: Update `values.yaml` in `notes-helm-app/` to change default configurations before deploying.

## Contributing

We welcome contributions! Please:
1. Fork the repository
2. Create a feature branch
3. Make your changes
4. Submit a pull request with a clear description of the changes

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

## Support

If you encounter any issues or have questions, please open an issue in this repository.