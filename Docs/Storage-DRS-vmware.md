# Storage DRS VMware Distributed Resource Scheduler
là một tính năng của VMware tối ưu hóa hiệu suất và tài nguyên của cụm vSphere của bạn. Lưu trữ DRS đã được giới thiệu trong vSphere một số bản phát hành trước đây và nó vẫn là một tính năng chính của vSphere 7.

* Cấu hình Storage cluster - cụm lưu trữ với Storage DRS (SDRS) trong vSphere 7 cho phép bạn cân bằng virtual machine disk files (VMDK) giữa các datastores trong datastore cluster.

Tương tự như DRS truyền thống, nơi các máy ảo được đặt ban đầu trên máy chủ khỏe mạnh nhất, vị trí ban đầu là thủ công với SDRS. Sau khi VM được đặt vào một kho dữ liệu, chức năng SDRS sẽ theo dõi các kho dữ liệu đó và đảm bảo rằng không có kho nào trong số chúng được lấp đầy hoàn toàn.

Nếu việc sử dụng kho dữ liệu vượt quá ngưỡng được xác định trước, DRS sẽ đưa ra khuyến nghị chuyển một số VMDK ra khỏi kho dữ liệu này và đặt chúng vào một kho dữ liệu có đủ dung lượng trống.

SDRS cũng theo dõi độ trễ I / O và kiểm tra những gì đã xảy ra trong 24 giờ qua. Có thể đã có một kho dữ liệu với một số I/O nặng trong 24 giờ qua, điều đó có thể có nghĩa là hệ thống sẽ không chuyển VMDK vào đó.

SDRS cho phép bạn đặt một kho dữ liệu vào chế độ bảo trì, cho phép bạn di tản VMDK của mình sang một kho dữ liệu khác để cho phép ngừng hoạt động.

Bạn có thể sử dụng kho dữ liệu dựa trên VMFS hoặc NFS, nhưng bạn không thể kết hợp VMFS với NFS trong cùng một cụm SDRS. Trong trường hợp này, chỉ cần tạo các cụm SDRS riêng biệt.

Nếu bạn có một số mảng lưu trữ hỗ trợ tăng tốc phần cứng, bạn không nên trộn chúng với các mảng khác không có. Như một thực tiễn tốt, cụm kho dữ liệu phải được duy trì đồng nhất.

::))
- Đặt máy ảo ban đầu trên kho dữ liệu với mức sử dụng không gian thấp nhất
- Cân bằng tải dựa trên công suất sử dụng
- Cân bằng tải dựa trên tải I / O

## Các tính năng cốt lõi Storage DRS
* **Resource aggregation**: nhóm nhiều DS vào một nhóm
* **Initial placement**: chăm sóc vị trí đĩa cho các hoạt động như Tạo máy ảo, thêm đĩa, sao chép và định vị lại.
* **Load balancing based on Space and IO**: Storage DRS cân bằng động sự mất cân bằng của cụm Storage DRS dựa trên bộ ngưỡng Space và IO. Ngưỡng space mặc định cho mỗi kho dữ liệu là % 80-90 và ngưỡng độ trễ IO mặc định là 5-15-20-25ms.
* **Datastore maintenance mode**: khi quản trị viên muốn thực hiện các hoạt động bảo trì trên storage. Tương tự như chế độ bảo trì máy chủ, Storage DRS sẽ lưu trữ vMotion tất cả các tệp máy ảo.
* **Inter/Intra VM Affinity rules**: các quy tắc về mối quan hệ / chống quan hệ giữa các máy ảo hoặc VMDK.