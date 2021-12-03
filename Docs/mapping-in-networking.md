# Mapping?

## Network Mapping có nghĩa là gì?
Network mapping là một quá trình được sử dụng để khám phá và trực quan hóa kết nối mạng vật lý và ảo thông qua một nhóm các tác vụ có liên quan với nhau để tạo thuận lợi cho việc tạo bản đồ mạng, bao gồm biểu đồ luồng, sơ đồ mạng, phát hiện cấu trúc liên kết và kiểm kê thiết bị. Nó hướng tới việc tạo ra các tài liệu và công cụ hỗ trợ trực quan có thể được sử dụng cho nhiều mục đích, đặc biệt là bảo trì mạng.

Sử dụng phương pháp thăm dò tích cực để thu thập dữ liệu mạng bằng cách gửi các gói thăm dò chuyển từ nút này sang nút khác, các gói này sẽ trả về thông tin cho hệ thống ánh xạ cùng với địa chỉ IP và các chi tiết kỹ thuật khác.

## Logical unit number (LUN)
A logical unit number (LUN) là gì?
* Số nhận dạng duy nhất để chỉ định một riêng biệt hoặc tập hợp các thiết bị lưu trữ vật lý hoặc ảo thực hiện các lệnh input/output (I/O) với máy tính chủ, như được định nghĩa bởi Small System Computer Interface (SCSI) Tiêu chuẩn.
* SCSI là một kết nối I/O được triển khai rộng rãi có thể tạo điều kiện trao đổi dữ liệu giữa các máy chủ và thiết bị lưu trữ thông qua các giao thức truyền tải. Ví dụ về các giao thức truyền tải bao gồm Internet SCSI và Fibre Channel. Bộ khởi tạo SCSI trong  máy chủ  bắt nguồn chuỗi lệnh I/O, sau đó được truyền đến thiết bị lưu trữ người nhận hoặc điểm cuối đích. A logical unit là một thực thể trong mục tiêu SCSI đáp ứng lệnh SCSI I/O.
* LUN được sử dụng để xác định các tập con dữ liệu trong đĩa để các thiết bị tính toán sử dụng chúng có thể thực thi các hoạt động.

## Cách thức hoạt động của LUN:
logical unit
Logical unit
* Thiết lập LUN khác nhau tùy theo hệ thống. A logical unit được chỉ định khi máy chủ quét thiết bị SCSI và phát hiện ra logical unit. LUN xác định logical unit cụ thể cho bộ khởi tạo SCSI khi được kết hợp với thông tin như target port identifier.
* Logical unit có thể là một phần của ổ đĩa lưu trữ, toàn bộ ổ đĩa lưu trữ hoặc tất cả các bộ phận của một số ổ đĩa lưu trữ như ổ đĩa cứng, ổ đĩa trạng thái rắn, trong một hoặc nhiều hệ thống lưu trữ. Một LUN có thể tham chiếu đến toàn bộ tập hợp RAID , một ổ đĩa hoặc  phân vùng , hoặc nhiều ổ đĩa lưu trữ hoặc phân vùng. Trong mọi trường hợp, logical unit được coi như thể nó là một thiết bị duy nhất và được xác định bằng số đơn vị lôgic. Giới hạn dung lượng của một LUN thay đổi tùy theo hệ thống.
* LUN là trung tâm của việc quản lý  mảng lưu trữ khối   trong mạng vùng lưu trữ - storage-area network(SAN). Sử dụng LUN có thể đơn giản hóa việc quản lý tài nguyên lưu trữ vì các đặc quyền truy cập và kiểm soát có thể được chỉ định thông qua các mã định danh logic.

## Các loại LUN
* Mirrored LUN: LUN chịu lỗi với các bản sao giống hệt nhau trên hai ổ đĩa vật lý để dự phòng và sao lưu dữ liệu  .
* **Concatenated LUN** - Nối: củng cố nhiều LUN thành một đơn vị logic đơn hoặc khối lượng .
* **Striped LUN**:  Ghi dữ liệu trên nhiều ổ đĩa vật lý, có khả năng nâng cao hiệu suất bằng cách phân phối các yêu cầu I / O trên các ổ đĩa.
* **Striped LUN with parity**:  Truyền dữ liệu và   thông tin chẵn lẻ trên ba hoặc nhiều ổ đĩa vật lý. Nếu một ổ đĩa vật lý bị lỗi, dữ liệu có thể được tạo lại từ thông tin trên các ổ đĩa còn lại. Tính toán parity có thể có tác động đến hiệu suất ghi.

LUN uses
* hoạt động như một số nhận dạng để chỉ định một thiết bị lưu trữ; tuy nhiên, trường hợp sử dụng có thể khác nhau đối với mỗi loại LUN.
* Các LUN có thể được sử dụng để zoning and masking(phân vùng và tạo mặt nạ) trong SAN hoặc chúng có thể được ảo hóa để ánh xạ nhiều LUN vật lý.
* Mặc dù thuật ngữ LUN chỉ là số nhận dạng của đơn vị lôgic, nhưng người ta thường nghe nó được sử dụng như viết tắt để chỉ đơn vị lôgic.

**LUN zoning and masking**
* Storage area networks(SAN) kiểm soát quyền truy cập của máy chủ vào các LUN để thực thi tính toàn vẹn và bảo mật của dữ liệu. Mặt nạ LUN và  phân vùng dựa trên công tắc quản lý các tài nguyên SAN có thể truy cập được đối với các máy chủ đính kèm.
* LUN zoning cung cấp các đường dẫn riêng biệt cho I/O thông qua kết cấu FC SAN giữa các cổng cuối để đảm bảo hành vi xác định. Máy chủ bị giới hạn trong khu vực mà nó được chỉ định. Phân vùng LUN thường được thiết lập ở lớp chuyển đổi. Nó có thể giúp cải thiện bảo mật và loại bỏ các điểm nóng trong mạng.

LUNS và ảo hóa
* LUN tạo thành một dạng  ảo hóa  theo nghĩa là nó trừu tượng hóa các thiết bị phần cứng đằng sau nó bằng một phương pháp nhận dạng và giao tiếp SCSI tiêu chuẩn. Đối tượng lưu trữ được đại diện bởi LUN có thể được cung cấp , nén hoặc loại bỏ trùng lặp miễn là biểu diễn đối với máy chủ lưu trữ không thay đổi. Một LUN có thể được di chuyển trong và giữa các thiết bị lưu trữ, cũng như được sao chép, nhân bản, chụp nhanh và phân cấp.
* Một  LUN ảo  có thể được tạo để ánh xạ tới nhiều LUN vật lý cũng như để ảo hóa dung lượng, có thể được tạo ra vượt quá không gian vật lý có sẵn. Các LUN ảo được tạo vượt quá dung lượng vật lý hiện có được sử dụng để giúp tối ưu hóa việc sử dụng bộ nhớ, vì bộ nhớ vật lý không được cấp phát cho đến khi dữ liệu được ghi. Điều này đôi khi được gọi là LUN mỏng.
* Một LUN ảo có thể được thiết lập ở cấp hệ điều hành máy chủ (OS),  hypervisor  hoặc bộ điều khiển lưu trữ. Vì  máy ảo (VM) không nhìn thấy LUN vật lý trên hệ thống lưu trữ nên không cần phân vùng LUN.
* Một ứng dụng phần mềm có thể đưa ra một LUN cho một máy ảo chạy trên hệ điều hành khách. Công nghệ độc quyền, chẳng hạn như Khối lượng ảo của VMware  , có thể cung cấp lớp ảo hóa và thiết bị lưu trữ để hỗ trợ chúng.

Quản lý LUNs
* LUN có thể được quản lý thông qua một chương trình phần mềm chỉ định đường dẫn giữa các LUN và máy chủ. Các LUN có thể được quản lý bằng cách kiểm soát tính khả dụng của LUN, tăng kích thước LUN và bằng cách xóa hoặc bảo mật LUN. Các phương pháp quản lý tốt nhất sẽ khác nhau tùy thuộc vào môi trường.
* Người dùng có thể tăng kích thước LUN; không có giới hạn về dung lượng mà một LUN có thể chiếm. Tuy nhiên, người dùng cần lưu ý không phân bổ nhiều không gian lưu trữ hơn mức cần thiết.
* Xóa thường đề cập đến việc ghi đè lên không gian đã sử dụng trong một ổ đĩa, không phải là ngắt kết nối hoặc tách LUN. Quản trị viên phải là người dùng duy nhất được phép xóa LUN.
* Khoanh vùng và tạo mặt nạ là những cách khác để nói rằng một LUN được bảo mật.


Link tham khảo: [LUN ?](https://searchstorage.techtarget.com/definition/logical-unit-number)
Link tham khảo: [LUN & Datastore?](https://communities.vmware.com/t5/vSphere-Storage-Discussions/what-is-LUN-and-datastore/td-p/2607572)
https://communities.vmware.com/t5/vSphere-Storage-Discussions/what-is-LUN-and-datastore/td-p/2607572