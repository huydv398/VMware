# @a
## Vấn đề an ninh!
Cải thiện tính bảo mật của tài nguyên vSphere mà theo tôi, chủ yếu là ESXi và vCenter Server.

Trong bài viết này, tìm hiểu những khái niệm cơ bản nhất và có thể bị bỏ qua nhiều nhất mà người ta có thể triển khai liên quan đến việc bảo mật vCenter Server. Đây được coi là nguyên tắc của đặc quyền ít nhất(principle of least privilege). Nói một cách đơn giản, người dùng chỉ nên được cấp những đặc quyền và quyền hạn cho phép họ thực hiện công việc mà không bị cản trở. Khái niệm này rất được khuyến khích và phù hợp với môi trường bảo mật được chia sẻ và sử dụng bởi người dùng từ các phòng ban khác nhau với các chức năng và vai trò khác nhau.
## Bảo mật máy chủ vCenter. Những thứ khác bạn nên biết
Tất cả các hệ thống đang chạy ở cấp bản vá mới nhất.

Triển khai vCenter Server cho Windows, đòi hỏi hệ điều hành Microsoft phải tăng tốc về mặt cài đặt các bản cập nhật mới nhất bằng Windows Server Update Services hoặc bất kỳ phần mềm quản lý bản vá nào khác. Đây là điều nhất định phải có. Bạn chỉ đơn giản là không thể bỏ qua nó.

Bạn cũng nên đảm bảo tắt tất cả các dịch vụ dư thừa và chặn các cổng mạng không sử dụng bằng cách sử dụng tường lửa hoặc cách khác, bất kể máy chủ có kết nối Internet hay không.

Một khía cạnh quan trọng khác cần xem xét là tác biệt lưu lượng mạng. Đây là một yêu cầu bắt buộc đối với sản phẩm, hoặc ít nhất là một yêu cầu rất được khuyến khích, không chỉ từ góc độ bảo mật - như trong việc ngăn chặn nghe trộm - mà còn để ngăn chặn hiệu suất bị ảnh hưởng xấu; ví dụ như tắc nghẽn lưu lượng mạng. VLAN là một cách tuyệt vời để tách riêng lưu lượng truy cập nhưng bạn cũng có thể sử dụng các mạng vật lý hoàn toàn độc lập để cô lập các dịch vụ storage, vMotion hoặc management services của mình.

## Single Sign-On (SSO)
vCenter Single Sign-On (SSO) là một thành phần xử lý quản lý danh tính cho quản trị viên và ứng dụng tương tác với nền tảng vSphere. SSO dựa trên công nghệ quản lý danh tính được xây dựng bởi RSA và được thiết kế riêng cho việc triển khai Cơ sở hạ tầng đám mây VMware(VMware Cloud Infrastructure). SSO hoạt động bằng cách liên kết xác thực và truy vấn dữ liệu chính với Active Directory (AD) hoặc bất kỳ phiên bản dựa trên LDAP nào khác. SSO cũng có miền hoặc cửa hàng người dùng nội bộ của riêng nó - vsphere.local trừ khi bạn đặt tên khác trong khi cài đặt - vì vậy bạn không nhất thiết phải có Active Directory hoặc cơ chế xác thực dựa trên LDAP khác để chạy SSO. Không giống như các phiên bản xác thực dựa trên LDAP hoặc Windows, dữ liệu chính được lưu trữ trong cửa hàng nội bộ 

Hình 1: Quản lý người dùng và Group trong Local
![image1](/images/Screenshot_1.png)

Hình 2: Các nguồn định danh đã được vcenter xác minh định danh.
![image2](/images/Screenshot_2.png)

- vSphere.local - miền cục bộ vCenter Server bao gồm các nhóm và người dùng được xác định trước như administrator@vsphere.local .
- Localos - đây là tên NetBIOS của hộp Windows chạy vCenter Server. Điều này ngụ ý rằng người dùng và nhóm được tạo trong Windows có thể được sử dụng để chỉ định quyền trên tài nguyên vSphere.
- sun.local - đây là miền Active Directory (AD), người dùng và nhóm từ đó có thể được sử dụng để gán quyền trên tài nguyên vSphere. Bạn nên biết rằng SSO cung cấp hai phương pháp tương tác AD riêng biệt. 
	- Đầu tiên và phổ biến nhất là nơi máy chủ Windows, trên đó máy chủ vCenter đã được cài đặt trên thực tế là một thành viên của miền AD. 
	- Phương pháp thứ hai đơn giản chuyển tiếp xác thực bằng LDAP mà không cần Máy chủ vCenter được thiết lập như một thành viên của miền AD. Điều này đạt được bằng cách hoàn thành cấu hình cho tùy chọn “Active Directory như một LDAP Server” trong khi thêm nguồn nhận dạng SSO như được giải thích trong phần sắp tới.

Thêm nguồn nhận dạng SSO mới. Xem lại bài hướng dẫn trước.
## Mô hình quyền máy chủ vCenter
Mô hình ủy quyền quyền vCenter Server được hiển thị bên dưới , phác thảo quy trình mà các quyền được thiết lập trên một đối tượng vSphere có thể là một thư mục, máy ảo hoặc cách khác. Các bước bạn cần làm theo là;

* Tạo hoặc sao chép một Role hiện có.
* Thêm hoặc sửa đổi các privileges-đặc quyền được chỉ định cho Role-vai trò.
Cấp quyền cho một đối tượng bằng cách chỉ định người dùng hoặc nhóm mà một role-vai trò cụ thể đã được chỉ định.
![image3](/images/Screenshot_3.png)
* Permissions - Quyền: quyền cho mỗi đối tượng trên vCenter
    * Mỗi đối tượng trong cấu trúc phân cấp đối tượng vCenter Server có các quyền liên quan. Mỗi quyền chỉ định cho một nhóm hoặc người dùng mà nhóm hoặc người dùng đó có đặc quyền trên đối tượng.
* Global Permissions - Quyền toàn cầu: được áp dụng cho một đối tượng root bao gồm các giải pháp, ví dụ: cả vCenter Server và vCenter Orchestrator. Sử dụng quyền toàn cầu để cấp cho người dùng hoặc nhóm đặc quyền cho tất cả các đối tượng trong tất cả các cấu trúc phân cấp đối tượng. Mỗi giải pháp có một đối tượng root trong hệ thống phân cấp đối tượng của riêng nó. Đối tượng root toàn cục hoạt động như một đối tượng mẹ cho mỗi đối tượng giải pháp. Bạn có thể chỉ định quyền toàn cầu cho người dùng hoặc nhóm và quyết định vai trò cho từng người dùng hoặc nhóm. Vai trò xác định tập hợp các đặc quyền. Bạn có thể chỉ định một vai trò xác định trước hoặc tạo các vai trò tùy chỉnh.
* Object: một thực thể mà các hành động được thực hiện như Datacenter, folder, resource pools, cluster, host, VM.
* Privileges: đặc quyền – kiểm soát truy cập chi tiết vào tài nguyên, các đặc quyền nhóm thành các vai trò được ánh xạ tới user hoặc group
* Users and groups: Trên hệ thống máy chủ vCenter, chỉ có thể chỉ định đặc quyền cho user hoặc nhóm user đã được xác thực thông qua đăng nhập một lần (SSO) hoặc từ các nguồn nhận dạng bên ngoài nà vCenter đang sử dụng như Microsoft Active Directory.
* Roles: Vai trò là tập hợp các đặc quyền. Vai trò cho phép chỉ định quyền trên một đối tượng dựa trên một nhóm tác vụ điển hình mà người dùng thực hiện. Các vai trò mặc định, chẳng hạn như Administrator, được xác định trước trên vCenter và không thể thay đổi. Các vai trò khác, chẳng hạn như Resource Pool Administrator, là các vai trò mẫu được xác định trước, có thể tạo các vai trò tùy chỉnh từ đầu hoặc bằng cách sao chép và sửa đổi các vai trò mẫu.

Quyền thường phải được định nghĩa trên cả đối tượng nguồn và đối tượng đích. Ví dụ: nếu di chuyển một máy ảo, cần có các đặc quyền trên máy ảo đó, nhưng cũng có các đặc quyền trên trung tâm dữ liệu đích.
## Tạo các group user có các đặc quyền
1. Group User quản lý vm
1. Group User chỉ xem log
1. Group User giám sát
1. Group User mạng
1. Group User lưu trữ
![image4](/images/Screenshot_4.png)
## Tạo các Role tương ứng
### 1. Đối với người dùng quản trị vm
* Datastore:
    * Browse datastore
* Global:
    * Cancel task
* Scheduled task:
    * Create tasks
    * Modify task
    * Remove task
    * Run task
* Virtual machine:
    * Change Configuration
    * Acquire disk lease
    * Add existing disk
    * Add new disk
    * Add or remove device
    * Advanced configuration
    * Change CPU count
    * Change Memory
    * Change Settings
    * Change resource
    * Modify device settings
    * Remove disk
    * Rename
    * Reset guest information
    * Upgrade virtual machine * compatibility
* Edit Inventory:
    * Create from existing
    * Create new
* Interaction:
    * Answer question
    * Configure CD media
    * Configure floppy media
    * Connect devices
    * Console interaction
    * Guest operating system * management by VIX API
    * Install VMware Tools
    * Power off
    * Power on
    * Reset
    * Suspend
* Provisioning:
    * Clone virtual machine
    * Create template from virtual * machine
* Snapshot management:
    * Create snapshot
    * Remove snapshot
    * Rename snapshot
    * Revert to snapshot
Dựa trên Role Virtual machine power user (sample)

### 2.Đối với user có quyền để hoạt động backup:
* Cryptographic operations
    * Add disk
    * Direct Access
    * Encrypt
    * Encrypt new
    * Migrate
* dvPort Group
    * Create
    * Delete
    * Modify
* Datastore
    * Allocate space
    * Browse datastore
    * Configure datastore
    * Low-level file operations
    * Remove file
* Extension
    * Register extension
    * Unregister extension
* Folder
    * Create folder
    * Delete folder
* Global
    * Disable methods
    * Enable methods
    * Licenses
    * Log event
    * Manage custom attributes
    * Set custom attribute
    * Settings
* Host
    * Configuration
    * Advanced settings
    * Maintenance
    * Network configuration
    * Query patch
    * Storage partition configuration
* vSphere Tagging
    * Assign or Unassign vSphere Tag
* Network
    * Assign network
    * Configure
* Resource
    * Assign virtual machine to resource pool
    * Create resource pool
    * Migrate powered off virtual machine
    * Migrate powered on virtual machine
    * Remove resource pool
* Datastore cluster
    * Configure a datastore cluster
* Profile-driven storage
    * Profile-driven storage update
    * Profile-driven storage view
    * vApp
    * Add virtual machine
    * Assign resource pool
    * Unregister
* Virtual Machine
    * Change Configuration
        * Acquire disk lease
        * Add existing disk
        * Add new disk
        * Add or remove device
        * Advanced configuration
        * Change Settings
        * Change resource
        * Configure RAW device*
        * Extend virtual disk
        * Modify device settings
        * Remove disk
        * Rename
        * Set annotation
        * Toggle disk change tracking
    * Edit Inventory
        * Create
        * Register
        * Remove
        * Unregister
    * Guest operations
        * Guest operation modifications
        * Guest operation program execution
        * Guest operation queries
    * Interaction
        * Configure CD media
        * Configure floppy media
        * Console interaction
        * Connect devices
        * Guest operating system management by VIX API
        * Power Off
        * Power On
        * Suspend
    * Provisioning
        * Alow disk access
        * Allow read-only disk access
        * Allow virtual machine download
        * Allow virtual machine files upload
        * Mark as template
        * Mark as virtual machine
    * Snapshot Management
        * Create snapshot
        * Remove snapshot
        * Rename snapshot
        * Revert to snapshot   

### 3. User có quyền giám sát tương ứng với Role Read-onle
### 4. User chỉ có quyền Collect Log
* Global
    * Diagnostics
    * Licenses
    * Settings
* Host
    * Configuration
        * Change SNMP settings
        * Hyperthreading
        * Memory configuration
        * Network configuration
        * Power
        * Security profile and firewall
        * Storage partition configuration
* Session
    * View and stop sessions
* System
    * Anonymous *
    * Read *
    * View *

Tham khảo : [Splunk- Create vCenter user accounts](https://docs.splunk.com/Documentation/VMW/4.0.2/Installation/CreatevCenterserviceaccounts)


### 5.User chỉ có quyền quản lí Storage

* Datastore
    * Allocate space
    * Browse datastore
    * Configure datastore
    * Low level file operations
    * Move datastore
    * Remove datastore
    * Remove file
    * Rename datastore
    * Update virtual machine files
    * Update virtual machine metadata
* Datastore cluster
    * Configure a datastore cluster   
### 6.User chỉ có quyền quản lí Network

* dvPort group
    * Create
    * Delete
    * IPFIX operation
    * Modify
    * Policy operation
    * Scope operation
* Distributed switch
    * Create
    * Delete
    * Host operation
    * IPFIX operation
    * Modify
    * Move
    * Network I/O control operation
    * Policy operation
    * Port configuration operation
    * Port setting operation
    * VSPAN operation
* Datacenter
    * Network protocol profile * configuration
    * Network
    * Assign network
    * Configure
    * Move network
    * Remove
* NSX
    * Manage NSX configuration
    * Modify NSX configuration
    * Read NSX configuration
Để tạo Role vào **Menu** > **Administration** > **Access Control** > **Roles**
## Tạo Role trên vCenter

![image6](/images/Screenshot_6.png)
![image7](/images/Screenshot_7.png)
## Tạo user trên local
![image14](/images/Screenshot_14.png)
## Tạo group user trên vCenter
Vào  **Menu** > **Administration** > **Single Sign On** > **User and Group**
![image5](/images/Screenshot_5.png)

![image8](/images/Screenshot_8.png)

![image10](/images/Screenshot_10.png)
## Gắn quyền của Group, user cho đối tượng
Chọn đối tượng cần gắn quyền.
* Object: một thực thể mà các hành động được thực hiện như Datacenter, folder, resource pools, cluster, host, VM.
Sau đó chọn tab **Permission**:
![image11](/images/Screenshot_11.png)

![image13](/images/Screenshot_13.png)

Nếu không chọn **Propagate to children** 

* Nếu bạn chỉ định global permission và không chọn Propagate to children , người dùng hoặc nhóm được liên kết với quyền này không có quyền truy cập đếncác đối tượng trong hệ thống phân cấp. Họ chỉ có quyền truy cập đến một số global permission chẳng hạn như tạo roles- vai trò.
