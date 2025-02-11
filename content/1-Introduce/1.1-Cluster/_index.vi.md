---
title: "Kiến trúc Cluster Kubernetes (K8s)"
weight: 1
chapter: false
pre: "<b> 1.1 </b>"
---



#### Tổng quan

Kubernetes là một nền tảng điều phối container mã nguồn mở được thiết kế để tự động hóa việc triển khai, mở rộng và quản lý các ứng dụng container hóa. Hệ thống này được tổ chức theo kiến trúc master-worker, trong đó mỗi thành phần đều có vai trò quan trọng trong việc duy trì hoạt động ổn định của cluster.

![Kubernetes Architecture](/images/1/1/0002.png?featherlight=false&width=60pc)

#### Control Plane (Master Node)

Control Plane đóng vai trò là bộ não của cluster Kubernetes, bao gồm các thành phần核心 (core components) sau:

#### API Server

API Server hoạt động như một gateway chính của cluster, xử lý tất cả các communication giữa các thành phần khác nhau. API Server implement một RESTful API interface, cho phép các tool như kubectl, dashboard và các ứng dụng khác tương tác với cluster. API Server cũng thực hiện authentication và authorization cho mọi request.

#### etcd 

etcd là một distributed key-value store đảm bảo high availability cho cluster state data. Nó lưu trữ toàn bộ configuration data và state information của cluster, hoạt động theo distributed consensus algorithm Raft để đảm bảo data consistency.

#### Scheduler

Scheduler chịu trách nhiệm watching các newly created pod và assign chúng vào các node phù hợp. Quá trình scheduling được thực hiện dựa trên nhiều factor như:

- Resource requirements
- Hardware/software constraints
- Affinity/anti-affinity specifications 
- Data locality
- Inter-workload interference

#### Controller Manager

Controller Manager chạy các controller process để regulate cluster state. Một số controller quan trọng bao gồm:

- Node Controller: Monitoring node health
- Replication Controller: Maintain pod replicas
- Endpoints Controller: Populate endpoints objects
- Service Account & Token Controllers: Handle default accounts và API access tokens

#### Worker Nodes

Worker nodes là nơi application workloads thực sự được running. Mỗi node bao gồm các thành phần sau:

#### Kubelet

Kubelet là primary node agent chạy trên mỗi node. Nó đảm bảo:

- Container running trong pod
- Node registration với cluster
- Pod và container health monitoring
- Resource usage reporting

#### Container Runtime

Container Runtime Interface (CRI) implementation như Docker hoặc containerd chịu trách nhiệm:

- Pulling container images
- Running containers
- Managing container lifecycle
- Handling container networking

#### Kube Proxy 

Kube Proxy maintain network rules trên nodes để enable pod networking và load balancing. Nó implement phần network portion của Kubernetes Service concept.

#### Workload Resources

#### Pods

Pod là smallest deployable unit trong Kubernetes. Mỗi pod encapsulate:

- One or more containers
- Storage resources
- Unique network IP
- Options governing container runtime behavior

#### Services

Service là một abstraction layer define một logical set of pods và policy để access chúng. Types của service bao gồm:

- ClusterIP: Internal cluster access
- NodePort: External access via node port
- LoadBalancer: External access via cloud provider load balancer
- ExternalName: External service mapping

#### Additional Components

#### Storage

Kubernetes cung cấp nhiều storage options:

- Persistent Volumes (PV): Cluster-wide storage resources
- Storage Classes: Dynamic volume provisioning
- Volume Claims (PVC): Storage requests từ pods

#### Networking

Network connectivity được handle bởi:

- Container Network Interface (CNI) plugins
- Service networking
- Ingress controllers cho HTTP/HTTPS routing

#### Security

Security được implement qua:

- Role-Based Access Control (RBAC)
- Network Policies
- Pod Security Policies
- Secret Management

Kiến trúc modular này cho phép Kubernetes scale efficiently và maintain high availability cho enterprise workloads. Mỗi component được thiết kế để có thể được replaced hoặc extended, tạo nên một hệ thống flexible và robust.