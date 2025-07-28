Here's a **list of 50 small hands-on tasks** to help you learn **Kubernetes (k8s)** step by step — covering everything from basics to intermediate-level stuff like volumes, probes, config management, scaling, and RBAC.

---

### 🧱 **BASICS (1–10)**

> Understand core components (pods, services, deployments)

1. Create a basic pod using nginx image
2. Expose that pod with a ClusterIP service
3. Create a Deployment with 3 replicas of nginx
4. Scale the Deployment to 5 replicas
5. Delete one pod from the Deployment and observe recreation
6. Run a busybox pod and exec into it to test DNS resolution
7. Create a pod with resource limits (CPU and memory)
8. Check logs of a pod using `kubectl logs`
9. Set a label on a pod and filter using `kubectl get pod -l`
10. Add annotations to a resource and fetch them

---

### 📦 **CONFIG & ENV VARS (11–18)**

> Learn about ConfigMaps, Secrets, and environment variables

11. Create a ConfigMap and mount it as environment variables
12. Mount a ConfigMap as a volume
13. Create a Secret and mount it into a pod
14. Use a Secret as an env var in a pod
15. Decode secret value using `base64 --decode`
16. Use `envFrom` to load all env vars from a ConfigMap
17. Create a pod that uses a config file from a volume
18. Update a ConfigMap and trigger a rollout

---

### 📂 **VOLUMES & STORAGE (19–28)**

> Understand PersistentVolumes, PVCs, hostPath, and StatefulSet basics

19. Create a PV using `hostPath`
20. Create a PVC and bind to the above PV
21. Create a pod that mounts the PVC and writes a file
22. Delete the pod and verify file persistence
23. Deploy nginx using StatefulSet + PVC
24. Add multiple replicas to StatefulSet and write unique content
25. Delete one StatefulSet pod and observe data persistence
26. Explore PV reclaim policies: Retain, Delete
27. Use `emptyDir` volume for temporary pod storage
28. Mount a volume at read-only mode

---

### 🔍 **LIVENESS / READINESS PROBES (29–32)**

> Improve application health check mechanisms

29. Add a readinessProbe to an nginx pod
30. Add a livenessProbe that checks HTTP `/healthz`
31. Break the container intentionally and see the probe reaction
32. Use `initialDelaySeconds` and `periodSeconds` effectively

---

### 🚀 **JOBS & CRONJOBS (33–35)**

> Automate one-time and scheduled tasks

33. Create a Job that runs `echo Hello`
34. Create a Job that runs a shell script from a ConfigMap
35. Create a CronJob that runs every minute

---

### 🔒 **RBAC & NAMESPACES (36–40)**

> Control access and isolation

36. Create a new namespace
37. Deploy resources inside the new namespace
38. Create a ServiceAccount and bind it to a pod
39. Create a Role and RoleBinding in a namespace
40. Create a ClusterRole and ClusterRoleBinding

---

### 🔁 **ROLLING UPDATE & ROLLBACK (41–43)**

> Handle deployments safely

41. Update the image version in a Deployment
42. Watch the rollout progress
43. Roll back to the previous version

---

### 🧠 **NODE MANAGEMENT & SCHEDULING (44–47)**

> Placement of pods and control over node assignment

44. Label nodes with a custom key
45. Use nodeSelector to schedule a pod to a specific node
46. Use taint on a node and toleration in a pod
47. Use affinity and anti-affinity rules for pod placement

---

### 🌐 **NETWORKING & SERVICES (48–50)**

> Access pods and apps securely

48. Expose a pod with NodePort and access it via external IP
49. Create an Ingress and route to multiple services
50. Add a TLS secret and enable HTTPS via Ingress

---

### 💡 Bonus Tips:

- Keep your cluster clean with `kubectl delete`
- Use `kubectl describe` and `kubectl get -o yaml` to learn internals
- Start with Minikube or kind for local testing if not in cloud
- Create a GitHub repo for your YAMLs, call it: `k8s-learning-lab`

---
