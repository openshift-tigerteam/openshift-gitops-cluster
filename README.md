# openshift-gitops-cluster

## Install Openshift GitOps

```bash
./install-openshift-gitops.sh
```

## Create Secret for GitHub Access

```bash
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

## Apply the App-of-Apps

```bash
oc apply -f apps.yaml
```

## Add Users to the ArgoCD Admins Group

```bash
oc adm groups add-users cluster-admins <user>
```