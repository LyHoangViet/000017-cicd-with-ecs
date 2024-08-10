+++
title = "Giới thiệu"
date = 2021
weight = 1
chapter = false
+++

# Triển khai ứng dụng với CI/CD Pipeline trên Amazon Elastic Container Service

{{% notice note %}}
Bài thực hành này yêu cầu bạn đã thực hiện bài thực hành [Triển khai ứng dụng trên ECS](https://000016.awsstudygroup.com/). Việc triển khai thử ứng dụng lên ECS sẽ làm tiền đề để áp dụng CI/CD Pipeline vào việc khởi xây dựng và triển khai ứng dụng một các tự động.
{{% /notice %}}

#### Amazon Elastic Container Service (ECS)
**Amazon ECS** là dịch vụ quản lý **container** với khả năng mở rộng cao cho phép đơn giản hóa việc chạy, ngừng chạy và quản lý các container trong cluster. Container sẽ được định nghĩa trong các task definition nhằm chạy các task đơn lẻ hoặc nhiều task trong một service.

#### CI/CD Pipeline là gì?
CI/CD Pipeline (Continuous Integration/Continuous Delivery or Continuous Deployment Pipeline) là một quy trình tự động hóa giúp tích hợp, kiểm thử và triển khai phần mềm một cách liên tục. CI/CD Pipeline là một phần quan trọng của DevOps, giúp đội ngũ phát triển và vận hành phần mềm làm việc hiệu quả hơn bằng tự động hóaTự động hóa, phát hiện lỗi sớm, triển khai nhanh chóng, cải thiện chất lượng phần mềm.

#### Nội dung cần làm
Sau khi xây dựng và thực thi Service trong một Cluster, chúng ta có thể thực hiện các yêu cầu thay đổi liên quan đến cấu hình như số lượng Tasks, bổ sung hoặc thay đổi Containers cùng những giá trị CPU, Memory… bên trong Task Definition Revision.

Để thực hiện những thay đổi này, ECS cung cấp 3 phương pháp sau:
Rolling update: thực thi bởi ECS, sử dụng service scheduler để cập nhật phiên bản mới của Container. Trong quá trình cập nhật, số lượng Tasks thêm vào hoặc loại bỏ được cấu hình thông qua những giá trị:

Minimum healthy percent: giá trị cận dưới của Tasks cần duy trì ở trạng thái RUNNING / so với Tasks mong muốn (khai báo trong Auto Scaling).
Maximum percent: giá trị cận trên của Tasks cần duy trì ở trạng thái RUNNING hoặc PENDING / so với Tasks mong muốn (khai báo trong Auto Scaling).
Blue/Green: thực thi bởi CodeDeploy, duy trì hai phiên bản: product (BLUE) / test (GREEN). Trong quá trình triển khai, lưu lượng dữ liệu gửi đến servie dần dịch chuyển từ BLUE sang GREEN theo một trong những cách thức:

Canary: chia lưu lượng thành 2 phần và xác định khoảng thời gian thực thi quá trình chuyển đổi. Ví dụ:
CodeDeployDefault.ECSCanary10Percent5Minutes: chuyển 10% trong phần đầu tiên, và 90% còn lại sau 5 phút.
CodeDeployDefault.ECSCanary10Percent15Minutes: chuyển 10% trong phần đầu tiên, và 90% còn lại sau 15 phút.
Linear: chia lưu lượng thành các phần bằng nhau và xác định khoảng thời gian. Ví dụ:
CodeDeployDefault.ECSLinear10PercentEvery1Minutes: chuyển 10% sau mỗi 1 phút cho đến khi kết thúc toàn bộ.
CodeDeployDefault.ECSLinear10PercentEvery3Minutes: chuyển 10% sau mỗi 3 phút cho đến khi kết thúc toàn bộ.
All-at-one: Toàn bộ lưu lượng được chuyển dịch từ BLUE sang GREEN cùng lúc.
External: thực thi bởi deployment controller từ một bên thứ ba (third-party) dựa trên các Service/Task APIs.


#### Nội dung chính

1. [Các bước chuẩn bị](1-create-new-aws-account/)
2. [Tạo AWS Gitlab](2-mfa-setup-for-aws-user-(root)/)
3. [Tạo CodeBuild](3-create-admin-user-and-group/)
4. [Tạo CodePipeline](4-verify-new-account/)
5. [Khắc phục lỗi](4-verify-new-account/)
6. [Dọn dẹp tài nguyên](4-verify-new-account/)
