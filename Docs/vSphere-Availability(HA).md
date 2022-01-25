About vSphere Availability

**vSphere Availability** - mô tả các giải pháp cung cấp tính liên tục trong kinh doanh, bao gồm cách thiết lập vSphere® Tính khả dụng cao (HA) và Khả năng chịu lỗi vSphere.

Phần mềm VMware cung cấp mức độ sẵn sàng cao hơn cho các ứng dụng quan trọng trở nên đơn giản và ít tốn kém hơn. Với vSphere, bạn có thể tăng mức độ sẵn sàng cơ bản được cung cấp cho tất cả các ứng dụng và cung cấp mức độ sẵn sàng cao hơn một cách dễ dàng hơn và tiết kiệm chi phí. Với vSphere, bạn có thể:

* Cung cấp tính khả dụng cao không phụ thuộc vào phần cứng, hệ điều hành và ứng dụng.
* Giảm thời gian chết theo kế hoạch cho các hoạt động bảo trì thông thường.
* Cung cấp khả năng phục hồi tự động trong các trường hợp bị lỗi.

## vSphere HA cung cấp khả năng phục hồi nhanh chóng khi ngừng hoạt động

vSphere HA tận dụng nhiều máy chủ ESXi được định cấu hình như một cụm để cung cấp khả năng phục hồi nhanh chóng sau sự cố và tính sẵn sàng cao với chi phí hiệu quả cho các ứng dụng chạy trong máy ảo.

vSphere HA bảo vệ tính khả dụng của ứng dụng theo những cách sau:

* Nó bảo vệ khỏi sự cố máy chủ bằng cách khởi động lại máy ảo trên các máy chủ khác trong cụm.
* Nó bảo vệ khỏi lỗi ứng dụng bằng cách liên tục theo dõi máy ảo và đặt lại nó trong trường hợp phát hiện lỗi.
* Nó bảo vệ khỏi các lỗi khả năng truy cập kho dữ liệu bằng cách khởi động lại các máy ảo bị ảnh hưởng trên các máy chủ khác vẫn có quyền truy cập vào kho dữ liệu của chúng.
* Nó bảo vệ các máy ảo khỏi sự cô lập của mạng bằng cách khởi động lại chúng nếu máy chủ của chúng bị cô lập trên mạng quản lý hoặc vSAN . Bảo vệ này được cung cấp ngay cả khi mạng đã được phân vùng.
Không giống như các giải pháp phân cụm khác, vSphere HA cung cấp cơ sở hạ tầng để bảo vệ tất cả khối lượng công việc với cơ sở hạ tầng:

* Bạn không cần phải cài đặt phần mềm đặc biệt trong ứng dụng hoặc máy ảo. Tất cả khối lượng công việc được bảo vệ bởi vSphere HA. **Sau khi vSphere HA được cấu hình, không cần thực hiện hành động nào để bảo vệ các máy ảo mới. Chúng được bảo vệ tự động.**
* Bạn có thể kết hợp vSphere HA với vSphere Distributed Resource Scheduler (DRS) để bảo vệ khỏi các lỗi và cung cấp khả năng cân bằng tải trên các máy chủ trong một cụm.
## vSphere HA có một số ưu điểm so với các giải pháp chuyển đổi dự phòng truyền thống
* **Thiết lập tối thiểu**</br>Sau khi một cụm vSphere HA được thiết lập, tất cả các máy ảo trong cụm đều được hỗ trợ chuyển đổi dự phòng mà không cần cấu hình bổ sung.
* **Giảm chi phí phần cứng và thiết lập**</br>Máy ảo hoạt động như một bộ chứa di động cho các ứng dụng và nó có thể được di chuyển giữa các máy chủ. Quản trị viên tránh trùng lặp cấu hình trên nhiều máy. Khi bạn sử dụng vSphere HA, bạn phải có đủ tài nguyên để không vượt quá số lượng máy chủ mà bạn muốn bảo vệ bằng vSphere HA. Tuy nhiên, hệ thống VMware vCenter Server ® tự động quản lý tài nguyên và cấu hình các cụm.
* **Tăng tính khả dụng của ứng dụng**</br>Bất kỳ ứng dụng nào chạy bên trong máy ảo đều có quyền truy cập để tăng tính khả dụng. Vì máy ảo có thể phục hồi sau lỗi phần cứng, nên tất cả các ứng dụng khởi động khi khởi động đều có tính khả dụng cao hơn mà không cần tăng nhu cầu tính toán, ngay cả khi bản thân ứng dụng đó không phải là ứng dụng được phân cụm. Bằng cách giám sát và phản hồi nhịp tim của VMware Tools và khởi động lại các máy ảo không phản hồi, nó bảo vệ khỏi sự cố hệ điều hành khách.
* **Tích hợp DRS và vMotion**</br>Nếu một máy chủ bị lỗi và các máy ảo được khởi động lại trên các máy chủ khác, DRS có thể đưa ra các đề xuất di chuyển hoặc di chuyển các máy ảo để phân bổ tài nguyên cân bằng. Nếu một hoặc cả hai máy chủ nguồn và máy đích của quá trình di chuyển bị lỗi, vSphere HA có thể giúp khôi phục sau lỗi đó.