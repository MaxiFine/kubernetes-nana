# Kubernetes Quick Reference README

This README is a practical, hands-on refresher for working with Kubernetes, including setup, key concepts, and common commands.

---

## 📦 Core Kubernetes Concepts

* **Pod**: Smallest deployable unit. Wraps one or more containers.
* **Deployment**: Manages ReplicaSets and ensures desired pod count.
* **Service**: Exposes pods internally or externally.
* **ConfigMap**: Stores configuration data as key-value pairs.
* **Secret**: Stores sensitive information like passwords or tokens.
* **Volume**: Provides persistent storage to containers.

---

## 🔧 Basic Commands

### Cluster & Context

```bash
kubectl config get-contexts     # List contexts
kubectl config use-context <ctx> # Switch context
kubectl cluster-info             # Cluster details
```

### Pods

```bash
kubectl get pods                 # List pods
kubectl describe pod <pod>       # Pod details
kubectl logs <pod>               # View pod logs
kubectl exec -it <pod> -- bash   # Enter pod shell
```

### Deployments

```bash
kubectl apply -f deployment.yaml # Apply manifest
kubectl get deployments          # List deployments
kubectl rollout restart deployment <name>   # Restart deployment
```

### Services

```bash
kubectl get svc                   # List services
kubectl port-forward svc/<svc> 8080:80 # Forward port
minikube service <svc>           # Open in browser
```

### ConfigMaps & Secrets

```bash
kubectl create configmap my-config --from-literal=key=value
kubectl get configmap my-config -o yaml

kubectl create secret generic my-secret --from-literal=password=1234
kubectl get secret my-secret -o yaml
kubectl describe secret my-secret
```

---

## ⚙️ Debugging

### Pod Status Reference

* `ImagePullBackOff`: Check image name or registry access.
* `CrashLoopBackOff`: Check logs for crash causes.
* `CreateContainerConfigError`: Likely missing secret or config.

### Describe for Detailed Events

```bash
kubectl describe pod <pod>
```

### View Logs

```bash
kubectl logs <pod>
```

---

## 📁 File Structure Example

```text
.
├── mongo-cluster/
│   ├── mongo-deployment.yaml
│   ├── mongo-express-deployment.yaml
│   ├── mongo-secret.yaml
│   ├── mongo-configmap.yaml
│   └── mongo-service.yaml
```

---

## 🧪 Useful Tips

* Always match `selector` labels between deployments and services.
* Use `env` from `secretKeyRef` and `configMapKeyRef`.
* Avoid using `latest` tag in production.
* Use `readinessProbe` and `livenessProbe` for robust pods.

---

## 🔄 Backdate Commits (Git Trick)

```bash
GIT_COMMITTER_DATE="2024-06-10T15:30:00" git commit --amend --no-edit --date "2024-06-10T15:30:00"
```

---

## 📚 Resources

* [Kubernetes Docs](https://kubernetes.io/docs/)
* [Kubectl Cheat Sheet](https://kubernetes.io/docs/reference/kubectl/cheatsheet/)
* [Play with Kubernetes](https://labs.play-with-k8s.com/)

---

Happy K8s'ing! 🚀
