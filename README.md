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
