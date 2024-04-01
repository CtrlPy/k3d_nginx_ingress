# k3d_nginx_ingress


step1. *created new cluster k3d*

 ```zsh
 k3d cluster create -p "8081:80@loadbalancer" --agents 2
 ```