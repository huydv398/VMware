# VMware vSphere Distributed Switch

VMware vSphere Distributed Switch (VDS) cung cấp một giao diện tập trung mà từ đó bạn có thể định cấu hình, giám sát và quản trị chuyển mạch truy cập máy ảo cho toàn bộ trung tâm dữ liệu. VDS cung cấp:
* Cấu hình mạng máy ảo đơn giản hóa 
* Nâng cao khả năng giám sát và khắc phục sự cố mạng 
* Hỗ trợ các tính năng mạng VMware vSphere nâng cao



Một trong những trụ cột cốt lõi của cơ sở hạ tầng VMware vSphere là virtual networking - virtual networking cơ bản được cung cấp bởi virtual switch hoặc vSwitch. Nếu không có vSwitch, sẽ không thể giao tiếp giữa các lớp khác nhau của ngăn xếp ảo, bao gồm cả lớp mạng vật lý.

vSphere Distributed Switch (vDS) có nhiều ưu điểm hơn so với vSphere Standard Switch (VSS). Hướng dẫn đầy đủ về công tắc vDS này sẽ xem xét các khái niệm cơ bản của vDS, bao gồm tạo, cấu hình, yêu cầu, port VMkernel, di chuyển và các chủ đề khác.

### Những thách thức của vSphere Standard Switch (VSS)
Để hiểu vSphere Distributed Switch là gì, trước tiên chúng ta cần hiểu thêm một chút về vSphere Standard Switch. vSphere Standard Switch cung cấp kết nối mạng mặc định cho các máy chủ và máy ảo. Nó có thể bridge traffic nội bộ giữa các máy ảo chạy trên máy chủ và liên kết chúng với các mạng bên ngoài.

Chức năng này tương tự như một bộ switch Ethernet vật lý. Virtual machine network adapters và NIC vật lý trên máy chủ ESXi sử dụng các port logic của Switch vì mỗi bộ adapter sử dụng một port. Mỗi port logic trên VSS là một thành viên của một port group duy nhất. Một trong những điểm khác biệt chính giữa vSphere Standard Switch (VSS) và vSphere Distributed Switch là nơi management resides - quản lý cư trú. VSS là một công tắc ảo vSphere lấy máy chủ làm trung tâm . Nó được tạo theo mặc định khi bạn cài đặt VMware ESXi lần đầu tiên . Khi bạn gán địa chỉ IP quản lý cho máy chủ ESXi, đây là port VMkernel đầu tiên được tạo trên vSwitch0 mặc định của máy chủ ESXi.

Virtual switches chứa hai yếu tố để xem xét: management plane và data plane. VSS bao gồm cả management plane và data plane. Vì lý do này, bạn quản lý từng VSS như một thực thể độc lập, duy nhất từ ​​quan điểm của máy chủ ESXi.

![image](/images/Screenshot_222.png)

Vì VSS chứa cả management plane và data plane, mọi VLANS và các port group liên quan với các VLAN đó phải được quản lý và duy trì trên từng máy chủ ESXi cụ thể. Ngay cả các máy chủ ESXi khác trong cùng một cụm vSphere cũng không biết về các công tắc VSS và port group được định cấu hình trên các máy chủ ESXi khác. Nếu bạn có 100 port group VSS được tạo trên một máy chủ ESXi cụ thể, bạn phải tạo các port group VSS tương tự này trên tất cả các máy chủ ESXi khác để truy cập các port group cụ thể đó.

Điều cần thiết trong một cụm vSphere là có các port group VSS giống nhau và các ID VLAN được định cấu hình với cùng tên và chi tiết chính xác. Bất kỳ máy ảo nào được di chuyển giữa các máy chủ ESXi trong một cụm nhất định phải có cùng các virtual networking trên máy chủ ESXi đích, nếu không những máy này sẽ có nguy cơ mất kết nối mạng.

vSphere Standard Switch hoạt động tốt trong môi trường vSphere nhỏ và thậm chí lớn. Tuy nhiên, thách thức với VSS nằm ở hình thức quản lý trên quy mô lớn . Ngoài ra, các giải pháp VMware cụ thể yêu cầu vSphere Distributed Switch (vDS), NSX-T là một nếu không sử dụng N-VDS.

Khi bạn nghĩ về việc tạo các vSphere Standard Switches và port groups giống nhau trên một vài máy chủ, điều này không quá khó. Tuy nhiên, điều gì sẽ xảy ra nếu bạn có hàng trăm hoặc thậm chí hàng nghìn máy chủ cần cùng một vSwitch? Điều gì sẽ xảy ra nếu bạn cần thực hiện một thay đổi đơn giản trên vSwitch và cần sự thay đổi này được phản ánh trên tất cả các máy chủ? Trong các tình huống quản lý này, đây là nơi các rủi ro về quản lý của vSphere Standard Switches bắt đầu hiển thị và nơi vSphere Distributed Switch bắt đầu tỏa sáng. Không cần quảng cáo thêm, chúng ta hãy giới thiệu vSphere Distributed Switch.

## vSphere Distributed Switch (vDS) là gì?
Khi nói đến những điều cơ bản về cách vSphere Distributed (vDS) vượt qua lưu lượng, nó rất giống với VSS. Tuy nhiên, về mặt quản lý và tính năng, nó là một cấu trúc virtual networking mạnh hơn nhiều. vSphere Distributed Switch phân tách management plane và data plane. Tất cả việc quản lý vSphere Distributed Switch nằm trên Máy chủ vCenter trong khi data plane chuyển lưu lượng truy cập vẫn cục bộ cho máy chủ ESXi.

Dưới đây là mô hình cơ bản của vSphere Distributted Switch 

![image](/images/Screenshot_221.png)

Sự tách biệt giữa các management plane và dữ liệu có nghĩa là trong khi tất cả các nhiệm vụ quản lý được thực hiện ở cấp Máy chủ vCenter, không có lưu lượng truy cập vSphere Distributed Switch nào đi qua Máy chủ vCenter. Bằng cách này, không có gián đoạn mạng nào với máy chủ của bạn bằng cách sử dụng vSphere Distributed Switch nếu Máy chủ vCenter gặp sự cố. Thành phần data plane được định cấu hình trên máy chủ ESXi được gọi là proxy switch máy chủ .

Để phân tách hiệu quả các management plane và dữ liệu của vSphere Distributed Switch, VMware đã giới thiệu hai tính năng mới trong kiến ​​trúc của vDS. Đây là uplink port group và distributed port group . Hãy xem chúng hoạt động như thế nào với vSphere Distributed Switch.

## Uplink port group vSphere Distributed Switch
Uplink port group vDS, còn được gọi là port group dvuplink, được tạo lần đầu tiên khi bạn tạo vSphere Distributed Switch mà nó được liên kết với nó. Như đã đề cập, nó là một sự trừu tượng cho phép bản chất phân tán của vDS. Uplink port group vSphere Distributed Switch là một **template** của các loại **cho phép** định **cấu hình** các **physical uplinks** trên các máy chủ ESXi và các policies - chính sách xác định cấu hình **failover and load-balancing** - chuyển đổi dự phòng và cân bằng tải. Mỗi **physical uplinks** trên máy chủ ESXi  **maps** - ánh xạ tới **ID uplink port group** . Bạn **configure policies** -cấu hình các chính sách trên **uplink port group**. Proxy switch máy chủ nằm trên máy chủ ESXi nhận cấu hình được xác định trong chính sách chuyển đổi dự phòng và cân bằng tải.

## Port group vSphere Distributed Switch
Các port group vSphere Distributed Switch là cấu trúc thiết yếu trong vDS. Chúng **cung cấp kết nối mạng** tới các **máy ảo** và cũng cung cấp **đường dẫn** cho **VMkernel traffic**. Bạn gắn nhãn port group vDS bằng nhãn mạng giống như bạn dán nhãn port group VSS. Chúng phải là duy nhất cho mỗi trung tâm dữ liệu vSphere. Các port group vDS cũng rất quan trọng vì đây là nơi các chính sách được áp dụng ảnh hưởng đến việc tạo nhóm, chuyển đổi dự phòng, cân bằng tải, cấu hình VLAN, định hình lưu lượng và bảo mật.

Bạn áp dụng cấu hình cho port group vSphere Distributed Switch ở cấp Máy chủ vCenter. Sau đó, các cài đặt sẽ truyền xuống proxy switch máy chủ ESXi. Bằng cách này, các máy ảo có thể chia sẻ cùng một cấu hình mạng bằng cách kết nối các máy ảo với cùng một port group vSphere Distributed Switch.

## Các ưu điểm khác của vSphere Distributed Switch (vDS)
Ngoài khả năng quản lý virtual networking của bạn mạnh mẽ hơn trên toàn cảnh vSphere, vDS còn cung cấp nhiều ưu điểm và tính năng khác so với vSphere Standard Switch. Chúng bao gồm những điều sau:

* **Cấu hình mạng máy ảo được đơn giản hóa** - Với vDS, bạn có thể đơn giản hóa đáng kể cấu hình mạng VM trên cơ sở hạ tầng vSphere của mình. VDS cho phép bạn cung cấp quyền kiểm soát tập trung mạng máy ảo của mình, bao gồm kiểm soát tập trung đối với việc đặt tên port group, cấu hình VLAN, bảo mật và nhiều cài đặt khác.
*  **Link Aggregation Control Protocol** - Giao thức kiểm soát tổng hợp liên kết (LACP): Hãy nhớ rằng cách duy nhất được hỗ trợ để chạy LACP trong môi trường vSphere của bạn với virtual networking vSphere là sử dụng vSphere Distributed Switch.
* **Khả năng kiểm tra tình trạng mạng** - vDS cung cấp nhiều khả năng kiểm tra tình trạng mạng, bao gồm xác minh vSphere để kiểm tra mạng vật lý.
* **Giám sát và khắc phục sự cố mạng nâng cao** - Với vDS, bạn có quyền truy cập vào RSPAN ERSPAN, IPFIX Netflow phiên bản 10, SNMPv3, khôi phục và khôi phục cấu hình mạng
* **Templates sao lưu và khôi phục** cấu hình mạng máy ảo
* **Netdump** để gỡ lỗi máy chủ lưu trữ dựa trên mạng
* **Các tính năng mạng nâng cao** - Chúng bao gồm Network I/O Control (NIOC), SR-IOV và bộ lọc BPDU, trong số những tính năng khác.
* **Hỗ trợ VLAN riêng (PVLAN)** - vSphere Distributed Switch cho phép sử dụng VLAN riêng, cung cấp nhiều tùy chọn bảo mật hơn để phân đoạn lưu lượng
* **Định hình lưu lượng hai hướng** - Bạn có thể định hình chính sách lưu lượng dựa trên các định nghĩa port group DV (băng thông trung bình, băng thông đỉnh và kích thước cụm)

## Yêu cầu của vSphere Distributed Switch (vDS)
Có một số yêu cầu cần xem xét với vSphere Distributed Switch. Yêu cầu đầu tiên là một tuyên bố về điều hiển nhiên. vSphere Distributed Switch là một cấu trúc vCenter Server, vì vậy bạn cần phải chạy vCenter Server. Bạn sẽ không thể sử dụng vSphere Distributed Switch nếu bạn đang chạy các máy chủ độc lập không được kết nối với Máy chủ vCenter.

Không giống như vSphere Standard Switch được tìm thấy với tất cả các loại giấy phép vSphere và ngay cả với ESXi miễn phí, vSphere Distributed Switch chỉ khả dụng với giấy phép vSphere Enterprise Plus . Tuy nhiên, nhiều người có thể không nhận ra rằng họ nhận được vSphere Distributed Switch như một phần của giấy phép vSAN . VDS cung cấp nhiều lợi thế về hiệu suất trong môi trường vSAN do sử dụng Network I/O Control (NIOC).

## Tính năng vDS bị thiếu trong VSS
Tuy nhiên, những tính năng vDS nào bị thiếu trong vSphere Standard Switch (VSS)? Bao gồm các:

* **Centralized management** - Quản lý tập trung: Như đã mô tả, vDS được quản lý từ Máy chủ vCenter chứ không phải từ máy chủ ESXi.
* **Port mirroring** - Phản chiếu port: Khả năng phản chiếu lưu lượng mạng từ một virtual switch port sang virtual switch port khác. Port mirroring thường được sử dụng để khắc phục sự cố hoặc thậm chí **ghi lại lưu lượng truy cập** cho các mục đích bảo mật hoặc pháp y.
* **Network I/O Control** là một tính năng rất mạnh mẽ giúp giảm thiểu tranh chấp mạng và ưu tiên lưu lượng nếu mạng trở nên bão hòa.
* **Các tính năng mạng nâng cao** - Các tính năng được hỗ trợ như Link Aggregation Control Protocol (LACP),  Private VLANs (PVLANs), NetFlow, and Link Layer Discovery Protocol (LLDP) không được tìm thấy trên vSphere Standard Switch
* vNetwork Switch API - Điều này cung cấp giao diện cho các nhà cung cấp bên thứ ba để mở rộng chức năng vSphere Distributed Switch tích hợp sẵn. Tuy nhiên, VMware đã kết thúc hỗ trợ chương trình vSwitch của bên thứ ba . Các thiết bị chuyển mạch vS của bên thứ ba phổ biến như Cisco 1000V không còn được hỗ trợ trong Bản cập nhật 1 vSphere 6.5 trước đây.
* **Ability to backup and restore vSwitches** - Khả năng sao lưu và khôi phục vSwitches: Cấu hình vDS có thể được sao lưu trong vSphere Client và được khôi phục. Không có chức năng tích hợp nào tương đương cho vSphere Standard Switch.
* **Virtual Machine port blocking** - Chặn cổng Máy ảo: Có thể có trường hợp bạn muốn chặn có chọn lọc các port gửi hoặc nhận dữ liệu bằng cách sử dụng chính sách chặn port vSphere Distributed Switch.
* **Hỗ trợ NSX-T** - vSphere Distributed Switch là vSwitch duy nhất được hỗ trợ để sử dụng với NSX-T. Tạo một vSphere Distributed Switch (vDS)
* **vSphere với sự hỗ trợ của Tanzu** - Mới với vSphere 7 Update1 và vSphere với Tanzu, khách hàng có thể sử dụng mạng vSphere gốc với vDS để hỗ trợ các cụm Tanzu Kubernetes Grid của họ. Mới với vSphere với Tanzu, VMware đã loại bỏ yêu cầu phải có NSX-T trong môi trường. Bây giờ, bạn có thể sử dụng vSphere Distributed Switch để kết nối với giao diện giao diện người dùng, khối lượng công việc và quản lý của mình.

[Link tham khảo](https://www.altaro.com/vmware/vsphere-distributed-switch-guide/)


