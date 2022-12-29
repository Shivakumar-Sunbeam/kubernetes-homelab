Configurring Metallb as a Load balancer service On Your Home Kubernetes Env
--> Create a cluster using minikube 
minikube start --nodes=5 --memory='3' --cpus='2' --vm-driver=virtualbox --network='wlo1'

--> Next, I am installing MetalLB using Kubernetes manifest, 
use the following lines. I am simply following the installation documentation found here.

kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.12.1/manifests/namespace.yaml
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.12.1/manifests/metallb.yaml

--> Next create and apply a config map that provides the list of ips that can be assigned to the load balancer as shown below :-

apiVersion: v1
kind: ConfigMap
metadata:
  name: config
  namespace: metallb-system
data:
  config: |
    address-pools:
    - name: default
      protocol: layer2
      addresses:
      - 192.168.59.108-192.168.59.120
