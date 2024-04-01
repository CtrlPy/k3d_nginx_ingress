# k3d_nginx_ingress


step1. *created new cluster k3d*

 ```zsh
 k3d cluster create -p "8081:80@loadbalancer" --agents 2
 ```
 step2. *created new manifest file ingress-nginx.yaml* 

 ```zsh
 # apiVersion: networking.k8s.io/v1beta1 # for k3s < v1.19
apiVersion: networking.k8s.io/v1
kind: Ingress
metadata:
  name: nginx
  annotations:
    ingress.kubernetes.io/ssl-redirect: "false"
spec:
  rules:
  - http:
      paths:
      - path: /
        pathType: Prefix
        backend:
          service:
            name: nginx
            port:
              number: 80
 ```
