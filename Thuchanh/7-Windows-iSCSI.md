# Cấu hình Windows iSCSI
Một máy chủ đích cho máy chủ VMware vCenter  hoặc ESXi.

Windows iSCSI là gì?
* Internet Small Computer Systems Interface. iSCSI là một giao thức lớp vận chuyển hoạt động trên giao thức TCP (Transport Control Protocol). Nó cho phép truyền dữ liệu SCSI ở block-level giữa iSCSI initiator và storage target trên các mạng TCP / IP. iSCSI hỗ trợ mã hóa các gói mạng và giải mã khi đến đích.

* Cơ bản iSCSI cung cấp Storage qua IP

Mô hình cơ bản:
![image](/images/Screenshot_61.png)

IPPlanning:
![image16](/images/Screenshot_16.png)

# Tạo iSCSI
Cấu hình: 
![image17](/images/Screenshot_17.png)

Cấu hình địa chỉ IP như sau:

![image20](/images/Screenshot_20.png)

Add role:

![image21](/images/Screenshot_21.png)

![image22](/images/Screenshot_22.png)

![image23](/images/Screenshot_23.png)

![image24](/images/Screenshot_24.png)

Chọn iSCSI Target Server,
![image25](/images/Screenshot_25.png)

![image26](/images/Screenshot_26.png)

![image27](/images/Screenshot_27.png)

![image28](/images/Screenshot_28.png)


Tạo iSCSI virtual disk
![image29](/images/Screenshot_29.png)

Chọn phân vùng E: làm virtual disk 
![image30](/images/Screenshot_30.png)

Đánh dấu disk này là OS Image - Datastore

![image31](/images/Screenshot_31.png)

![image32](/images/Screenshot_32.png)

![image33](/images/Screenshot_33.png)

![image34](/images/Screenshot_34.png)

![image35](/images/Screenshot_35.png)
![image36](/images/Screenshot_36.png)
![image37](/images/Screenshot_37.png)
![image38](/images/Screenshot_38.png)
![image39](/images/Screenshot_39.png)
![image40](/images/Screenshot_40.png)
## Connect iSCSI Storage ESXi 7
### Cấu hình Networking
Đăng nhập ESXi-1
![image41](/images/Screenshot_41.png)

Kiểm tra dải mạng làm storage:

![image43](/images/Screenshot_43.png)

Thực hiện: **Networking** -> **Virtual switches** -> **Add standard virtual switch**

![image42](/images/Screenshot_42.png)

![image44](/images/Screenshot_44.png)

Chọn tab VMkernel NICs và nhấp vào Add VMKernel NIC

![image45](/images/Screenshot_45.png)

Thực hiện cấu hình:
![image](/images/Screenshot_46.png)

Đặt địa chỉ IP theo dải Storage.

![image](/images/Screenshot_48.png)

Theo IP Planning:
![image](/images/Screenshot_47.png)

Kết quả:

![image](/images/Screenshot_49.png)

**Thực hiện tương tự trên ESXi-2**.

### Cấu hình Storage
Chọn **Storage** -> **Adapter** -> **Software iSCSI**.

![image](/images/Screenshot_50.png)

Chọn **Enable iSCSI**

![image](/images/Screenshot_51.png)

Phần **Dynamic Target**, Chọn **Add Dynamic target** -> Nhập địa chỉ IP của server iSCSI storage, chọn **Save configuration** để hoàn thành.
![image](/images/Screenshot_52.png)

Kiểm tra xem đã nhận Dynamic Target chưa:

![image56](/images/Screenshot_56.png)

Kiểm tra Device:

![image57](/images/Screenshot_57.png)

Chuyển sang tab **Datastores**, chọn **New datastore**
![image](/images/Screenshot_53.png)

![image](/images/Screenshot_54.png)

![image](/images/Screenshot_55.png)

Sử dụng Full Partition:
![image](/images/Screenshot_58.png)

![image](/images/Screenshot_59.png)

Kết quả:

![image](/images/Screenshot_60.png)

## Các loại khi tạo một datastores
![image](/images/Screenshot_62.png)
* Create new VMFS datastore: Tạo một VMFS mới trên thiết bị Disk đang được kết nối đến local(có thể là Disk đang cắm tại local, Hoặc iSCSI virtual Disk đã được kết nối đến local ESXi)
* Add an extent to existing VMFS datastore: thêm kích thước của một datastore hiện có bằng cách thêm một phạm vi trên DISK khác
* Expand an existing VMFS datastore extent: Tăng kích thước của datastore hiện có
* Mount NFS datastore: tạo một datastore mới bằng cách gắn một ổ đĩa từ NFS