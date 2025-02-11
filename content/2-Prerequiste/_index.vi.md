---
title: "Các Bước Chuẩn Bị"
weight: 2
chapter: false
pre: "<b> 2. </b>"
---


#### Giới thiệu

Trước khi bắt đầu thực hành với bộ workshop Amazon Elastic Kubernetes Service (Amazon EKS), bạn cần hoàn thành ba bước chuẩn bị quan trọng sau đây. Những bước này sẽ đảm bảo môi trường của bạn được cấu hình đúng cách và sẵn sàng cho việc triển khai các workload trên Kubernetes.

#### Chuẩn bị môi trường AWS

Bước đầu tiên là thiết lập môi trường làm việc của bạn với AWS. Quá trình này bao gồm:

- Cấu hình AWS credentials để xác thực và kết nối với tài khoản AWS của bạn
- Cài đặt và cấu hình AWS CLI để tương tác với các dịch vụ AWS thông qua command line
- Thiết lập Integrated Development Environment (IDE) phù hợp cho việc phát triển
- Tạo cấu trúc thư mục source code theo tiêu chuẩn

#### Khởi tạo Amazon EKS Cluster

Tiếp theo, bạn sẽ cần tạo một EKS cluster để chạy các Kubernetes workload. Bạn có hai lựa chọn để provisioning cluster:

- Sử dụng AWS CloudFormation template để tự động hóa việc tạo infrastructure
- Áp dụng Infrastructure as Code với Terraform để quản lý tài nguyên AWS

#### Tìm hiểu cấu trúc Laboratory

Bước cuối cùng là làm quen với cấu trúc của các bài lab trong workshop. Điều này sẽ giúp bạn:

- Hiểu rõ flow của các bài thực hành
- Nắm được các thành phần và tài nguyên sẽ được sử dụng
- Chuẩn bị tốt cho việc thực hiện các lab tiếp theo

Mỗi bước trên đều được thiết kế để đảm bảo bạn có một nền tảng vững chắc trước khi đi vào các phần thực hành chuyên sâu với Amazon EKS.