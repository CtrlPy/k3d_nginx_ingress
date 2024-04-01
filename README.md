# k3d_nginx_ingress


step1. *created new cluster k3d*

 ```zsh
 k3d cluster create --api-port 6550 -p "8081:80@loadbalancer" --agents 2
 ```

step2. *deploy nginx-deployment.yaml*



```zsh
kubectl apply -f nginx-deployment.yaml
```

step.3 *deploy nginx-service.yaml*


```zsh
kubectl apply -f nginx-service.yaml
```


 step4. *deploy ingress-nginx.yaml* 


```zsh 
kubectl apply -f ingress-nginx.yaml
```

 *check the local host*
 
```zsh
curl -v http://localhost:8081/
```


```zsh 
k3d cluster delete k3s-default
```