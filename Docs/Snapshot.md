# Snapshot là gì?
* Ghi lại trạng thái và dữ liệu của máy ảo tại thời điểm cụ thể khi Snapshot. Snapshot máy ảo là một bản sao chính xác của máy ảo và có thể được sử dụng để di chuyển máy ảo hoặc tạo nhiều phiên bản của cùng một máy ảo. Nó cũng có thể được sử dụng để khôi phục máy ảo về trạng thái cũ mà Snapshot chụp.

Snapshot không phải là một giải pháp tốt dùng để backup.
## Snapshot máy ảo là gì?
Snapshot máy ảo chỉ là một hình ảnh về trạng thái và dữ liệu của máy ảo, được chụp và lưu trữ tại một thời điểm nhất định. Các trạng thái nguồn của máy ảo có thể như sau: đang chạy, tắt nguồn, không xác định, bị treo, bị hủy hoặc tạm dừng, và đang hoạt động hoặc bị ngắt kết nối. Dữ liệu của máy ảo bao gồm tất cả các tệp từ đĩa, trong bộ nhớ và trên các thiết bị lưu trữ được hỗ trợ khác.

Snapshot máy ảo không có bất kỳ tác động nào đến chính máy ảo. Tuy nhiên, nếu bạn đang làm việc trong một môi trường mà bạn cần phải quay lại nhiều lần về trạng thái cụ thể của máy ảo, thì Snapshot máy ảo có thể cho phép bạn làm như vậy mà không cần phải tạo nhiều máy ảo. Ví dụ: bạn có thể sử dụng Snapshot máy ảo làm điểm khôi phục an toàn để thực hiện nâng cấp hoặc thực hiện thay đổi trong cấu hình và cài đặt máy ảo hiện có. Nếu có sự cố, bạn có thể hoàn nguyên về Snapshot VM đã chụp một cách dễ dàng. Nó cũng có thể hữu ích trong môi trường phát triển và thử nghiệm, nơi bạn cần một số máy ảo có cấu hình tương tự cho mục đích thử nghiệm. Hoặc, bạn có thể đang thực hiện và thử nghiệm lặp đi lặp lại một số thay đổi mã và cần có điểm khôi phục an toàn.

## What Are the Components of a Snapshot File - các thành phần?

bao gồm tất cả các tệp được lưu trữ trên thiết bị lưu trữ của máy ảo. Snapshot sẽ tạo các tệp có phần mở rộng .vmdk, -delta.vmdk, .vmsd và .vmsn, được lưu trữ cùng với tệp cơ sở VM. Các tệp delta được lưu trữ bằng tệp VMDK cơ sở, tệp này được lưu trữ ở chế độ chỉ đọc để duy trì trạng thái của nó. Và các tệp VMSD và VMSN được lưu trữ trong thư mục VM.

## What Are the Limitations of VMware Snapshots- Hạn chế của Vmware Snapshots?
Có thể ảnh hưởng đến hiệu suất của máy ảo, vì chúng sử dụng cơ sở hạ tầng và tài nguyên giống như máy ảo mẹ. Có một số hạn chế khác cần lưu ý khi chụp Snapshot VMware :
* Không hỗ trợ chụp nhanh VMware của đĩa thô, đĩa chế độ vật lý ánh xạ thiết bị thô (RDM) và hệ điều hành khách có trình khởi tạo Giao diện Hệ thống Máy tính Nhỏ Internet (iSCSI) không được hỗ trợ.
* Không hỗ trợ Snapshot của máy ảo được bật nguồn hoặc bị treo với các đĩa độc lập. Máy ảo phải được tắt trước khi chụp nhanh.
* Không hỗ trợ chụp nhanh các máy ảo được định cấu hình để chia sẻ bus hoặc hỗ trợ thiết bị I/O PCI vSphere Direct Path.
* Snapshot không được khuyến khích sử dụng làm phương tiện sao lưu và phục hồi vì tiêu thụ dung lượng đĩa lớn và ảnh hưởng đến hiệu suất máy ảo.
* Snapshot các máy ảo với ổ cứng lớn hơn 2 TB có thể mất quá nhiều thời gian.

## Snapshot Files
VMDK là Disk Image Files - Virtual Machine Disk File, dưới định dạng N/A được phát triển bởi VMware. Virtual Disk lưu trữ nội dung của một máy ảo VMware trên ổ cứng vật lý; có thể được truy cập như một ổ cưng vật lý với phần mềm VMware;

Bao gồm các tệp được lưu trữ trên thiết bị lưu trữ được hỗ trợ. Thao tác Snapshot sẽ tạo các tệp .vmdk , -delta.vmdk , .vmsd và .vmsn . Theo mặc định, đĩa đầu tiên và tất cả các đĩa delta được lưu trữ với tệp .vmdk cơ sở. Các tệp .vmsd và .vmsn được lưu trữ trong thư mục máy ảo.

**Delta disk files**- Tệp .vmdk
mà hệ điều hành-OS có thể ghi vào. Đĩa delta đại diện cho sự khác biệt giữa trạng thái hiện tại của đĩa ảo và trạng thái tồn tại tại thời điểm mà Snapshot trước đó được thực hiện. Khi bạn tạo Snapshot, trạng thái của đĩa ảo được giữ nguyên, operating system-OS ngừng ghi vào đây và một delta hoặc đĩa con được tạo.</br>
Một delta disk có hai tệp. Một là tệp bộ mô tả nhỏ chứa thông tin về Virtual disk, chẳng hạn như hình học và thông tin mối quan hệ cha-con. Cái còn lại là tệp tương ứng chứa dữ liệu raw.

Các tệp tạo nên đĩa delta được gọi là child disks hoặc redo log -nhật ký làm lại.

**Flat file**

Tệp -flat.vmdk là một trong hai tệp bao gồm base disk. Flat disk chứa dữ liệu raw cho base disk. Tệp này không xuất hiện dưới dạng tệp riêng biệt trong Datastore Browser.

**Database file**

Tệp .vmsd chứa thông tin Snapshot của máy ảo và là nguồn thông tin chính cho Snapshot Manage. Tệp này chứa các mục nhập dòng, xác định mối quan hệ giữa các ảnh chụp nhanh và giữa các đĩa con cho mỗi ảnh chụp nhanh.

**Memory file**

Tệp .vmsn bao gồm trạng thái hoạt động của máy ảo. Ghi lại trạng thái bộ nhớ của máy ảo cho phép bạn hoàn nguyên về trạng thái máy ảo đã bật. Với nonmemory snapshots, bạn chỉ có thể hoàn nguyên về trạng thái máy ảo đã tắt. Memory snapshots mất nhiều thời gian để tạo hơn nonmemory snapshots. Thời gian máy chủ ESXi cần để ghi bộ nhớ vào đĩa phụ thuộc vào dung lượng bộ nhớ mà máy ảo được cấu hình để sử dụng.
Thao tác Snapshot sẽ tạo các tệp .vmdk , -delta.vmdk , vmsd và vmsn.

