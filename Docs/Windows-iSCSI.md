# iSCSI - Internet Small Computer System Interface
iSCSI là tiêu chuẩn một giao thức lớp vận chuyển, nhằm mục đích truyền tải qua các lệnh SCSI qua IP hoạt động trên giao thức TCP/IP(Transport Control Protocol). Từ đó iSCSI cho phép truy cập các khối dữ liệu trên hệ thống lưu trữ SAN qua các lệnh SCSI và truyền tải dữ liệu qua hệ thống lưu trữ SAN qua các lệnh SCSI và truyền tải dữ liệu qua hệ thống mạng Network (LAN/WAN)

Lệnh iSCSI được đóng gói trong lớp TCP/IP và truyền qua mạng nội bộ LAN hoặc cả qua mạng internet  Public mà không cần quan tâm đến các thiết bị chuyên biệt như Fiber Channel, chỉ cần cấu hình đúng Gigabit ethernet và iSCSI.

iSCSI sử dụng không gian nhớ ảo LUN trên Linux hoặc File and Storage service trên Window, giảm chi phí sử dụng các thiết bị có sẵn như switch, hub, router, ... 

## Các thành phần của iSCSI.
![image19](/images/Screenshot_19.png)
iSCSI bao gồm 2 thành phần chính:
* iSCSI Initiator (iSCSI Initiator Node): là thiết bị Client trong kiến trúc hệ thống lưu trữ qua mạng. iSCSI Initiator sẽ kết nối đến máy chủ iSCSI Target và truyền tải các lệnh SCSI thông qua đường truyền mạng TCP/IP. iSCSI Initiator có thể được khởi chạy từ chương trình phần mềm trên OS hoặc phần cứng thiết bị hỗ trợ iSCSI
* iSCSI Target (iSCSI Target Node): thường là một máy chủ lưu trữ có thể là hệ thống NAS. Từ máu chủ iSCSI Target sẽ tiếp nhận các phản hồi request giử từ máy iSCSI Initiator gửi đến và gửi trả dữ liệu trả về. iSCSI Target quản lý các ổ đĩa iSCSI với các tên gọi LUN(Logical Unit Number) được sử dụng để chia sẻ ổ đĩa lưu trữ iSCSI với phía iSCSI Initiator.

## Hoạt đông của iSCSI 
![image18](/images/Screenshot_18.png)

Máy Client là iSCSI Initiator khởi một request yêu cầu truy xuất dữ liệu đến server là iSCSI Target.

Tiếp đến máy iSCSI sẽ tạo một số lệnh SCSI tương ứng với yêu cầu của client.

Các lệnh SCSI và các thông tin sẽ được đóng gói trong gói tin SCSI Protocol Data Unit(SCSI PDU).

Thông tin PDU được sử dụng cho kết nối giữa target và Initiator với các thông tin nhằm xác định các node, thiết lập session, truyền tải lệnh iSCSI và truyền tải dữ liệu

Sau đó gói tin PDU được đóng gói trong lớp TCP/IP và truyền tải qua mạng Network đên iSCSI Target.

Máy chủ iSCSI nhận gói tin và tiến hành mở gói tin ra kiểm tra iSCSI PDU nhằm trích xuất các thành phần liên quan.

Sau đó lệnh SCSI được đưa vào iSCSI Controller để thực thi, sau khi thực thi xong sẽ trả về iCSI response co máy Initiator và Target.

Tất cả quá trình bắt đầu đến truyền tải trên được gọi là một session.


### Lưu trư được chia sẻ trên Network với iSCSI
Nhiều cách để chia sẻ lưu dữ liệu trên mạng hiện có. Giao thức iSCSI định nghĩa một cách để xem một khối thiết bị từ xa là Ổ đĩa củ máy cục bộ. Một thiết bị từ xa trên Network được gọi là iSCSI Target, một máy Client kết nối với iSCSI Target đượcgọi là iSCSI Initiator.

