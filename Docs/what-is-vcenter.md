# GIỚI THIỆU VỀ VMWARE VCENTER

VMware vCenter Server cũng gần tương tự như Active Directory. Nó cung cấp một tiện ích quản lý tập trung cho tất cả máy chủ ESX/ESXi và máy ảo tương ứng của nó.

- Hỗ trợ đến 1000 host/1 vCenter

- Hỗ trợ lên đến 10.000 máy ảo/1 vCenter

![Imgur](https://i.imgur.com/yf9YWtE.png)
​
Vmware vCenter Server là một ứng dụng về cơ sở dữ liệu cho phép triển khai, quản lý, giám sát, tự động hoá, và bảo mật cho cơ sở hạ tầng ảo một cách dễ dàng.

Các cơ sở dữ liệu back-end được vCenter Server sử dụng để lưu trữ tất cả các dữ liệu về máy chủ và các máy ảo.

![Imgur](https://i.imgur.com/xdkQFYV.png)

vCenter còn có các tính năng cung cấp và triển khai các máy ảo một cách nhanh chóng, điều khiển việc phân phối tài nguyên tốt hơn.

vCenter Server cung cấp các công cụ phục vụ cho các tính năng nâng cao của

- VMware VMotion
- Vmware Distributed Resource Schedule
- VMware High Availability
- VMware Fault Tolerance.

Việc sử dụng vCenter Server để quản lý máy chủ ESX/ESXi cũng mở ra một số tính năng khác:

- Enhanced VMotion Compatibility (EVC) có chức năng thúc đẩy phần cứng từ Intel và AMD để có được khả năng tương thích CPU tốt hơn giữa các máy chủ trong VMware DRS cluster

- Host Profiles mang lại sự nhất quán hơn cho các quản trị viên trong việc cấu hình máy chủ và để xác định cấu hình bị thiếu hoặc không chính xác

- vNetwork Distributed Switches cung cấp nền tảng cho việc tinh chỉnh hệ thống mạng trên diện rộng và các thiết bị chuyển mạch ảo của bên thứ ba.

vCenter Server đóng vai trò trung tâm trong vSphere. 

vCenter Server có sẵn trong ba phiên bản:

- vCenter Server Essentials được tích hợp vào phiên bản vSphere Essentials để triển khai cho các doanh nghiệp nhỏ
- vCenter Server Standard cung cấp tất cả các chức năng của Server vCenter, bao gồm dự phòng, quản lý, giám sát, và tự động hóa.
- vCenter Foundation Server giống như vCenter Server Standard nhưng được giới hạn trong quản lý ba máy chủ ESX/ESXi.

## 1. vCenter Server

vCenter Server là 1 ứng dụng và framework dùng để quản lý tập trung. Nói cho dễ hiểu, Vcenter dùng để quản lý tập trung các node ESXi. 

​Các tính năng mà enterprise yêu cầu trong vCenter như:

- Vmware vMotion (dùng để transfer VM)
- Vmware High Availability (HA)
- Vmware Distributed Resource Scheduler (DRS)
- Vmware Update Manager (UM)

## 2. vCenter Server Physical hay Virtual?

vCenter Server có thể là cài đặt trên 1 Physical hoặc như 1 máy ảo

Physical

- Bạn cần có 1 máy chuyên dụng để cài đặt vCenter trên 1 Physical server

- Khi cài đặt vCenter trên Physical thì không có rủi ro khi vSphere ngừng hoạt động

Virtual

- Virtual có thể được hỗ trợ với các VM khác nhau như: windows, linux
- Virtual không lãng phí tài nguyên physical server để chạy vCenter như cài vCenter trên physical
- Khi cài vCenter như 1 máy ảo bạn có thể cho vCenter tham gia HA và vMotion
- Có rủi ro của vSphere ngừng hoạt động

## 3. vCenter Server pre-installation

- vCenter nên là 1 thành phần của Domain
- Ban nên đặt IP tĩnh và Hostname cho máy cài vCenter
- Tạo Back-end database
- Xác định lựa chọn License triển khai
- Chỉnh chính xác thời gian và ngày tháng…
- Server phải được đăng ký trong DNS và đảm bảo ràng nó phân giải được từ tất cả các ESXi host
- vCenter không thể là 1 Domain Controler
- Account để thực hiện cài đặt nên là:
    - Member của administrator group
    - Như 1 thành phần của hệ điều hành
    - Log on như 1 service

## 4. HW and SW yêu cầu

Hardware

- CPU: 2 CPU 64-bit hoặc 1 CPU 64-bit dual-core (2GHx hoặc cao hơn)
- Memory: 4GB hoặc cao hơn nếu bạn cài Database chạy trên vCenter Server
- Storage: tối thiểu 4GB và nhiều hơn nếu DB được cài đặt trên vCenter
- Networking: 1 card 1GB hoặc nhiều hơn

Software

- Windows Server 2003 bản STD, END hoặc Datacenter 64-bit SP2
- Windows Server 2003 bản STD, END hoặc Datacenter 64-bit SP1
- Windows Server 2008 bản STD, END hoặc Datacenter 64-bit SP2
- Windows Server 2008 R2 bản STD, END hoặc Datacenter 64-bit
- Microsoft .NET 3.5 Sp1 Framework
- Microsoft Windows Installer 4.5 (nếu bạn sử dụng SQL 2008R2 Express)

## 5. Database

Các database được hỗ trợ:

- IBM DB2 9.5 và 9.7
- Microsoft SQL server 2008 R2 Express
- Microsoft SQL server 2005
- Microsoft SQL server 2008 và 2008 R2
- Oracle 10g R2 và 11g

Các Database mặc định

- Microsoft SQL server 2008 R2 Express
- Có thể sử dụng được trong môi trường nhỏ khoảng 5 hosts và 50 VMs

## 6. Port yêu cầu

- 80/443 cho truy cập web
- 902 cho heartbeat, quản lý ESXi và truy cập Console của VM
- 8080/8443 cho dịch vụ web và HTTPs
- 389 cho LDAP, bạn có thể thay đổi port này trong khoảng 1025 đến 65535
- 636 cho Linked Mode trong vCenter, bạn có thể thay đổi port này trong khoảng 1025 đến 65535.
- 60099 web serice là port thông báo các dịch vụ thay đổi
- 10443 vCenter Inventory service HTTPS
- 10109 vCenter Inventory Service management
- 10111 vCenter Inventory Service linked mode communications

## 7. vCenter Server Appliance là gì ?

- vCSA là 1 chọn lựa mới trong việc triển khai vCenter Server trên vSphere 5. Theo cách truyền thống thì chúng ta phải cài windows server lên sau đó mới cài đặt vCenter lên Windows server.
- vCSA là 1 máy ảo chạy trên nền Linux, được tối ưu để chạy vCenter.
- Bạn không cần có kiến thức về linux mà vẫn có thể triển khai được vCSA. Nó đơn giản chỉ là VM được cài đặt sẵn và việc cấu hình nó bạn có thể sử dụng trình duyệt web để cấu hình khá đơn giản.
- Bạn không cần thực hiện cài đặt vCSA. Nó giống như 1 VM đã được cài đặt sẵn trước bạn chỉ cần download về và import vào VMware
- Bạn chỉ tốn chi phí mua license vCenter. Không như triển khai vCenter truyền thống trên Windows là bạn phải mua license windows sau đó mua thêm license vCenter

## 8. Ưu điểm và khuyết điểm của vCSA

Ưu điểm:

- Hỗ trợ tất cả các tính năng củ vCenter truyền thống như: DRS, SDRS, HA, Host profiles, dvSwitch…
- Không cần mua license windows
- Triển khai đơn giản và nhanh chóng

Nhược điểm:

- Không hỗ trợ SQL và database bên ngoài vì nó tích hợp sẵn database của Posgres
- Chức năng link mode trên vCenter Server không hoạt động
- Tính năng heartbeat trên vCenter Server không hoạt động
- Single-sing on không sử dụng được thông tin cá nhân phiên làm việc của windows
- vSphere Storage Appliance (VSA) thì không tương thích được

## 9. Deploying the cCenter Server 5 Appliance (vCSA)

- Để triển khi vCSA bạn cần cài đặt sẵn ESXi server và vSphere Client
- Bạn có thể download file cài đặt vCSA tại trang chủ của vmware
    - File có định dạng .OVF
    - Yêu cầu HDD còn trống tối thiểu 4GB
- Trên vSphere client bạn chọn Deply OVF để thực hiện cài đặt vCenter APP
- Username và password mặc định của vCSA: root|vmware
- Bạn có thể cấu hình network và timezone bằng console hoặc bằng trình duyệt web
- Bạn nên cấu hình IP tĩnh và DNS cho vCSA

## 10.  Giao tiếp giữa Vcenter và ESXi

![Imgur](https://i.imgur.com/iuY1UAt.png)

Khi Vsphere Client kết nối trực tiếp đến ESXi thì trên ESXi có công cụ Hostd (agent) chuyên nhận các lệnh từ Vsphere Client

Khi dùng Vcenter và Vsphere Web Client thì phải thông qua agent có tên là vpxa  rồi mới qua hostd
Vpxa sẽ được khởi động trên ESXi khi nó được them vào trong Vcenter inventory.

Hostd biết tất cả những máy ảo có trên ESXi, tình trạng máy ảo, các vùng lưu trữ trên ESXi. Hầu hết các lệnh từ Vcenter Server đều qua hostd như: tạo, migrate, bật, ắt máy ảo v.v…

Khi ta log on Vcenter bằng Vshere Web Client thì Vcenter sẽ gửi các lệnh đến vpxa và lúc đó Vcenter database sẽ được update, còn nếu dùng Vsphere Client thì đương nhiên sẽ đi trực tiếp đến Hostd và Vcenter database sẽ không được cập nhập

ESXi nhận lệnh qua port 902 TCP/UDP

Vcenter  nhận lệnh qua 443 và 9443

## Nguồn

https://securityzone.vn/t/chapter-2-gioi-thieu-va-tim-hieu-vmware-vcenter-server.528/

https://www.mrtech.vn/2016/03/vmware-vsphere-co-ban-ve-vmware-vcenter.html