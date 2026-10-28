# KCNA Practice Exam: 60 Questions

**Format:** 60 multiple-choice questions, 90 minutes, pass mark about 75% (45/60). No resources allowed.
**Domains (approx. weights):** Kubernetes Fundamentals 46%, Container Orchestration 22%, Cloud Native Architecture 16%, Observability 8%, Application Delivery 8%.
Questions 1-28 Fundamentals, 29-41 Orchestration, 42-51 Architecture, 52-56 Observability, 57-60 Delivery.
Answer key is at the end. Verify weights against github.com/cncf/curriculum.

---

## Kubernetes Fundamentals

**1.** What is the smallest deployable unit in Kubernetes?
A. Node  B. Deployment  C. Pod  D. Container

**2.** Which component exposes the Kubernetes API?
A. kube-apiserver  B. kube-proxy  C. kubelet  D. etcd

**3.** Which command creates or updates resources declaratively from a manifest?
A. kubectl run  B. kubectl apply -f  C. kubectl exec  D. kubectl port-forward

**4.** What does a Kubernetes controller do?
A. Pulls images  B. Stores secrets  C. Runs containers directly  D. Continuously reconciles actual state toward desired state

**5.** Which resource manages ReplicaSets and provides rolling updates?
A. Job  B. Ingress  C. Deployment  D. DaemonSet

**6.** Which node component maintains network rules that implement Services?
A. CoreDNS  B. kube-proxy  C. kubelet  D. kube-scheduler

**7.** What is the default `restartPolicy` of a Pod?
A. Once  B. OnFailure  C. Never  D. Always

**8.** Which resource runs a task to completion?
A. Job  B. Ingress  C. DaemonSet  D. ReplicaSet

**9.** Which statement about annotations is true?
A. They hold non-identifying metadata  B. They are used by selectors  C. They are required on Pods  D. They are limited to 63 characters

**10.** Which Service type provisions an external load balancer through a cloud provider?
A. ExternalName  B. NodePort  C. ClusterIP  D. LoadBalancer

**11.** How is a headless Service created?
A. `selector: {}`  B. `type: None`  C. `clusterIP: None`  D. `type: Headless`

**12.** What is the default-domain FQDN of Service `web` in namespace `shop`?
A. web.svc.shop.local  B. web.shop.svc.cluster.local  C. web.shop.cluster.local  D. shop.web.svc.cluster.local

**13.** Which resource is intended for small amounts of sensitive data?
A. ConfigMap  B. Namespace  C. Secret  D. PersistentVolume

**14.** Which access mode allows read-write mounting by a single node?
A. ReadWriteNone  B. ReadWriteOnce  C. ReadWriteMany  D. ReadOnlyMany

**15.** What do taints do?
A. Limit CPU  B. Label nodes  C. Repel Pods from nodes unless they tolerate the taint  D. Attract Pods to nodes

**16.** Resource requests are primarily used by which component?
A. kubelet to restart containers  B. kube-scheduler to place Pods  C. kube-proxy  D. etcd

**17.** What happens when a container exceeds its memory limit?
A. It is throttled  B. It is evicted from etcd  C. It is OOMKilled  D. Nothing

**18.** What happens when a liveness probe fails?
A. Container is restarted  B. Pod is deleted permanently  C. Node is drained  D. Pod removed from endpoints

**19.** What happens when a readiness probe fails?
A. Image re-pulled  B. Node cordoned  C. Container restarted  D. Pod removed from Service endpoints

**20.** What is required for an Ingress resource to take effect?
A. A DaemonSet only  B. An Ingress controller  C. A StatefulSet  D. A NodePort only

**21.** Which consensus algorithm does etcd use?
A. Raft  B. Gossip  C. Paxos  D. Two-phase commit

**22.** What does a kubeconfig file contain?
A. Clusters, users and contexts  B. Nodes and Pods  C. Secrets only  D. Images

**23.** Which of these is cluster-scoped?
A. Role  B. RoleBinding  C. ServiceAccount  D. ClusterRole

**24.** What does `kubectl cordon` do?
A. Evicts Pods  B. Marks the node unschedulable  C. Reboots the node  D. Deletes the node

**25.** What does `kubectl drain` do?
A. Deletes the namespace  B. Only cordons  C. Cordons and evicts Pods  D. Scales to zero

**26.** Which resource is NOT namespaced?
A. ConfigMap  B. Pod  C. Node  D. Service

**27.** What is a key property of a StatefulSet?
A. One Pod per node  B. Stable identities and per-Pod storage  C. Batch execution  D. Random Pod names

**28.** What does `kubectl get pods -o wide` add?
A. Logs  B. Node and IP information  C. Secrets  D. RBAC rules

---

## Container Orchestration

**29.** How do containers differ from VMs?
A. Each has its own kernel  B. They share the host kernel  C. They cannot be isolated  D. They need a hypervisor

**30.** Container image layers are:
A. Immutable read-only layers  B. Mutable  C. A single file  D. Always encrypted

**31.** What is the CRI?
A. API between etcd and API server  B. API between kubelet and container runtimes  C. Network plugin spec  D. Storage spec

**32.** What is runc?
A. A reference OCI runtime  B. A CNI plugin  C. A service mesh  D. An ingress controller

**33.** Linux cgroups are used to:
A. Encrypt traffic  B. Resolve DNS  C. Layer filesystems  D. Limit and account for resources

**34.** NetworkPolicy objects are enforced by:
A. etcd  B. The CNI plugin  C. kube-apiserver  D. kubelet

**35.** What does a service mesh do?
A. Stores secrets  B. Builds images  C. Manages service-to-service communication (mTLS, retries, telemetry)  D. Provisions nodes

**36.** Calico and Cilium are examples of:
A. CRI runtimes  B. CNI plugins  C. CSI drivers  D. Ingress classes only

**37.** What does CSI allow?
A. Vendors to ship storage drivers without changing Kubernetes core  B. Pod scheduling  C. DNS customisation  D. Image scanning

**38.** Kubernetes network model requires that Pods can communicate:
A. Only on the same node  B. Only via NAT  C. Only via Services  D. Without NAT

**39.** How does kube-scheduler pick a node?
A. Randomly  B. Filters nodes, then scores feasible ones  C. Alphabetically  D. Scores then filters

**40.** What does a PodDisruptionBudget limit?
A. Cloud cost  B. Pod priority  C. Pod security  D. Voluntary disruptions of Pods

**41.** What does a container registry do?
A. Collects logs  B. Routes traffic  C. Stores and distributes container images  D. Schedules Pods

---

## Cloud Native Architecture

**42.** Which is a characteristic of microservices?
A. A single deployable unit  B. Independently deployable services  C. No APIs  D. Shared database mandatory

**43.** What does the Vertical Pod Autoscaler adjust?
A. Number of nodes  B. Ingress rules  C. Number of replicas  D. Resource requests/limits of Pods

**44.** Which project provides serverless workloads on Kubernetes?
A. Helm  B. Knative  C. Falco  D. Jaeger

**45.** Envoy is best described as:
A. A storage driver  B. A high-performance proxy used in many service meshes  C. A package manager  D. A CNI plugin

**46.** What is KEDA used for?
A. Cluster upgrades  B. Image signing  C. Event-driven autoscaling  D. Log shipping

**47.** What is the role of the CNCF Technical Oversight Committee (TOC)?
A. Running clusters  B. Writing application code  C. Technical governance and project acceptance  D. Selling licences

**48.** What does immutable infrastructure imply?
A. Never deploy  B. Patch servers in place  C. Replace rather than modify running instances  D. Use only VMs

**49.** What are Kubernetes SIGs?
A. Signed Image Guards  B. Special Interest Groups owning areas of the project  C. Service Ingress Gateways  D. Security Incident Groups

**50.** What does the Horizontal Pod Autoscaler change?
A. Pod CPU limits only  B. Image tags  C. Node count  D. Number of Pod replicas

**51.** Which best matches the CNCF definition of cloud native?
A. Monolithic apps  B. Apps without containers  C. Scalable apps in dynamic environments using containers, microservices, immutable infrastructure and declarative APIs  D. Apps run only on one cloud

---

## Observability

**52.** What are the three pillars of observability?
A. Alerts, tickets, dashboards  B. CPU, RAM, disk  C. Pods, Nodes, Services  D. Logs, metrics, traces

**53.** What is the query language of Prometheus?
A. SQL  B. PromQL  C. LogQL  D. GraphQL

**54.** How does Prometheus normally collect metrics?
A. Reads etcd  B. Pulls (scrapes) from targets  C. Targets push over SMTP  D. Uses SSH

**55.** What does distributed tracing help with?
A. Scheduling  B. Following a request across services  C. Building images  D. Storing secrets

**56.** Fluent Bit and Fluentd are used for:
A. Autoscaling  B. Log collection and forwarding  C. Service mesh  D. Image scanning

---

## Application Delivery

**57.** What is the difference between CI and CD?
A. CI integrates and tests changes; CD delivers/deploys them  B. They are identical  C. CI is only for ops  D. CD builds images only

**58.** What is the core GitOps principle?
A. Manual kubectl in prod  B. Git is the source of truth for desired state  C. Databases hold config  D. No version control

**59.** What is a Helm chart?
A. A log format  B. A container image  C. A CNI plugin  D. A packaged set of Kubernetes resource templates

**60.** What is a blue/green deployment?
A. Gradual 5% rollout  B. Deleting the old version first  C. Running one version only  D. Two environments, switching traffic from old (blue) to new (green)

---

## Answer Key

| Q | A | Why |
|---|---|-----|
| 1 | C | Pod |
| 2 | A | kube-apiserver |
| 3 | B | apply is declarative |
| 4 | D | Reconciliation loop |
| 5 | C | Deployment manages ReplicaSets |
| 6 | B | kube-proxy programs Service rules |
| 7 | D | Always |
| 8 | A | Job |
| 9 | A | Non-identifying metadata |
| 10 | D | LoadBalancer |
| 11 | C | clusterIP: None |
| 12 | B | svc.cluster.local |
| 13 | C | Secret |
| 14 | B | RWO |
| 15 | C | Repel unless tolerated |
| 16 | B | Scheduler uses requests |
| 17 | C | OOMKilled |
| 18 | A | Restart |
| 19 | D | Removed from endpoints |
| 20 | B | Controller needed |
| 21 | A | Raft |
| 22 | A | Clusters, users, contexts |
| 23 | D | ClusterRole is cluster-scoped (Role, RoleBinding and ServiceAccount are namespaced) |
| 24 | B | Unschedulable |
| 25 | C | Cordon plus evict |
| 26 | C | Nodes are cluster-scoped |
| 27 | B | Stable identity/storage |
| 28 | B | Node and IP |
| 29 | B | Shared kernel |
| 30 | A | Read-only layers |
| 31 | B | CRI |
| 32 | A | OCI runtime |
| 33 | D | Resource limits |
| 34 | B | CNI enforces |
| 35 | C | Mesh functions |
| 36 | B | CNI |
| 37 | A | Out-of-tree drivers |
| 38 | D | No NAT |
| 39 | B | Filter then score |
| 40 | D | Voluntary disruptions |
| 41 | C | Image storage |
| 42 | B | Independent deployability |
| 43 | D | VPA changes requests/limits |
| 44 | B | Knative |
| 45 | B | Envoy proxy |
| 46 | C | Event-driven autoscaling |
| 47 | C | TOC governance |
| 48 | C | Replace not patch |
| 49 | B | SIGs |
| 50 | D | HPA scales replicas |
| 51 | C | CNCF definition |
| 52 | D | Logs, metrics, traces |
| 53 | B | PromQL |
| 54 | B | Scrape model |
| 55 | B | Request tracing |
| 56 | B | Log collection |
| 57 | A | CI vs CD |
| 58 | B | Git as source of truth |
| 59 | D | Packaged templates |
| 60 | D | Blue/green |

**Scoring:** 45+ = pass-ready. Below 45, review the domains of the questions you missed.
