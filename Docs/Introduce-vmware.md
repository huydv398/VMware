# TỔNG QUAN VỀ CÔNG NGHỆ ẢO HÓA - VMWARE VSPHERE

Tổng hợp lý thuyết: https://securityzone.vn/f/ly-thuyet-96/

## VMWare vSphere là gì?

VMWare vSphere là bộ sản phẩm của VMWare, dùng để phục vụ nhu cầu ảo hóa hệ thống.

Các thành phần và chức năng của vSphere:

Với VMware vSphere, người quản trị có rất nhiều các công cụ để sử dụng cho mọi môi trường kiến trúc khác nhau từ vài máy chủ đến hàng ngàn máy chủ bởi sự năng động trong việc điều khiển các nguồn tài nguyên, cũng như tính sẵn sàng cao, tính năng chịu lỗi ưu việt của sản phẩm.

Bộ sản phẩm VMware vSphere bao gồm các sản phẩm với nhiều chức năng cho phép cung cấp đầy đủ các tính năng ảo hóa: 

- VMware ESX and ESXi
- VMware Virtual Symmetric Multi-Processing
- VMware vCenter Server
- VMware vCenter Update Manager
- VMware vSphere Client
- VMware vMotion and Storage vMotion
- VMware Distributed Resource Scheduler
- VMware High Availability
- VMware Fault Tolerance
- VMware Consolidated Backup
- VMware vShield Zones
- VMware vCenter Orchestrator

## 1. VMware ESX and ESXi

VMWare ESXi Server : lớp ảo hóa chính chạy trên nền server vật lý ( hay còn gọi là Hypervisor )
Cốt lõi của bộ sản phẩm vSphere là hypervisor, là lớp ảo hóa nền tảng cho phần còn lại của dòng sản phẩm. Trong vSphere, hypervisor bao gồm hai hình thức khác nhau: VMware ESX và VMware ESXi. Cả hai sản phẩm này đều có thể hỗ trợ cùng một tập hợp các tính năng ảo hóa, và cả hai được cài đặt và chạy trên hệ thống phần cứng. VMware ESX và ESXi chỉ khác nhau về cách thức đóng gói.

VMware ESX bao gồm hai thành phần tương tác với nhau để cung cấp một môi trường ảo hóa năng động và mạnh mẽ: Service Console và VMkernel. Service Console là hệ điều hành được sử dụng để tương tác với VMware ESX và các máy ảo chạy trên máy chủ. Service Console bao gồm các dịch vụ có thể tìm thấy trong các hệ điều hành truyền thống chẳng hạn như tường lửa, Simple Management Protocol (SNMP) hay web server... Tuy nhiên Service Console cũng thiếu nhiều tính năng và lợi ích mà hệ một điều hành truyền thống cung cấp, đây không phải là sự thiếu hụt mà vì chúng đã được loại bỏ để Service Console chỉ bao gồm những dịch vụ cần thiết cho việc hỗ trợ ảo hóa. Thành phần thứ hai là VMkernel, VMkernel là nền tảng thực sự của quá trình ảo hóa. Các VMkernel quản lý truy cập của máy ảo đến các phần cứng vật lý bên dưới bằng cách cung cấp quá trình sử dụng của CPU, quản lý bộ nhớ, và quá trình chuyển đổi dữ liệu ảo.

VMware ESXi là thế hệ kế tiếp của nền tảng ảo hóa VMware. Không giống như VMware ESX, ESXi cài đặt và chạy mà không cần Service Console, điều này làm cho ESXi nhẹ hơn hẳn. ESXi chia sẻ cùng một VMkernel như VMware ESX và hỗ trợ cùng một tập hợp các tính năng ảo.

## 2. VMware Virtual Symmetric Multi-Processing

VMware Virtual Symmetric Multi-Processing (VSMP, hay SMP ảo) cho phép nhà quản trị cơ sở hạ tầng có thể xây dựng các máy ảo với nhiều bộ xử lý ảo. VMware Virtual SMP không phải là một sản phẩm bản quyền cho phép ESX/ESXi được cài đặt trên máy chủ với nhiều bộ xử lý, mà nó là công nghệ có phép sử dụng nhiều bộ xử lý bên trong một máy chủ ảo hóa. Với VMware Virtual SMP, những ứng dụng cần sử dụng nhiều CPU sẽ có thể chạy trên các máy ảo đã đượccấu hình với nhiều CPU ảo. Điều này cho phép các tổ chức ảo hóa nhiều ứng dụng hơn mà không xảy ra xung đột cũng như khả năng không đáp ứng được các yêu cầu về mức độ dịch vụ (SLA).

## 3. VMware vCenter Server

VMware vCenter Server cũng giống như Active Directory. Nó cung cấp một tiện ích quản lý tập trung cho tất cả máy chủ ESX/ESXi và máy ảo tương ứng của nó.

Vmware vCenter Server là một ứng dụng về cơ sở dữ liệu dựa trên nền Window cho phép quản trị viên triển khai, quản lý, giám sát, tự động hoá, và bảo mật cho cơ sở hạ tầng ảo một cách dễ dàng. Các cơ sở dữ liệu back-end được vCenter Server sử dụng để lưu trữ tất cả các dữ liệu về máy chủ và các máy ảo. Bên cạnh việc cấu hình và quản lý hệ thống, vCenter còn có các tính năng như cung cấp và triển khai các máy ảo một cách nhanh chóng, điều khiển việc phân phối tài nguyên tốt hơn. vCenter Server cung cấp các công cụ phục vụ cho các tính năng nâng cao của VMware VMotion, Vmware Distributed Resource Scheduler, VMware High Availability, và VMware Fault Tolerance.

Ngoài VMware VMotion, VMware Distributed Resource Scheduler, VMware High Availability, và VMware Fault Tolerance, việc sử dụng vCenter Server để quản lý máy chủ ESX/ESXi cũng mở ra một số tính năng khác:

- Enhanced VMotion Compatibility (EVC) có chức năng thúc đẩy phần cứng từ Intel và AMD để có được khả năng tương thích CPU tốt hơn giữa các máy chủ trong VMware DRS cluster
- Host Profiles mang lại sự nhất quán hơn cho các quản trị viên trong việc cấu hình máy chủ và để xác định cấu hình bị thiếu hoặc không chính xác
- vNetwork Distributed Switches cung cấp nền tảng cho việc tinh chỉnh hệ thống mạng trên diện rộng và các thiết bị chuyển mạch ảo của bên thứ ba.

vCenter Server đóng vai trò trung tâm trong vSphere. vCenter Server có sẵn trong ba phiên bản:

- vCenter Server Essentials được tích hợp vào phiên bản vSphere Essentials để triển khai cho các doanh nghiệp nhỏ
- vCenter Server Standard cung cấp tất cả các chức năng của Server vCenter, bao gồm dự phòng, quản lý, giám sát, và tự động hóa.
- vCenter Foundation Server giống như vCenter Server Standard nhưng được giới hạn trong quản lý ba máy chủ ESX/ESXi.

## 4. VMware vCenter Update Manager

vCenter Update Manager là một plug-in cho Server vCenter giúp người dùng quản lý máy chủ ESX/ESXi và các máy ảo được cập nhật đầy đủ. vCenter Update Manager cung cấp các chức năng sau đây:
- Quét để xác định hệ thống có tương thích với các bản cập nhật mới nhất không.
- Các quy tắc do người dùng định ra để xác định những hệ thống đã quá hạn.
- Tự động cài đặt các bản vá lỗi cho các máy chủ ESX/ESXi.
- Tích hợp đầy đủ với các tính năng khác như Distributed Resource Scheduler...
- Hỗ trợ vá lỗi cho hệ điều hành Windows và Linux.
- Hỗ trợ bản vá lỗi cho các ứng dụng Windows trong máy ảo.

## 5. VMware vSphere Client

VMware vSphere Client là một ứng dụng trên nền Windows cho phép bạn quản lý các máy chủ ESX / ESXi trực tiếp hoặc thông qua một vCenter Server. Bạn có thể cài đặt vSphere Client bằng trình duyệt với URL của máy chủ ESX/ESXi hoặc vCenter Server và chọn liên kết cài đặt thích hợp. vSphere client là một giao diện đồ họa (GUI) được sử dụng để quản lý tất cả các nhiệm vụ theo từng ngày. Sử dụng máy trạm để kết nối trực tiếp đến một máy chủ ESX / ESXi đòi hỏi bạn phải sử dụng một tài khoản người dùng được lưu trên máy chủ đó, trong khi sử dụng máy trạm để kết nối đến vCenter Server thì yêu cầu bạn phải sử dụng tài khoản Windows trên máy vCenter Server. Hầu như tất cả các công cụ quản lý công việc đều sẵn sàng khi bạn đang kết nối trực tiếp vào một máy chủ ESX/ ESXi cũng như khi bạn đang kết nối với một vCenter Server. Tuy nhiên những khả năng quản lý có sẵn thông qua một vCenter Server thì sẽ nhiều hơn và quan trọng hơn khi kết nối trực tiếp tới một máy chủ ESX /ESXi.

## 6. VMware VMotion và Storage VMotion

VMotion hay còn được gọi là live migration, là một tính năng của ESX / ESXi và vCenter Server cho phép một máy ảo đang chạy có thể được di chuyển từ một máy chủ vật lý này đến một máy chủ vật lý khác mà không cần phải tắt nguồn máy ảo. Sự di chuyển giữa hai máy chủ vật lý xảy ra không có thời gian chết và không làm mất kết nối mạng đến máy ảo. VMotion đáp ứng cho nhu cầu của một tổ chức nhằm duy trì SLA để đảm bảo tính sẵn sàng cho server. Quản trị viên có thể dễ dàng dùng VMotion để loại bỏ tất cả các máy ảo từ một máy chủ ESX /ESXi để thực hiện bảo trì. Sau khi bảo trì hoàn tất và máy chủ được đưa trở lại trực tuyến, VMotion một lần nữa có thể được sử dụng để trả các máy ảo đó về với máy chủ ban đầu. Ngay cả trong các hoạt động bình thường hàng ngày, VMotion có thể được sử dụng khi nhiều máy ảo trên cùng một máy chủ đang cạnh tranh tài nguyên. VMotion có thể giải quyết vấn đề bằng cách cho phép người quản trị di chuyển bất kì máy ảo đang chạy nào đang bị tranh chấp tài nguyên nhưng có nhu cầu sử dụng tài nguyên lớn hơn đến một máy chủ ESX/ESXi khác.

Storage VMotion xây dựng trên ý tưởng và nguyên tắc của Vmotion nhằm làm giảm thời gian chết cùng với chức năng có thể di chuyển kho lưu trữ của máy ảo trong khi nó đang chạy. Tính năng này đảm bảo sẽ không xảy ra việc ngừng các máy ảo khi dữ liệu quá tải hoặc chuyển dữ liệu sang một mạng hệ thống dữ liệu mới (Storage area network) và cung cấp cho quản trị viên một công cụ để tăng tính linh hoạt nhằm đáp ứng những yêu cầu trong công việc.

## 7. VMware Distributed Resource Scheduler

Distributed Resource Scheduler (DRS) là một tính năng nhằm cung cấp một tiện ích giúp tự động phân phối nguồn tài nguyên đến nhiều máy chủ ESX / ESXi được cấu hình trong cùng một cluster. Một ESX / ESXi cluster là một tập hợp tiềm ẩn về sức mạnh CPU và bộ nhớ của tất cả các máy chủ tham gia vào cluster đó. Sau khi hai hoặc nhiều máy chủ đã được gán vào 1 cluster thì chúng sẽ làm việc đồng loạt để cung cấp CPU và bộ nhớ cho các máy ảo được gán trong cluster.
Mục tiêu của DRS có hai phần:

- Khi khởi động, DRS sẽ nỗ lực để đặt từng máy ảo trên máy chủ thích hợp để chạy máy ảo đó tốt nhất.
- Trong khi một máy ảo đang chạy, DRS sẽ tìm cách cung cấp cho máy ảo các tài nguyên phần cứng cần thiết và giảm thiểu số lượng tranh chấp tài nguyên để duy trì hiệu suất tối đa.

DRS không chỉ hoạt động lúc khởi động máy ảo mà còn quản lý vị trí của máy ảo trong khi nó đang chạy.

## 8. VMware High Availability

Trong nhiều trường hợp, tính sẵn sàng cao (HA) hoặc thiếu tính khả dụng cao là lý do chính chống lại sự ảo hóa. Trước khi ảo hóa, sự xuất hiện lỗi của một máy chủ vật lý chỉ ảnh hưởng đến một ứng dụng hoặc công việc. Tuy nhiên sau khi ảo hóa, thì lỗi này sẽ ảnh hưởng đến nhiều ứng dụng hoặc công việc đang chạy trên máy chủ tại thời điểm đó.

Chính vì vậy Vmware High Availability (HA) được biết đến như là giải pháp cho vấn đề này. VMware HA cung cấp một quá trình tự động cho việc khởi động lại máy ảo đang chạy trên một máy chủ ESX/ ESXi tại thời điểm mà server bị lỗi. VMware HA có tính năng không giống như DRS, không sử dụng công nghệ Vmotion như một phương tiện chuyển đổi server đến một máy chủ khác.

## 9. VMware Fault Tolerance

Vmware Fault Tolerance (FT) là tính năng dành cho những người có yêu cầu về tính sẵn sàng cao hơn so với VMware HA có thể cung cấp. VMware HA bảo vệ khỏi việc phát sinh lỗi của máy chủ vật lý bằng cách khởi động lại máy ảo vào lúc xảy ra lỗi, tuy nhiên việc làm này sẽ phát sinh thời gian ngừng hoạt động (downtime) khoảng 3 phút.

Đối với VMware FT, thời gian ngừng hoạt động sẽ được loại bỏ, bằng cách sử dụng công nghệ vLockstep. VMware FT duy trì một bản sao của máy ảo phụ và nó được lưu trữ trong lockstep của máy ảo chính nằm trên một máy chủ vật lý riêng biệt. Tất cả mọi thứ xảy ra trên máy ảo chính đều xảy ra trên máy ảo phụ, do đó khi máy ảo chính chạy trên máy chủ vật lý bị lỗi thì các máy ảo thứ cấp có thể ngay lập tức bước vào phiên làm việc mà không mất kết nối. VMware FT cũng sẽ tự động tạo ra máy ảo phụ trên máy chủ khác một khi mà máy chủ vật lý chứa máy ảo thứ cấp đang chạy đó bị lỗi. Trong trường hợp những máy chủ đang cùng chạy máy ảo chính và máy ảo phụ bị lỗi thì VMware HA sẽ khởi động lại máy ảo chính trên một máy chủ đã sẵn sàng, và VMware FT cũng sẽ tự động tạo ra một máy ảo phụ mới. Chính vì vậy mà máy ảo chính luôn được bảo đảm sẵn sàng.

VMware FT có thể làm việc cùng với Vmotion nhưng nó không thể làm việc với DRS, vì vậy phải vô hiệu hóa DRS trên các máy ảo được bảo vệ với VMware FT.

## 10. VMware Consolidated Backup

Một trong những khía cạnh quan trọng nhất đối với hệ thống mạng không chỉ là một cơ sở hạ tầng được ảo hóa mà còn cần một chiến lược dự phòng vững chắc. VMware Consolidated Backup (VCB) là một bộ công cụ và giao diện cung cấp chức năng sao lưu Lan-free và Lan-based cho các giải pháp backup. VCB đưa ra một tiến trình sao lưu với một máy chủ vật lý hay máy ảo chuyên dụng và cung cấp hướng tích hợp với các giải pháp sao lưu khác như Backup Exec, TSM, NetBackup, … VCB sử dụng lợi thế của chức năng snapshot (lưu lại tình trạng và dữ liệu của máy ảo) trong ESX / ESXi để gắn kết thông tin snapshot vào hệ thống tập tin của máy chủ VCB. Sau khi các file trong máy ảo tương ứng được gắn kết, toàn bộ những máy ảo hoặc các tập tin cá nhân có thể được sao lưu bằng cách sử dụng công cụ sao lưu khác. VCB có những lệnh tích hợp với một số các giải pháp sao lưu khác để cung cấp một phương tiện tự động hoá quá trình sao lưu.

## 11. VMware vShield Zones

VMware vSphere cung cấp một số tính năng kết nối mạng ảo, và vShield Zones xây dựng dựa trên chức năng mạng ảo của vSphere để thêm vào chức năng tường lửa ảo. vShield Zone cho phép người quản trị vSphere quan sát và quản lý mạng lưới giao thông xảy ra trên các thiết bị chuyển mạch ảo. Chúng ta có thể áp dụng các chính sách an ninh mạng trên toàn bộ các nhóm máy, và phải đảm bảo rằng các chính sách này được duy trì đúng mặc dù các máy ảo có thể di chuyển từ máy chủ này sang máy chủ khác thông qua VMotion và DRS.

## 12. VMware vCenter Orchestrator

VMware vCenter Orchestrator là một công cụ tự động hóa quy trình làm việc và được cài đặt một cách tự động đối với các phiên bản vCenter Server. Sử dụng vCenter Orchestrator, các quản trị viên có thể xây dựng một qui trình công việc tự động từ đơn giản cho đến phức tạp.

## 13. vNetwork

Một hệ thống mạng ảo sẽ thực hiện việc kết nối các máy chủ và máy ảo với nhau thông qua các Switch ảo (vSwitch). Tất cả các thông tin mạng trên một máy chủ được truyền tải qua một hoặc nhiều vSwitch. Một vSwitch cung cấp kết nối giữa các máy ảo với nhau ngay cả khi chúng nằm trên cùng một máy chủ hoặc trên nhiều máy chủ khác nhau. Một vSwitch cũng cho phép kết nối đến Service Console của máy chủ ESX, đến Management Network của máy chủ ESXi và thậm chí đến những IP storage.
Trên một vSwitch có các kiểu kết nối sau:

- Service Console port : chỉ dành riêng cho máy chủ ESX.
- VMkernel port : dùng để thực hiện tính năng vMotion, FT, kết nối đến các IP Storage (iSCSI, NAS, NFS) hoặc kết nối đến Management Network của máy chủ ESXi.
- Virtual Machine port group : dùng để kết nối với các máy ảo trên máy chủ ESX (ESXi).
- Uplink port: dùng để kết nối với các NIC thật trên máy chủ ESX (ESXi) cho phép lưu thông mạng giữa trong và ngoài máy chủ.
Một hệ thống mạng ảo hỗ trợ hai loại vSwitch sau:

- vNetwork Standard Switch : là vSwitch được cấu hình trên một máy chủ đơn lẻ. Một vNetwork Standard Switch có các tính năng gần như giống với một Switch vật lý ở Layer 2.
- vNetwork Distributed Switch: bao gồm các thành phần tương tự như vNetwork Standard Switch nhưng nó có tính năng như một vSwitch chung cho toàn bộ hệ thống các máy chủ có kết nối với nhau. Điều này cho phép các máy ảo duy trì được tính nhất quán trong việc cấu hình mạng ngay cả khi phải di chuyển qua nhiều máy chủ.

## 14. vStorage

Các loại công nghệ storage được hỗ trợ trong VMware vSphere gồm các loại sau:

- Direct Attached Storage (DAS): là hệ thống lưu trữ mà trên đó các HDD, thiết bị nhớ được gắn trực tiếp vào máy chủ qua các cổng SATA, SAS, SCSI...
- Storage Area Network (SAN): là một mạng được thiết kế để kết nối các máy chủ tới hệ thống lưu trữ dữ liệu gồm nhiề thiết bị lưu trữ như một khối chung duy nhất. Công nghệ kết nối thường được dùng là Fibre Channel (cáp quang).
- iSCSI SAN : iSCSI là Internet SCSI (Small Computer System Interface ), là một chuẩn cho phép truyền tải các lệnh SCSI qua mạng IP hiện có bằng cách sử dụng giao thức TCP/IP. Không như Fiber Channel (FC) SAN là phải xây dựng hạ tầng mạng mới, iSCSI SAN tận dụng hạ tầng LAN sẵn có (các thiết bị mạng, Swich... trên nền IP).
- Network Attached Storage (NAS) là công nghệ lưu trữ mà theo đó các thiết bị lưu trữ được gắn trực tiếp vào mạng IP và sử dụng các giao thức chia sẻ file (NFS, CIFS) để cho phép các thiết bị trên mạng IP truy cập vào.
Một kho dữ liệu (datastore) là một nơi lưu trữ vật lý được dùng để lưu trữ các file của máy ảo cũng như các loại dữ liệu khác. Tùy vào dạng storage mà ta sử dụng, datastore có thể chia thành hai định dạng sau:

- VMware vStorage VMFS: là một hệ thống file cluster, nó cho phép nhiều máy chủ vật lý có thể truy cập vào cùng một thiết bị lưu trữ tại cùng một thời điểm. VMFS được sử dụng với các thiết bị DAS, FC SAN, iSCSI SAN. Với VMFS ta có thể mở rộng phân vùng một cách dễ dàng và kích thước của một block là 8MB cùng với các subblock cho phép lưu trữ file từ lớn đến nhỏ một cách hiệu quả. VMFS cũng giúp thực hiện các công việc liên quan đến ảo hóa như: di chuyển máy ảo (vMotion, SvMotion), tự khởi động lại máy ảo khi máy chủ bị lỗi (HA, FT)...
- Network File System (NFS) : có tính năng tương tự như VMFS nhưng NFS datastore được sử dụng để kết nối các máy chủ với các thiết bị NAS thông qua giao thức chia sẽ file NFS
Nhằm mục đích tối ưu hóa việc sử dụng các thiết bị lưu trữ, VMware đã đưa vào vStorage chức năng Thin Provisioning. Thin Provisioning giúp nén dung lượng của máy ảo xuống bằng với dung lượng mà máy ảo sử dụng. Ta có thể chuyển đổi giữa định dạng thin và thick bằng Storage vMotion.

## Nguồn
[DungDB-https://github.com/lukabobo/VMware](https://github.com/lukabobo/VMware)

http://www.idz.vn/2017/04/tong-quan-ve-cong-nghe-ao-hoa-vmware.html
