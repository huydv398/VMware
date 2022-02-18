# What is Alarm
là các thông báo xảy ra để phản ứng với các sự kiện hoặc điều kiện nhất định xảy ra với một đối tượng trong vCenter Server. Có thể tạo cảnh báo cho các đối tượng vCenter Server như máy ảo, máy chủ ESXi, mạng và kho dữ liệu.

Dựa trên đối tượng, các cảnh báo này có thể theo dõi mức tiêu thụ tài nguyên hoặc trạng thái của đối tượng và cảnh báo cho bạn khi các điều kiện nhất định đã được đáp ứng, chẳng hạn như sử dụng tài nguyên cao hoặc dung lượng đĩa thấp. Cảnh báo rất hữu ích vì chúng cho phép bạn chủ động hơn trong việc quản lý môi trường vSphere của mình.

Mỗi loại cảnh báo có ba loại hành động chung:
* **Send a notification email**: Nhận thông báo về email
* **Send a notification trap**: Thông báo bằng giao thức SNMP
* **Run a command**:  chạy một tập lệnh (Script) để khắc phục sự cố mà đối tượng đang gặp phải.

vCenter Server có một số cảnh báo được tích hợp sẵn. Chúng có thể được sử dụng cho các mục đích chung, chẳng hạn như thông báo cho bạn khi trạng thái nguồn của máy chủ thay đổi, kho dữ liệu sắp hết dung lượng đĩa, mức sử dụng CPU máy ảo cao, v.v. Bạn cũng có thể tạo báo thức của riêng mình, nếu báo động mặc định cũng vậy chung cho các mục đích của bạn.