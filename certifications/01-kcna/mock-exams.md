# KCNA Mock Exams

Two 15-question mocks (25 min each). Use Mock 1 as a diagnostic about 7-10 days before the exam and Mock 2 as a dress rehearsal 2-3 days before.

## KCNA Mock 1 (15 questions, 25 min)

**1.** Which component stores all cluster state in Kubernetes?

- A. kube-scheduler
- B. etcd
- C. kubelet
- D. kube-proxy

**2.** What is the default Service type?

- A. NodePort
- B. LoadBalancer
- C. ClusterIP
- D. ExternalName

**3.** Which workload resource runs exactly one Pod on every node (or a selected set of nodes)?

- A. Deployment
- B. StatefulSet
- C. Job
- D. DaemonSet

**4.** Which CNCF graduated project is used primarily for metrics-based monitoring and alerting?

- A. Jaeger
- B. Prometheus
- C. Fluentd
- D. Envoy

**5.** What does the OCI define?

- A. Cloud pricing models
- B. Open standards for container image and runtime formats
- C. Kubernetes API versions
- D. Service mesh protocols

**6.** Which is a vendor-neutral standard for generating traces, metrics and logs?

- A. OpenTelemetry
- B. Grafana
- C. Loki
- D. Thanos

**7.** Which Kubernetes object holds non-sensitive configuration data?

- A. Secret
- B. ConfigMap
- C. PersistentVolume
- D. ServiceAccount

**8.** Which GitOps tool is a CNCF graduated project that syncs cluster state from Git?

- A. Jenkins
- B. Argo CD
- C. Terraform
- D. Ansible

**9.** What is the main responsibility of the kubelet?

- A. Scheduling Pods
- B. Ensuring containers described in PodSpecs are running on its node
- C. Storing secrets
- D. Routing external traffic

**10.** The Horizontal Pod Autoscaler needs which source for CPU/memory metrics in a typical cluster?

- A. etcd
- B. metrics-server
- C. kube-proxy
- D. CoreDNS

**11.** What does a CNI plugin provide?

- A. Container image storage
- B. Pod networking
- C. Persistent storage
- D. Authentication

**12.** Which of these is a CRI-compatible container runtime?

- A. containerd
- B. Helm
- C. Calico
- D. Kustomize

**13.** Which 12-factor principle says configuration should be stored where?

- A. In the codebase
- B. In the environment
- C. In the image
- D. In the database schema

**14.** Which command prints container logs for a Pod?

- A. kubectl describe
- B. kubectl logs
- C. kubectl top
- D. kubectl exec

**15.** What are the CNCF project maturity levels?

- A. Alpha, Beta, GA
- B. Sandbox, Incubating, Graduated
- C. Draft, Stable, Deprecated
- D. Bronze, Silver, Gold

**Answer key**

| Q | Answer |
|---|--------|
| 1 | B |
| 2 | C |
| 3 | D |
| 4 | B |
| 5 | B |
| 6 | A |
| 7 | B |
| 8 | B |
| 9 | B |
| 10 | B |
| 11 | B |
| 12 | A |
| 13 | B |
| 14 | B |
| 15 | B |

## KCNA Mock 2 (15 questions, 25 min)

**1.** What does kube-scheduler decide?

- A. Which node a new Pod runs on
- B. Which image to pull
- C. Which namespace to use
- D. Which CNI to install

**2.** Which workload provides stable network identity and ordered deployment?

- A. Deployment
- B. ReplicaSet
- C. StatefulSet
- D. CronJob

**3.** Which resource defines HTTP routing rules from outside the cluster to Services (when an ingress controller is installed)?

- A. Ingress
- B. NetworkPolicy
- C. Endpoints
- D. Namespace

**4.** What is the relationship between PV and PVC?

- A. PVC is storage; PV is a request
- B. PV is storage; PVC is a request for it
- C. They are identical
- D. PVC is only for secrets

**5.** What is the CSI for?

- A. Standard interface for storage drivers
- B. Container scanning
- C. Service discovery
- D. Cluster signing

**6.** Which tool is the package manager for Kubernetes?

- A. Helm
- B. Flux
- C. Linkerd
- D. etcdctl

**7.** When does the Cluster Autoscaler add nodes?

- A. When CPU on a node is 50%
- B. When Pods are Pending because they cannot be scheduled
- C. When a Service is created
- D. Every hour

**8.** What is the default update strategy of a Deployment?

- A. Recreate
- B. RollingUpdate
- C. Canary
- D. BlueGreen

**9.** Which is NOT a control plane component?

- A. kube-apiserver
- B. etcd
- C. kubelet
- D. kube-controller-manager

**10.** Which telemetry signal is best for numeric time-series data like request rate?

- A. Logs
- B. Traces
- C. Metrics
- D. Events

**11.** What is the main idea of a canary deployment?

- A. Roll a new version to a small subset of traffic first
- B. Delete old version immediately
- C. Run two clusters
- D. Disable rollbacks

**12.** Which RBAC objects grant permissions within a single namespace?

- A. ClusterRole + ClusterRoleBinding only
- B. Role + RoleBinding
- C. ServiceAccount only
- D. PodSecurityPolicy

**13.** What does a Namespace provide?

- A. Hardware isolation
- B. A scope for names and resource policies
- C. A separate control plane
- D. A separate etcd

**14.** What is a sidecar container?

- A. A container that runs in the same Pod to extend the main container
- B. A node agent
- C. A cluster add-on
- D. An init container only

**15.** What does the Linux Foundation / CNCF provide for projects?

- A. Vendor-neutral governance and community
- B. Commercial hosting only
- C. Proprietary licences
- D. Paid support only

**Answer key**

| Q | Answer |
|---|--------|
| 1 | A |
| 2 | C |
| 3 | A |
| 4 | B |
| 5 | A |
| 6 | A |
| 7 | B |
| 8 | B |
| 9 | C |
| 10 | C |
| 11 | A |
| 12 | B |
| 13 | B |
| 14 | A |
| 15 | A |
