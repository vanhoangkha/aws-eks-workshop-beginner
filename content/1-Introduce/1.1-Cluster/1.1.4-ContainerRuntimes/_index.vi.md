---
title: "Container Runtime"
weight: 4
chapter: false
pre: "<b> 1.1.4 </b>"
---


#### Tổng quan về Container Runtime

**Container runtime** là phần mềm nền tảng cốt lõi cho phép container hoạt động trong hệ thống máy chủ. Nó đảm nhiệm toàn bộ vòng đời của container, từ việc kéo container image từ registry đến quản lý và vận hành container trên hệ thống.

#### Chức năng và Vai trò Chính

#### Container Execution (Thực thi Container)

Container runtime thực hiện quy trình nhiều bước để vận hành container:

- Khởi tạo container và môi trường dựa trên container image chứa ứng dụng và dependencies
- Vận hành container và khởi động ứng dụng
- Quản lý toàn bộ vòng đời container bao gồm monitoring, tự động restart khi lỗi và cleanup resources

#### Host OS Interaction (Tương tác với Hệ điều hành)

Container runtime tương tác chặt chẽ với hệ điều hành host thông qua các tính năng:

- Sử dụng **namespace** và **cgroup** để isolation và quản lý tài nguyên
- Đảm bảo các process trong container không ảnh hưởng đến host hoặc container khác
- Duy trì môi trường vận hành an toàn và ổn định

#### Resource Management (Quản lý Tài nguyên)

Container runtime đóng vai trò quan trọng trong việc:

- Phân bổ và điều chỉnh CPU, memory và I/O cho từng container
- Ngăn chặn resource contention trong môi trường multi-tenant
- Quản lý hiệu quả tài nguyên hệ thống

#### Low-level và High-level Container Runtime

#### Phân loại Container Runtime

Container runtime được chia thành hai nhóm chính:

1. **Low-level Container Runtime**: Tập trung vào việc thực thi container (ví dụ: runc)
2. **High-level Container Runtime**: Cung cấp thêm các tính năng như quản lý image và API (ví dụ: **`containerd`**, **cri-o**)

#### Container Runtime trong Kubernetes 

Kubernetes sử dụng Container Runtime Interface (CRI) làm bridge giữa kubelet và container runtime. Các runtime phổ biến bao gồm:

#### Docker
- Runtime truyền thống kết hợp build, package và run container
- Sử dụng kiến trúc client/server với `dockerd` daemon
- Tích hợp **`containerd`** và `runc`

#### containerd
- High-level runtime được tách ra từ Docker
- Tập trung vào container orchestration
- Sử dụng CLI `ctr` để tương tác

#### cri-o
- CRI runtime nhẹ dành riêng cho Kubernetes
- Hỗ trợ OCI-compatible images
- Tương thích với nhiều low-level runtime

#### Tương tác với CRI Runtime

Ta có thể sử dụng công cụ `crictl` để tương tác với CRI runtime:

```bash
# Cấu hình crictl
cat <<EOF | sudo tee /etc/crictl.yaml
runtime-endpoint: unix:///run/containerd/containerd.sock
EOF

# Pull image
sudo crictl pull nginx

# Tạo và quản lý pod/container
SANDBOX_ID=$(sudo crictl runp sandbox.json)
CONTAINER_ID=$(sudo crictl create ${SANDBOX_ID} container.json sandbox.json)
```

Container runtime đóng vai trò nền tảng trong việc vận hành container và orchestration platform như Kubernetes. Việc hiểu rõ các loại runtime và cách chúng hoạt động giúp ta triển khai và vận hành container hiệu quả hơn trong môi trường production.