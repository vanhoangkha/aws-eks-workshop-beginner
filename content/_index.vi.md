---
title: "Làm quen với Amazon Elastic Kubernetes Service"
weight: 1
chapter: false
---

# Làm quen với Amazon Elastic Kubernetes Service (EKS)

#### Tổng quan

Amazon Elastic Kubernetes Service (EKS) là một dịch vụ được quản lý đầy đủ giúp bạn chạy Kubernetes trên AWS mà không cần phải cài đặt và duy trì control plane riêng. Workshop này sẽ giới thiệu cho bạn những kiến thức cơ bản về EKS và cách triển khai ứng dụng trên nền tảng này.

#### Mục tiêu học tập

Sau khi hoàn thành workshop này, bạn sẽ có khả năng:

1. Hiểu được kiến trúc cơ bản của Kubernetes và cách nó hoạt động trên AWS
2. Thiết lập và quản lý một cụm EKS từ đầu đến cuối
3. Triển khai các ứng dụng web đơn giản trên EKS
4. Sử dụng các công cụ phổ biến như Kustomize và Helm để quản lý ứng dụng

#### Giới thiệu về Kubernetes

Kubernetes, thường được viết tắt là K8s, là một nền tảng điều phối container mã nguồn mở được phát triển bởi Google. Dự án này được xây dựng dựa trên hơn 15 năm kinh nghiệm vận hành workload quy mô lớn tại Google, kết hợp với những đóng góp tốt nhất từ cộng đồng.

Tên gọi "Kubernetes" có nguồn gốc từ tiếng Hy Lạp (κυβερνήτης), có nghĩa là "người lái tàu" hoặc "hoa tiêu" - một cái tên phản ánh chính xác vai trò của nó trong việc điều hướng và quản lý các container trong môi trường cloud.

#### Nội dung chương trình

Trong workshop này, chúng ta sẽ tìm hiểu:

1. Kiến trúc cơ bản của Kubernetes:
   - Control plane và worker nodes
   - Các thành phần chính như API server, etcd, scheduler
   - Cách các components tương tác với nhau

2. Triển khai ứng dụng trên EKS:
   - Tạo và cấu hình cụm EKS
   - Viết manifests cho Kubernetes
   - Triển khai và quản lý các Deployments

3. Công cụ và best practices:
   - Sử dụng Kustomize để quản lý cấu hình
   - Làm quen với Helm charts
   - Các phương pháp triển khai và monitoring hiệu quả

#### Yêu cầu tiên quyết

Để tham gia workshop này một cách hiệu quả, bạn nên có:
- Kiến thức cơ bản về Docker và containers
- Tài khoản AWS với đầy đủ quyền hạn cần thiết
- Công cụ kubectl và AWS CLI đã được cài đặt
- Hiểu biết căn bản về command line và YAML