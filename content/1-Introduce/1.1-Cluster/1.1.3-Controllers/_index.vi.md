---
title: "Controllers trong Kubernetes"
weight: 3
chapter: false
pre: "<b> 1.1.3 </b>"
---


#### Giới thiệu về Control Loop

Trong lĩnh vực robotics và automation, **Control Loop** (vòng lặp điều khiển) là một quy trình lặp đi lặp lại liên tục nhằm điều chỉnh trạng thái của hệ thống.

Để minh họa khái niệm **Control Loop**, hãy xem xét ví dụ về thermostat (bộ điều nhiệt) trong phòng:
- Khi người dùng cài đặt nhiệt độ mong muốn, họ đang định nghĩa desired state (trạng thái mong muốn)
- Nhiệt độ hiện tại trong phòng chính là current state (trạng thái hiện tại)
- Thermostat sẽ liên tục điều chỉnh để đưa current state tiến gần hơn đến desired state thông qua việc bật/tắt các thiết bị điều hòa

#### Controllers trong Kubernetes

Trong hệ thống Kubernetes, **Controllers** là các **Control Loop** có nhiệm vụ giám sát trạng thái của cluster và thực hiện các thay đổi cần thiết. Mỗi Controller đảm bảo current state của cluster luôn hướng tới desired state đã được định nghĩa.

![Kubernetes Controller](/images/1/1/3/0002.png?featherlight=false&width=60pc)

#### Controller Pattern

#### Cơ chế hoạt động
Controller theo dõi ít nhất một loại Kubernetes resource. Mỗi resource có một trường **spec** đại diện cho desired state. Controller chịu trách nhiệm điều chỉnh current state tiến gần hơn đến desired state được định nghĩa trong **spec**.

#### Control thông qua API Server
**Job Controller** là một ví dụ điển hình về built-in controller trong Kubernetes. Các built-in controller tương tác với cluster's API server để quản lý trạng thái.

**Job** là một Kubernetes resource có nhiệm vụ thực thi một hoặc nhiều Pod để hoàn thành một tác vụ cụ thể. Khi Job Controller phát hiện một Job mới, nó sẽ:
1. Đảm bảo đúng số lượng Pod được chạy trên các Node trong cluster
2. Không trực tiếp quản lý Pod/container
3. Giao tiếp với API server để tạo/xóa Pod

#### Direct Control
Một số controller cần thực hiện các thay đổi với các thành phần bên ngoài cluster. Ví dụ như controller quản lý số lượng Node trong cluster sẽ cần tương tác với cloud provider để tạo/xóa Node khi cần thiết.

#### Desired State vs Current State

Kubernetes quản lý hệ thống theo hướng cloud-native, cho phép xử lý các thay đổi linh hoạt:
- Cluster có thể thay đổi bất cứ lúc nào
- Control loop tự động khắc phục lỗi
- Cluster không nhất thiết phải đạt trạng thái ổn định tuyệt đối

#### Design Principles

Kubernetes sử dụng multiple controllers, mỗi controller quản lý một khía cạnh cụ thể của cluster state. Thông thường, một controller sẽ:
- Sử dụng một resource type làm desired state
- Quản lý một resource type khác để đạt được desired state

#### Deployment Options

### Built-in Controllers
- Chạy trong kube-controller-manager
- Cung cấp core behaviors cho Kubernetes
- Hỗ trợ high availability thông qua controller plane redundancy

#### Custom Controllers  
- Có thể chạy bên ngoài control plane
- Được sử dụng để extend Kubernetes functionality
- Có thể được triển khai như Pod hoặc external service

{{% notice note %}}
Nhiều controller có thể cùng tạo/cập nhật một loại object. Kubernetes đảm bảo mỗi controller chỉ quản lý các resource được liên kết với nó thông qua labels và selectors.
![Kubernetes Controllers](/images/1/1/3/0003.png?featherlight=false&width=60pc)
{{% /notice %}}