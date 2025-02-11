---
title: "Giới thiệu"
weight: 1
chapter: false
pre: "<b> 1. </b>"
---


#### Tổng Quan về Kubernetes

Kubernetes là một nền tảng orchestration mã nguồn mở, được thiết kế để quản lý và tự động hóa việc triển khai các ứng dụng container hóa và microservices. Thuật ngữ Kubernetes, có nguồn gốc từ tiếng Hy Lạp với ý nghĩa "người lái tàu" hoặc "hoa tiêu", phản ánh vai trò của nó trong việc điều hướng và quản lý hệ thống container phức tạp.

Google đã phát triển Kubernetes dựa trên kinh nghiệm vận hành production workloads quy mô lớn trong hơn 15 năm, trước khi mở mã nguồn vào năm 2014. Kể từ đó, nền tảng này đã phát triển thành một hệ sinh thái phong phú với sự đóng góp từ cộng đồng developer toàn cầu.

![Kubernetes Architecture](/images/1/kubernetes.webp)

#### Quá Trình Phát Triển của Container Orchestration

Để hiểu rõ giá trị của Kubernetes, chúng ta cần nhìn lại quá trình phát triển của việc triển khai ứng dụng qua ba giai đoạn chính:

![Evolution of Deployment](/images/1/00010.svg)

**Giai Đoạn Traditional Deployment**: Trong thời kỳ đầu, các ứng dụng chạy trực tiếp trên physical servers. Điều này dẫn đến nhiều thách thức về resource allocation, khi không có cách hiệu quả để kiểm soát việc phân bổ tài nguyên giữa các ứng dụng, dẫn đến tình trạng resource contention và underutilization.

**Giai Đoạn Virtualized Deployment**: Công nghệ virtualization cho phép chạy nhiều Virtual Machines (VMs) trên cùng một physical server. VMs mang lại khả năng isolation tốt hơn và tận dụng tài nguyên hiệu quả hơn. Mỗi VM hoạt động như một máy tính độc lập với đầy đủ OS stack.

**Giai Đoạn Container Deployment**: Container technology đại diện cho bước tiến mới nhất, cung cấp một môi trường lightweight và portable hơn so với VMs. Containers chia sẻ host OS kernel nhưng vẫn duy trì tính isolation ở mức process level.

#### Lợi Ích của Container Technology

Container technology mang lại nhiều ưu điểm quan trọng cho DevOps workflow:

1. **Agile Application Creation and Deployment**: Đơn giản hóa quy trình build và deploy container images so với VM images.

2. **CI/CD**: Hỗ trợ build, test và deployment liên tục với khả năng rollback nhanh chóng.

3. **Dev/Ops Separation**: Tách biệt concerns giữa development và operations teams.

4. **Observability**: Cung cấp visibility không chỉ về OS metrics mà còn về application health.

5. **Environmental Consistency**: Đảm bảo môi trường development, testing và production nhất quán.

6. **Cloud and OS Distribution Portability**: Có thể chạy trên nhiều nền tảng cloud và OS distributions khác nhau.

#### Vai Trò và Ứng Dụng của Kubernetes

Kubernetes đảm nhận vai trò quan trọng trong việc quản lý container trong môi trường production. Khi hệ thống của bạn phải đảm bảo high availability và zero downtime, việc quản lý container một cách thủ công trở nên không khả thi. Kubernetes cung cấp framework mạnh mẽ để orchestrate distributed systems, tự động hóa nhiều tác vụ quan trọng:

#### Service Discovery và Load Balancing
Kubernetes tích hợp DNS service discovery và load balancing nâng cao. Mỗi container có thể được exposed thông qua DNS name hoặc IP address riêng. Khi traffic tới một service tăng cao, Kubernetes tự động phân phối network traffic để đảm bảo system stability và performance.

#### Storage Orchestration
Kubernetes cho phép tự động mount storage systems theo nhu cầu. Storage có thể đến từ local storage, cloud providers (như AWS EBS), hoặc shared network storage systems (như NFS). Việc quản lý storage được abstracted away từ application layer.

#### Automated Rollouts và Rollbacks
Kubernetes sử dụng declarative approach để quản lý application state. Bạn định nghĩa desired state, và Kubernetes controller sẽ liên tục điều chỉnh actual state để match với desired state. Điều này cho phép:
- Zero-downtime deployments
- Automated rollbacks khi phát hiện issues
- Phân bổ resources một cách thông minh

#### Bin Packing Tự Động
Kubernetes optimizer có thể tự động phân bổ container workloads across node clusters dựa trên resource requirements và constraints. Điều này tối ưu hóa việc sử dụng infrastructure resources và tiết kiệm chi phí.

#### Self-healing
Kubernetes platform tích hợp nhiều self-healing capabilities:
- Tự động restart failed containers
- Replace và reschedule containers khi node fails
- Kill containers không phản hồi health check
- Không expose containers tới clients cho đến khi ready

#### Secrets và Configuration Management 
Kubernetes cung cấp secure way để manage sensitive information như:
- Passwords
- OAuth tokens  
- SSH keys
- TLS certificates

Các sensitive data này được quản lý và cập nhật mà không cần rebuild container images hoặc expose secrets trong stack configuration.

#### Giới Hạn và Scope của Kubernetes

Mặc dù mạnh mẽ, Kubernetes không phải là giải pháp "silver bullet" cho mọi use case. Một số điểm quan trọng cần lưu ý:

#### Không Phải Traditional PaaS
Kubernetes cung cấp building blocks cho container orchestration nhưng không phải là full PaaS solution. Nó:
- Không prescribe logging, monitoring hay alerting solutions
- Không force specific configuration language/system
- Không provide built-in CI/CD pipeline

#### Application Workload Flexibility
Kubernetes designed để support diverse workloads:
- Stateless applications
- Stateful applications  
- Data processing workloads
- Batch jobs

Tuy nhiên, application phải có thể containerized để chạy trên Kubernetes.

#### Amazon EKS (Elastic Kubernetes Service)

Amazon EKS là managed Kubernetes service trên AWS cloud platform. EKS eliminated overhead của việc manually managing Kubernetes control plane, cho phép teams focus vào application development và deployment.

#### Core Features của Amazon EKS

##### Secure Networking và Authentication
EKS deep integration với AWS networking và security services:
- Native integration với VPC networking
- AWS IAM authentication cho Kubernetes clusters
- Support cho security groups và network policies
- Automated certificate management

##### Scalability
EKS provides enterprise-grade scalability:
- Horizontal pod autoscaling based on metrics
- Cluster autoscaling để add/remove nodes
- Support cho multiple node groups
- Cross-zone high availability

##### Managed Experience  
EKS simplified cluster management thông qua:
- eksctl CLI tool
- AWS Management Console
- AWS CLI và APIs
- Infrastructure as Code với Terraform
- Native kubectl support

##### High Availability
EKS designed for reliability:
- Control plane runs across multiple Availability Zones
- Automated failover
- Managed etcd cluster
- Automated backup và restore

##### AWS Service Integration
EKS tích hợp seamlessly với AWS ecosystem:
- Container registry (ECR)
- Load balancing (ALB/NLB)
- IAM for authentication
- CloudWatch for monitoring
- AWS App Mesh for service mesh
- AWS CloudTrail for audit logging

Qua đó, EKS cung cấp production-ready Kubernetes platform với enterprise features và AWS reliability.