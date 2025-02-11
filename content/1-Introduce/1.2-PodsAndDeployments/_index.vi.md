---
title: "Pod và Deployment"
weight: 2
chapter: false
pre: "<b> 1.2 </b>"
---


#### Pod - Đơn vị Cơ bản của Kubernetes

Pod là đơn vị triển khai nhỏ nhất và cơ bản nhất trong kiến trúc Kubernetes. Thay vì triển khai container trực tiếp lên worker node, Kubernetes sử dụng Pod như một wrapper để quản lý và điều phối container.

#### Đặc điểm của Pod

Một Pod có thể chứa một hoặc nhiều container, tuy nhiên best practice là mỗi Pod chỉ nên chứa một container chính để đảm bảo tính modularity và maintainability. Khi triển khai microservices trên Kubernetes, mỗi Pod thường đại diện cho một instance của service.

#### Triển khai Pod trên EKS

Để triển khai một Pod nginx đơn giản trên Amazon EKS, sử dụng kubectl command sau:

```bash
kubectl run nginx --image nginx
```

Kiểm tra trạng thái Pod:

```bash
kubectl get pods
```

#### Deployment - Quản lý Pod và ReplicaSet

Deployment là một resource cao cấp trong Kubernetes, cung cấp khả năng khai báo cập nhật cho Pod và ReplicaSet. Deployment Controller đảm bảo trạng thái thực tế của cluster khớp với trạng thái mong muốn được định nghĩa trong manifest.

#### Use Cases của Deployment

Deployment thường được sử dụng trong các tình huống sau:

1. Rolling update và rollback application
2. Scale số lượng replica của ứng dụng
3. Quản lý version của container image
4. Tự động recovery khi Pod gặp sự cố

#### Cấu hình Deployment trên EKS

Ví dụ về Deployment manifest (`deployment-definition.yaml`):

```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: nginx-deployment
  labels:
    app: nginx
spec:
  replicas: 3
  selector:
    matchLabels:
      app: nginx
  template:
    metadata:
      labels:
        app: nginx
    spec:
      containers:
      - name: nginx
        image: nginx:1.14.2
        ports:
        - containerPort: 80
```

#### Quản lý Deployment

Triển khai Deployment:

```bash
kubectl create -f deployment-definition.yaml
```

Kiểm tra status:

```bash
kubectl get deployment
kubectl get replicaset
kubectl get pods
kubectl get all
```

#### Best Practices

1. Sử dụng resource requests và limits cho Pod
2. Implement health checks và readiness probes
3. Cấu hình pod disruption budget để đảm bảo high availability
4. Sử dụng rolling update strategy để minimize downtime
5. Implement proper labeling và tagging cho resource management

#### Integration với AWS Services

Khi triển khai trên Amazon EKS, Pod và Deployment có thể tích hợp với nhiều AWS service:

- Amazon CloudWatch để monitoring và logging
- AWS IAM để authentication và authorization
- Amazon ECR để container image storage
- AWS Load Balancer để expose service

#### Tham khảo

- [Amazon EKS Documentation](https://docs.aws.amazon.com/eks/)
- [Kubernetes Official Documentation](https://kubernetes.io/docs/)
- [AWS Container Services Best Practices](https://aws.amazon.com/containers/best-practices/)

{{% notice note %}}
Khi làm việc với Deployment trên EKS, cần đảm bảo tuân thủ AWS Well-Architected Framework và security best practices.
{{% /notice %}}