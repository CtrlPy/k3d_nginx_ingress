# k3d_nginx_ingress


step1. *created new cluster k3d*

 ```zsh
 k3d cluster create -p "8081:80@loadbalancer" --agents 2

 ```

step2. *create deployment nginx-deployment.yaml*



```zsh
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
spec:
  replicas: 1
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx
        ports:
        - containerPort: 80

```

```zsh
kubectl apply -f nginx-deployment.yaml
```

step.3 *Create a ClusterIP service for it  nginx-service.yaml*

```zsh
apiVersion: v1
kind: Service
metadata:
  name: nginx-service
spec:
  selector:
    app: nginx
  ports:
    - protocol: TCP
      port: 80
      targetPort: 80
  type: ClusterIP

```

```zsh
kubectl apply -f nginx-deployment.yaml
```


 step4. *created new manifest file ingress-nginx.yaml* 

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
step3. *Create an ingress object for it by copying the following manifest to a file and applying with*

```zsh 
kubectl apply -f ingress-nginx.yaml
```

