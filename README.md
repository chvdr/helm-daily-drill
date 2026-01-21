# HELM DAILY DRILL — KodeKloud Helm Playground  

Version: v0.1 (Stable|Current)

## Preface

- Target time to finish (trained): ≤ 15 мин  
- Environment: k3s + Helm v3 (KodeKloud HELM Playground works) 
- Namespace: **drill**  
- Release: **web**  
- Chart: **bitnami/nginx**  

## 0) RESET

```
kubectl get ns
kubectl delete ns drill --ignore-not-found
kubectl create ns drill
helm uninstall web -n drill 2>/dev/null || true
```

## 1) REPO CHECK

```
helm repo add bitnami https://charts.bitnami.com/bitnami 2>/dev/null || true
helm repo update
helm search repo bitnami/nginx
```

### Expected result:

- bitnami/nginx is in the list 

## 2) INSTALL

```
helm install web bitnami/nginx -n drill
```

### Test(s)/Check(s):

```
helm list -n drill
helm status web -n drill
kubectl get deploy,svc,pods -n drill
```

### Expected result(s):

- Release web is being DEPLOYED
- Pod(s) are in *Running* state

## 3) UPGRADE

```
helm upgrade web bitnami/nginx -n drill --set replicaCount=2
```

### Test(s)/Check(s):

```
kubectl get deploy -n drill
helm history web -n drill
```

### Expected result(s):

- replicas = 2
- a new revision exists

## 4) ROLLBACK

```
helm rollback web 1 -n drill
``` 

### Test(s)/Check(s):

```
helm history web -n drill
kubectl get deploy -n drill
```

### Expected result(s):

- replicas = 1

## 5) TEMPLATE (RENDER)

```
helm template web bitnami/nginx -n drill > rendered.yaml
```

### Test(s)/Check(s):

```
grep -n "kind:" rendered.yaml | head
```

### Expected result(s):

- Deployment / Service / ConfigMap, etc... Are persisting. 

## 6) DRY-RUN + DEBUG

```
helm upgrade web bitnami/nginx -n drill --set replicaCount=3 --dry-run --debug
```

### Expected result(s):

- No real changes are being made
- Helm shows planned actions 

## 7) CLEANUP

```
helm uninstall web -n drill
kubectl delete ns drill
```

## Acceptance Criteria(s) 

- All executed w/o any help, from scratch
- ≤ 15 minutes
- No errors in namespace / release
- Good understanding of: status, history, template

