---
title: "Chuẩn bị môi trường"
weight: 1
chapter: false
pre: "<b> 2.1 </b>"
---



#### Tạo CloudFormation Stack

Để thiết lập môi trường phát triển, chúng ta sẽ sử dụng AWS CloudFormation để triển khai các tài nguyên cần thiết. Bắt đầu bằng việc tải template CloudFormation từ [GitHub repository](https://github.com/aws-samples/eks-workshop-v2/releases/download/release-snapshot-631eaeb7/ide-cfn.yaml).

Truy cập vào [AWS CloudFormation Console](console.aws.amazon.com/cloudformation/home) và thực hiện các bước sau:

1. Chọn "Create Stack" để bắt đầu quá trình tạo stack mới
2. Điền các thông tin cơ bản:
   - Stack Name: Đặt tên cho stack của bạn
   - Environment Name: Xác định tên môi trường

Các tham số còn lại có thể giữ nguyên giá trị mặc định hoặc tùy chỉnh theo nhu cầu. Quá trình tạo stack sẽ mất khoảng 4-5 phút để hoàn thành. Sau khi hoàn tất, chuyển đến tab "Outputs" để lấy thông tin truy cập IDE.

#### Truy cập Visual Studio Code Web IDE

Trong tab Outputs của CloudFormation stack, bạn sẽ thấy hai thông tin quan trọng:

- `IdeUrl`: URL để truy cập Web IDE
- `IdePasswordSecret`: Link đến AWS Secrets Manager chứa mật khẩu truy cập

#### Lấy mật khẩu truy cập

1. Mở link `IdePasswordSecret` trong AWS Secrets Manager
2. Nhấn nút "Retrieve secret value" để lấy mật khẩu
3. Sao chép mật khẩu được hiển thị

#### Đăng nhập vào IDE

1. Truy cập URL từ `IdeUrl` trong trình duyệt
2. Nhập mật khẩu đã sao chép khi được yêu cầu
3. Sau khi xác thực thành công, bạn sẽ thấy giao diện Visual Studio Code Web

#### Xử lý lỗi CloudFront Distribution

Trong trường hợp gặp lỗi khi tạo CloudFront Distribution do chưa xác thực tài khoản, thực hiện các bước sau để yêu cầu nâng giới hạn:

1. Truy cập [AWS Support Center](https://support.console.aws.amazon.com/support/home#/case/create?issueType=service-limit-increase)
2. Tạo case yêu cầu nâng giới hạn:
   - Service: Chọn "CloudFront Distribution"
   - Quota: Chọn "Web Distributions per Account"
   - New limit value: Nhập giá trị cao hơn giới hạn hiện tại
   - Case description: Cung cấp mã lỗi và mô tả chi tiết vấn đề

Sau khi gửi yêu cầu, theo dõi case và tương tác với AWS Support để được hỗ trợ xử lý.

#### Kiểm tra cấu hình AWS CLI

Để xác nhận môi trường đã được thiết lập đúng, chạy lệnh sau trong terminal:

```bash
aws sts get-caller-identity
```

Bước tiếp theo là [thiết lập cluster EKS](../../../../2.2-cluster-creation/) để tiếp tục workshop.

#### Note

Quá trình xác thực tài khoản và nâng hạn mức có thể mất một khoảng thời gian. Hãy kiên nhẫn và tích cực tương tác với AWS Support để đẩy nhanh quá trình xử lý.