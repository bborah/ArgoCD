
# Argo CD Application Sync Policy with Prune Feature Demonstration

## Prerequisites
- An operational Argo CD installation
- Access to a Kubernetes cluster with Argo CD installed
- A Git repository with Kubernetes manifests

## Steps

### 1. Define a Kubernetes Application
Create an `Application` resource in Argo CD. This YAML file defines the application, its source repository, and the sync policy, including the prune option.

[0-Demo-Files/Nginx_Deployment_ArgoCD_Apps/argo-app-prune-demo.yaml](../0-Demo-Files/Nginx_Deployment_ArgoCD_Apps/argo-app-prune-demo.yaml)

### 2. Apply the Application
Deploy this application to your Argo CD environment using `kubectl`.

**Command:**
```bash
kubectl apply -f argo-app-prune-demo.yaml
```

### 3. Modify the Manifests
Make changes to your manifests in the Git repository. For example, remove a resource that was previously deployed.

### 4. Sync the Application
Argo CD will automatically sync these changes based on the sync policy. If `selfHeal` is enabled, it will sync automatically, or you can manually trigger a sync.

**Manual Sync Command:**
```bash
argocd app sync prunetestapp
```

### 5. Observe Pruning
Argo CD will prune (delete) the resources that are no longer present in the repository from the Kubernetes cluster.

### 6. Check the Application Status
Verify the status of the application and ensure that the pruning occurred as expected.

**Command:**
```bash
argocd app get prunetestapp
```

### 7. Monitoring and Logs
Monitor the Argo CD UI or check logs for detailed information about the sync and prune process.

**Logs Command:**
```bash
kubectl logs deployment/argocd-repo-server -n argocd
```

## Notes
- Always ensure that the `prune` option is used cautiously, as it can remove resources from your cluster.
- Test the sync and prune behavior in a non-production environment before applying it to production.
- Keep your Git repository up-to-date and accurately reflecting the desired state of your cluster.