# k8s-homelab

#### Install Nginx Ingress Controller
  ```BASH
  helm upgrade --install ingress-nginx ingress-nginx --repo https://kubernetes.github.io/ingress-nginx --namespace ingress-nginx --create-namespace
  ```
**Sample Ingress**
```YAML
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: example
  namespace: foo
spec:
  ingressClassName: nginx
  rules:
    - host: www.example.com
      http:
        paths:
          - pathType: Prefix
            backend:
              service:
                name: exampleService
                port:
                  number: 80
            path: /
  # This section is only required if TLS is to be enabled for the Ingress
  tls:
    - hosts:
      - www.example.com
      secretName: example-tls  
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
**L2 Advertisement**
```YAML
apiVersion: metallb.io/v1beta1
kind: L2Advertisement
metadata:
  name: example
  namespace: metallb-system
spec:
  ipAddressPools:
  - cheap
  ```
