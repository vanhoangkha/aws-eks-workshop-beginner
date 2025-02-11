---
title: "Giao tiếp giữa các Node và Control Plane trong Kubernetes"
weight: 2
chapter: false
pre: "<b> 1.1.2 </b>"
---


Tài liệu này mô tả chi tiết các kênh giao tiếp giữa API Server và các thành phần khác trong cụm Kubernetes. Việc hiểu rõ các kênh giao tiếp này giúp người quản trị có thể tối ưu hóa cấu hình mạng, đặc biệt khi triển khai cụm trên môi trường mạng không đáng tin cậy hoặc trên public cloud.

![Kiến trúc giao tiếp Control Plane và Nodes](/images/1/1/2/0001.svg?featherlight=false&width=60pc)

#### Hướng giao tiếp từ Node tới Control Plane

Kubernetes sử dụng mô hình API hub-and-spoke, trong đó mọi tương tác API đều phải đi qua API Server. API Server là thành phần duy nhất trong Control Plane được thiết kế để tiếp nhận các kết nối từ xa. Cụ thể:

- API Server lắng nghe các kết nối HTTPS bảo mật trên cổng 443 (mặc định)
- Hỗ trợ nhiều cơ chế xác thực client khác nhau
- Yêu cầu cấu hình authorization, đặc biệt khi cho phép anonymous requests hoặc service account tokens

Để đảm bảo kết nối an toàn, các node cần được cung cấp:
- Cluster root CA certificate để xác thực API Server
- Client credentials hợp lệ (thường là client certificate cho kubelet thông qua TLS bootstrap)

Đối với Pod muốn kết nối tới API Server:
- Sử dụng service account được Kubernetes tự động inject:
  - Root CA certificate 
  - Valid bearer token
- Có thể truy cập API Server thông qua Kubernetes service (default namespace) được kube-proxy route tới HTTPS endpoint

#### Hướng giao tiếp từ Control Plane tới Node

#### 1. API Server tới Kubelet

Kết nối này được sử dụng cho các mục đích:
- Truy xuất pod logs
- Port-forward tới pod
- Attach vào pod đang chạy (thường qua kubectl)

Đặc điểm kỹ thuật:
- Kết thúc tại HTTPS endpoint của kubelet
- Mặc định API Server không verify kubelet serving certificate
- Có thể bị tấn công man-in-the-middle
- Cần thêm các biện pháp bảo mật:
  - Sử dụng --kubelet-certificate-authority flag
  - Thiết lập SSH Tunnel khi cần
  - Enable kubelet authentication/authorization

#### 2. API Server tới Node, Pod và Service 

Đặc điểm của kênh giao tiếp này:
- Mặc định là plain HTTP
- Không có authentication/encryption
- Có thể nâng cấp lên HTTPS bằng cách thêm prefix https:// trong API URL
- Tuy nhiên vẫn tồn tại giới hạn:
  - Không verify endpoint certificate
  - Không cung cấp client credentials
  - Chỉ có encryption, không đảm bảo integrity
  - Không an toàn trên mạng không tin cậy/public

Người quản trị cần cân nhắc các biện pháp bảo mật bổ sung khi triển khai trên môi trường production, đặc biệt là public cloud hoặc mạng không đáng tin cậy.