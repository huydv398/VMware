## Bước 1: Tạo New Switch Port Group
Tạo Portgroup vMotion:

![image](/images/Screenshot_305.png)

## Bước 2: Thêm Uplink và Đổi tên Uplink

Chọn  **vDS** -> **Settings** -> **Edit Settings**

![image](/images/Screenshot_306.png)

Thay đổi số Up link 

![image](/images/Screenshot_307.png)

Đổi tên cho Uplink

![image](/images/Screenshot_308.png)

## Bước 3: Assign Uplink to vDS Port Group

Thực hiện chọn **Networking** -> Chọn **Distributed Switch** -> **Configure** -> **Topology** 

Uplink vMotion 1-2 và vDS Port Group vMotion:

![image](/images/Screenshot_304.png)


![image](/images/Screenshot_309.png)

Chỉ chọn 2 Uplink của đường dẫn kết nối, đã được đặt tên cho dễ hiểu

![image](/images/Screenshot_310.png)

Sau khi chuyển các đường kết nối không cần thiết kết quả được như sau:

![image](/images/Screenshot_311.png)

Kết quả: 2 Uplink đường dịnh hướng đến vMotion

![image](/images/Screenshot_312.png)

## Bước 4: Tạo VMkernel Network Adapter lên tất cả các Host ESXi và kết nối tới vmnic
Vào từng host mà bạn muốn tạo vMotion.
Chọn ADD Network: 

![image](/images/Screenshot_313.png)

Chọn **VMkernel Network Adapter**

![image](/images/Screenshot_314.png)

CHọn một mạng đã có sẵn

![image](/images/Screenshot_315.png)

Gắn vào port group vMotion

![image](/images/Screenshot_316.png)


![image](/images/Screenshot_317.png)

Đặt địa chỉ IP:

![image](/images/Screenshot_318.png)


![image](/images/Screenshot_319.png)


![image](/images/Screenshot_320.png)

Add uplink, Đường kết nối vật lý tới máy ESXi 

![image](/images/Screenshot_321.png)

Thêm vmnic gắn vào vMotion 

Gắn vào vMotion-1

![image](/images/Screenshot_322.png)


![image](/images/Screenshot_323.png)

Gắn vào vMotion-2

![image](/images/Screenshot_324.png)


![image](/images/Screenshot_325.png)

sau khi add xong

![image](/images/Screenshot_326.png)


![image](/images/Screenshot_327.png)

![image](/images/Screenshot_328.png)

Hoàn thành Tạo vMotion máy thứ nhất. Tiếp theo cài đặt các máy ESXi còn lại theo các bước tương tự

Sau khi tôi thêm ESXi thứ 2 thì sẽ được kết quả như sau:

vMotion 1 và vMotion-2 phải có 2 Uplink( 3 Uplink nếu có 3 Host ESXi) 

## Bước 5 Thực hiện vMotion
![image](/images/Screenshot_332.png)


![image](/images/Screenshot_331.png)




![image](/images/Screenshot_329.png)


![image](/images/Screenshot_330.png)

* **Change compute resource only** : Di chuyển xang host hoạc Cluster khác
* Change storage only: Di chuyển storage tới datastore hoặc datastore cluster.
* **Change both compute resource and storage**: Thay đổi cả tài nguyên compute và Storage. Di chuyển các máy ảo đến một máy chủ hoặc cụm máy chủ cụ thể và bộ nhớ của chúng đến một kho dữ liệu hoặc cụm kho dữ liệu cụ thể.

