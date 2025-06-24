# KubeQuest - Dashboard - Cluster K3s

## ⚙ Setup Environment
1. Connect to the NODE MASTER in Cluster K3S.
2. Install HELM : https://helm.sh/docs/intro/install/
3. Use repo dashboard-kube HELM : https://artifacthub.io/packages/helm/argo/argo-cd
4. Run command :
```bash
sudo chmod 644 /etc/rancher/k3s/k3s.yaml
sudo helm repo add k8s-dashboard https://kubernetes.github.io/dashboard
sudo helm repo update
sudo KUBECONFIG=/etc/rancher/k3s/k3s.yaml helm install kubernetes-dashboard k8s-dashboard/kubernetes-dashboard --version 7.13.0 --namespace kubernetes-dashboard --create-namespace --set app.ingress.enabled=false --set nginx.enabled=false --set cert-manager.enabled=false
```
5. Run command (2), créer les droits etc:
```bash
kubectl apply -f - <<EOF
apiVersion: v1
kind: ServiceAccount
metadata:
  name: admin-user
  namespace: kubernetes-dashboard
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: admin-user-binding
roleRef:
  kind: ClusterRole
  name: cluster-admin
  apiGroup: rbac.authorization.k8s.io
subjects:
- kind: ServiceAccount
  name: admin-user
  namespace: kubernetes-dashboard
EOF
```
6. Run command (3), récupérer le Bearer Token :
```bash
kubectl -n kubernetes-dashboard create token admin-user
```
