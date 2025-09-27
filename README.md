# openshift-gitops-cluster

## Install Openshift GitOps

```shell
./install-openshift-gitops.sh
```

## Create Secret for GitHub Access

```shell
oc apply -f - <<EOF
apiVersion: v1
kind: Secret
metadata:
  name: openshift-cluster-gitops-credentials
  namespace: openshift-cluster-gitops
  labels:
    argocd.argoproj.io/secret-type: repository
type: Opaque
stringData:
  url: https://github.com/<org>/<yourrepo>.git
  username: <username>
  password: <github-pat>
  name: openshift-cluster-gitops
  project: cluster
EOF
```

## Apply the Apps

Apply the app of apps
```shell
oc apply -f apps.yaml
```

...or indivividually  

```shell
oc apply -f apps/openshift-gitops-operator.yaml
oc apply -f apps/openshift-gitops-cluster.yaml
oc apply -f apps/cluster-patches.yaml
# Then other stuff
oc apply -f apps/openshift-nmstate.yaml
oc apply -f apps/openshift-workload-availability.yaml
# Storage
oc apply -f _optional/openshift-storage/openshift-storage.yaml
# Registry
oc apply -f _optional/openshift-image-registry/openshift-image-registry.yaml
```

## Add Users to the ArgoCD Admins Group

```bash
oc adm groups add-users cluster-admins <user>
```

## Documentation

0 - Empty  
1 - Namespace, OperatorGroup  
2 - RBAC
3 - Subscriptions  
4 - <empty>
5+. Workloads, CRs, etc