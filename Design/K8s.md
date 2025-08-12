cloud-native environment stack (AWS, Terraform, Kubernetes), "kubectl" commands for microservice architecture are

* Pod/deployment management
* Logs and debugging
* Namespaces and contexts
* Scaling and rollout strategies
* Resource inspection and editing

---

## 🧰 ✅ **Must-Know `kubectl` Commands**

### 🔍 1. **Inspect Cluster Resources**

```bash
kubectl get pods                # List pods in current namespace
kubectl get pods -n <namespace>  # In a specific namespace
kubectl get deployments
kubectl get services
kubectl get nodes
kubectl get namespaces
kubectl get events             # View recent events (useful for debugging)
```

---

### 📦 2. **Deploy or Modify Applications**

```bash
kubectl apply -f <file.yaml>     # Apply YAML config (create/update)
kubectl delete -f <file.yaml>    # Delete resource defined in YAML
kubectl create -f <file.yaml>    # Create resource (older alternative to apply)

kubectl scale deployment my-app --replicas=5    # Scale deployment
kubectl rollout restart deployment my-app       # Restart pods in deployment
```

---

### 🔁 3. **Rollouts and Updates**

```bash
kubectl rollout status deployment my-app       # Check rollout status
kubectl rollout undo deployment my-app         # Roll back to previous version
```

---

### 🧪 4. **Debugging Pods**

```bash
kubectl logs <pod-name>                        # View logs
kubectl logs -f <pod-name>                     # Tail logs
kubectl logs <pod-name> -c <container-name>    # Multi-container pod logs

kubectl describe pod <pod-name>                # Details + events for pod
kubectl exec -it <pod-name> -- /bin/bash       # Shell into a running pod

kubectl port-forward pod/<pod-name> 8080:80    # Access service locally
```

---

### 🌐 5. **Namespace and Context Management**

```bash
kubectl config get-contexts                   # Show available contexts
kubectl config use-context <context-name>     # Switch context (cluster)
kubectl config current-context                # Show current context

kubectl get all -n <namespace>                # See all resources in namespace
kubectl config set-context --current --namespace=<namespace>  # Set default namespace
```

---

### 🧰 6. **Resource Editing & Live Debugging**

```bash
kubectl edit deployment <deployment-name>     # Live edit YAML in your editor
kubectl delete pod <pod-name>                 # Deletes pod (it will restart if managed by deployment)
kubectl top pod                               # Show resource usage (needs metrics server)
```

---

### 📁 7. **Generating Templates (Optional, Dev Use)**

```bash
kubectl run nginx --image=nginx --restart=Never --dry-run=client -o yaml > pod.yaml
kubectl expose deployment my-app --type=LoadBalancer --port=80 --target-port=8080
```

---

## 🧠 Bonus: Helpful Add-ons

| Tool      | Purpose                                     |
| --------- | ------------------------------------------- |
| `k9s`     | Terminal UI for Kubernetes management       |
| `kubectx` | Easily switch contexts                      |
| `kubens`  | Easily switch namespaces                    |
| `stern`   | Tail logs from multiple pods with filtering |
| `lens`    | GUI for cluster management                  |

---

## ✅ Summary Cheatsheet

| Area            | Key Command                                  |
| --------------- | -------------------------------------------- |
| Get Resources   | `kubectl get pods/services/deployments`      |
| Apply Configs   | `kubectl apply -f deployment.yaml`           |
| Logs & Debug    | `kubectl logs`, `kubectl exec`, `describe`   |
| Scale/Update    | `kubectl scale`, `rollout restart/undo`      |
| Cluster Context | `kubectl config use-context`, `get-contexts` |
| Namespace Mgmt  | `kubectl -n`, `kubens`, `set-context`        |
| Inspect Usage   | `kubectl top pod`, `kubectl top node`        |


