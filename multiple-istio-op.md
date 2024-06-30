- Issue: We are having two different istio-operator, one under namespace istio-system and another under namespace istio-operator:
```sh
ncn-m001:/home/istio # helm list -A | grep istio
cray-istio                              istio-system    2               2024-04-18 18:24:20.342379066 +0000 UTC deployed        cray-istio-2.10.0-20240404224452+4986080                1.11.8                      
cray-istio-deploy                       istio-system    1               2024-04-16 22:19:42.107546781 +0000 UTC deployed        cray-istio-deploy-1.29.0                                1.11.8                      
cray-istio-operator                     istio-system    4               2024-06-07 10:32:26.971194511 +0000 UTC deployed        cray-istio-operator-1.26.0                              1.11.8                      
cray-istio-operator                     istio-operator  4               2024-06-07 15:23:00.461909451 +0000 UTC deployed        cray-istio-operator-1.27.0-20240605221205+5d9fc26       1.19.10   
```
                  
But there is only one pod by the name istio operator:
```sh
ncn-m001:/home/istio # kubectl get po -A | grep istio
istio-operator   istio-operator-57745f66d5-l6j5n                                   1/1     Running             0               2d12h
istio-system     istio-ingressgateway-796954cf6d-9xcz2                             1/1     Running             0               52d
istio-system     istio-ingressgateway-796954cf6d-t5qrz                             1/1     Running             0               52d
istio-system     istio-ingressgateway-customer-admin-65798ffd66-88lj2              1/1     Running             0               52d
istio-system     istio-ingressgateway-customer-admin-65798ffd66-bmwjl              1/1     Running             0               52d
istio-system     istio-ingressgateway-customer-user-6b47cb7d76-5zjhs               1/1     Running             0               52d
istio-system     istio-ingressgateway-customer-user-6b47cb7d76-75bk2               1/1     Running             0               52d
istio-system     istio-ingressgateway-hmn-65b4565d97-299sc                         1/1     Running             0               52d
istio-system     istio-ingressgateway-hmn-65b4565d97-cnx7k                         1/1     Running             0               52d
istio-system     istiod-558994b769-6rk2p                                           1/1     Running             0               2d12h
istio-system     istiod-558994b769-lgv89                                           1/1     Running             0               2d12h
istio-system     istiod-558994b769-m29g4                                           1/1     Running             0               2d12h
istio-system     kiali-c57f76fb4-8lfc6                                             1/1     Running             0               54d
```

We ran out of the above error by removing the istio-operator and re-installed it
- after operator ugrade ran the health checks
- ncnHC not all passed
- ncnPHC all passed
