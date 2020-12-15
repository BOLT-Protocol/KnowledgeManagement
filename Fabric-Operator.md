# Fabric Operator Note

## Requirement
- Kubernetes is ready
- Istio is ready
- Helm is ready

## Sample
https://gitea-6f1861e5.baas.tmpstg.twcc.tw/TWCC-BAAS/fabric-operator/src/branch/tmp/operator/helm-charts

## Kubernetes command
- kubectl get pod
- kubectl get service
- kubectl logs {pod-name} {container-name} -n fabric
```shell
kubectl logs hlf-peer--atlantis--peer0-0 peer -n fabric
```

## Helm command
- helm install
- helm uninstall
- helm list

## Simple Sample
```shell
git clone
```


## Pod restart with latest image