# Những cái mới trong phần mềm ảo hóa VMware vSphere 7

## Thông tin tổng quan

Ảo hóa VMware vSphere là một trong những nền tảng ảo hóa phần cứng tốt nhất được sử dụng trên khắp thế giới. Có thể nói, hầu hết người dùng tự động nghĩ đến ảo hóa VMware khi có nhu cầu sử dụng. Các quản trị viên hệ thống đánh giá cao VMware vì độ tin cậy, hiệu suất và khả năng sử dụng tuyệt vời của nó. 

Ngày phát hành ảo hóa VMware vSphere 7 chính thức là ngày 2/4/2020. vSphere 7 là phiên bản mới nhất của nền tảng  ảo hóa VMware bổ sung nhiều tính năng mới. Ảo hóa VMware vSphere đã được “cấu trúc lại” đáng kể cho phiên bản 7. Ở phần tiếp theo của bài viết này, hãy cùng Viettel IDC tìm hiểu kỹ hơn về phiên bản ảo hóa VMware này nhé.

Nhưng trước hết, dù bạn sử dụng phiên bản ảo hóa VMware vSphere nào đi chăng nữa thì cũng đừng quên thực hiện sao lưu VMware vSphere bao gồm các máy ảo chạy trên các máy chủ và cụm ESXi. NAKIVO Backup & Replication hỗ trợ ảo hóa VMware vSphere 7 và sao lưu các máy ảo theo cụm bao gồm cả các máy ảo có khả năng chịu lỗi. 

## Một số tính năng nổi trội của ảo hóa VMware vSphere 7

### Hỗ trợ và tích hợp Kubernetes

Docker container phổ biến trong số các nhà phát triển tạo ứng dụng bằng cách sử dụng kiến ​​trúc microservice. Kubernetes có thể chạy các container trong một cụm và cung cấp khả năng cân bằng tải, tính khả dụng và khả năng mở rộng cao. Ảo hóa VMware vSphere 7 được tích hợp hoàn toàn với Kubernetes. 

Giờ đây, quản trị viên có thể cung cấp, chạy và quản lý các cụm Kubernetes trên vSphere thông qua giao diện Kubernetes. Việc hỗ trợ cả container và máy ảo trên một nền tảng duy nhất cho phép vSphere 7 chạy các pod Kubernetes trên các máy ảo bằng cách sử dụng Dịch vụ vSphere POD. Ảo hóa VMware vSphere POD có thể được quản lý giống như các máy ảo hiện có.

### Các tính năng Clustering được cải thiện

Cụm VMware DRS (Bộ lập lịch tài nguyên phân tán) đã được cải tiến trong ảo hóa VMware vSphere 7. Giờ đây DRS có thể đảm bảo cân bằng tải cho cả máy ảo và container. Trong ảo hóa VMware vSphere 6.7, DRS kiểm tra tải của từng máy chủ ESXi trong một cụm. 

Không giống như DRS trong các phiên bản trước của vSphere, trong ảo hóa VMware vSphere 7, DRS không nhằm mục đích cân bằng tải trên máy chủ ESXi. Đây là điểm khác biệt lớn nhất. Ưu tiên chính của DRS không còn tậm trung đến việc sử dụng máy chủ ESXi mà thay vào đó là khả năng thích nghi của máy ảo. Điều này có nghĩa là nó tập trung vào việc cung cấp đủ tài nguyên cho một máy ảo. 

Trình lập lịch tài nguyên phân tán trong ảo hóa VMware vSphere 7 có thể tính toán việc sử dụng tài nguyên mỗi phút. Trong các phiên bản vSphere trước, khoảng thời gian kiểm tra tối thiểu là 5 phút. 

### VMware vMotion

VMware vMotion được sử dụng để cung cấp khả năng di chuyển VM giữa các máy chủ ESXi mà không làm gián đoạn hoạt động của VM. Các cải tiến của ảo hóa VMware vSphere 7 vMotion dẫn đến việc tiêu thụ ít tài nguyên hơn để di chuyển VM trực tiếp. Sử dụng vMotion cho khối lượng công việc lớn trở nên thuận tiện hơn. 

### Cập nhật vCenter

VCenter mới được đơn giản hóa việc quản lý và vận hành với các tính năng mới của VMware. Hiện không thể cài đặt vCenter 7 trên máy Windows. VMware vCenter 7 chỉ có thể được triển khai như một thiết bị ảo (VCSA - vCenter Server Appliance) dựa trên Photon OS (một hệ điều hành dựa trên Linux do VMware duy trì). 

Không có thêm vSphere Web Client dựa trên Flash nữa. Chỉ HTML5 vSphere Client hỗ trợ tất cả các tính năng hiện có thể được sử dụng để quản lý vCenter. Bạn không cần cài đặt thêm bất kỳ plugin hoặc tiện ích bổ sung nào trong trình duyệt Web của mình để sử dụng HTML5 vSphere Client. vCenter 7 có thể được triển khai trên máy chủ ESXi 6.5 hoặc 6.7. Không thể triển khai vCenter 7 trên ESXi 6.0. VMware vCenter 7 có thể quản lý các phiên bản sau của ESXi: ESXi 6.5, ESXi 6.7 và ESXi 7.0. Máy chủ chạy ESXi 6.0 không thể được quản lý bởi vCenter 7.

Platform Service Controller được hợp nhất thành vCenter Server 7. Việc tăng tối đa cấu hình cho vCenter 7 giúp nó hỗ trợ số lượng máy ảo và máy chủ ESXi cao hơn phiên bản vCenter 6.7:

- Ở chế độ độc lập, vCenter 7 hỗ trợ tới 2.500 máy chủ ESXi và 40.000 máy ảo dạng powered-on.

- Trong chế độ được liên kết, vCenter 7 hỗ trợ 15 vCenter trên mỗi miền SSO, 15.000 máy chủ ESXi và 150.000 máy ảo powered-on.

vCenter Server Profiles cho phép bạn áp dụng cấu hình cho nhiều máy chủ vCenter và chuẩn hóa cấu hình của máy chủ vCenter. vCenter Server Upgrade Planner là một phần của vCenter. Nó sử dụng vSphere Lifecycle Manager để thông báo cho quản trị viên hệ thống về các vấn đề tiềm ẩn với các bản cập nhật.

## Nguồn

https://viettelidc.com.vn/tin-tuc/nhung-cai-moi-trong-phan-mem-ao-hoa-vmware-vsphere-7