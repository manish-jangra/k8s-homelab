# k8s-homelab

#### Install Nginx Ingress Controller
  ```BASH
  helm upgrade --install ingress-nginx ingress-nginx --repo https://kubernetes.github.io/ingress-nginx --namespace ingress-nginx --create-namespace
  ```
#### MetalLB Installation
  ```BASH
  helm repo add metallb https://metallb.github.io/metallb
  helm install metallb metallb/metallb
  ```
  
  **IP Address Pool**
  ```YAML
  apiVersion: metallb.io/v1beta1
  kind: IPAddressPool
  metadata:
    name: cheap
    namespace: metallb-system
  spec:
    addresses:
    - 192.168.0.5-192.168.0.10
  ```
