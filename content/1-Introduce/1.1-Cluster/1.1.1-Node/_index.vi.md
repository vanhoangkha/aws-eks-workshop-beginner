---
title: "Nodes trong Kubernetes"
weight: 1
chapter: false
pre: "<b> 1.1.1 </b>"
---



#### Tổng quan

**Kubernetes** là nền tảng điều phối container, vận hành workload của bạn bằng cách đặt các container vào trong **Pods** và triển khai chúng trên các **Nodes**. Một node có thể là máy ảo (Virtual Machine) hoặc máy vật lý (Physical Machine), phụ thuộc vào cấu trúc của cluster. Mỗi node được quản lý bởi control plane và chứa các service thiết yếu để vận hành **Pods**.

![Kiến trúc Kubernetes](/images/1/1/1/0001.png?featherlight=false&width=40pc)

Trong môi trường production, một Kubernetes cluster thường bao gồm nhiều **nodes** để đảm bảo tính sẵn sàng cao và khả năng mở rộng. Tuy nhiên, trong môi trường development hoặc learning, việc sử dụng single-node cluster là phổ biến để tiết kiệm tài nguyên.

Mỗi **node** bao gồm ba thành phần core:
- **kubelet**: Agent chạy trên mỗi node
- Container runtime: Phần mềm thực thi container
- **kube-proxy**: Network proxy để thực hiện các service networking

#### Cơ chế quản lý Node

Kubernetes hỗ trợ hai phương thức để thêm Node vào API Server:

1. Self-registration: Kubelet tự động đăng ký với Control Plane
2. Manual registration: Administrator thực hiện thêm Node object

Sau khi Node được tạo, Control Plane sẽ validate Node object. Ví dụ về manifest để tạo Node:

```json
{
  "kind": "Node",
  "apiVersion": "v1",
  "metadata": {
    "name": "10.240.79.157",
    "labels": {
      "name": "my-first-k8s-node"
    }
  }
}
```

#### Node Identity và Status

#### Unique Node Name
Mỗi Node trong cluster phải có tên duy nhất. Kubernetes sử dụng tên này để định danh Node và theo dõi trạng thái của nó. Khi cần thay đổi cấu hình Node, administrator cần xóa Node object hiện tại và tạo lại với cấu hình mới.

#### Node Status 
Node status bao gồm các thông tin quan trọng:

- Addresses: Địa chỉ network của node
- Conditions: Trạng thái hoạt động của node
- Capacity & Allocatable: Tài nguyên có sẵn và có thể phân bổ
- Info: Thông tin hệ thống

Administrator có thể kiểm tra status của Node bằng lệnh:

```bash
kubectl describe node <node-name>
```

#### Resource Management

Node object theo dõi thông tin về compute resources (CPU, memory) của Node. Đối với self-registered nodes, thông tin này được báo cáo tự động trong quá trình registration. Với manually-added nodes, administrator cần khai báo resource capacity khi tạo Node.

Kubernetes scheduler đảm bảo resource utilization hiệu quả bằng cách:
- Kiểm tra tổng resource requests của tất cả Pods trên Node
- So sánh với available capacity của Node
- Chỉ schedule Pods mới khi Node có đủ tài nguyên

Việc theo dõi resource chỉ áp dụng cho các containers được quản lý bởi kubelet, không bao gồm các containers được khởi động trực tiếp bởi container runtime hoặc các processes chạy ngoài kubelet control.