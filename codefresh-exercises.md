here are my codfresh exercise notes


## App of Apps
```
. <(argocd completion bash)

 argocd app create my-favorite-apps \
   --project default \
   --sync-policy none \
   --repo https://github.com/lalyos/gitops-cert-level-2-examples.git \
   --path ./app-of-apps/my-app-list \
   --dest-namespace argocd \
   --dest-server https://kubernetes.default.svc
```

## MultiCluster Deployment

```
 argocd app create external-app \
   --project default \
   --sync-policy auto \
   --repo https://github.com/lalyos/gitops-cert-level-2-examples.git \
   --path ./simple-application \
   --dest-namespace default \
   --dest-server https://10.5.0.176:6443
```

```
 argocd app create internal-app \
   --project default \
   --sync-policy auto \
   --repo https://github.com/lalyos/gitops-cert-level-2-examples.git \
   --path ./simple-application \
   --dest-namespace default \
   --dest-server https://kubernetes.default.svc
```

## ApplcationSets


```
 ## if want to recreate:
 argocd app delete my-application-sets -y


 argocd app create my-application-sets \
   --project default \
   --sync-policy auto \
   --sync-option Prune=true \
   --repo https://github.com/lalyos/gitops-cert-level-2-examples.git \
   --path ./application-sets/my-application-sets \
   --dest-namespace default \
   --dest-server https://kubernetes.default.svc
```

### registering clusters

generate copy-paste command for login on host cluster ("Argo"Cluster)
```
echo argocd login kubernetes-vm:30443 --insecure --username admin --password $(cat admin-pass.txt)
```

paste it into cluster2 / cluster3
```
argocd cluster add default --name cluster-${HOSTNAME#kubernetes-vm} -y
```