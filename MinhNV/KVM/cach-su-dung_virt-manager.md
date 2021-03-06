# Cách sử dụng Virsh Virtual Machine
## Cài đăt : apt-get install virt-manager
- Ở đây chúng ta dùng putty để ssh vào máy server đã cài đặt sẵn KVM. Vì vậy: 
 - Máy client cần cài đặt putty ( cần có X11) 
 - Máy server cần được cài đặt KVM  và Linux Brigde
## Bước 1: Kích hoạt X11 trong putty ở máy client
- Cấu hình putty để sử dụng được xming
- Khởi động putty và cấu hình để kích hoạt X11 phía client theo hình các thao tác: Connection => SSH => X11

<img src="http://i.imgur.com/cN29L7z.png">

## Bước 2: Thực hiện nhập IP của máy chủ Ubuntu vào mục Secssion trong putty 

**Login với tài khoản root (lưu ý, tính năng cho phép ssh bằng root phải được kích hoạt trước) và gõ lệnh dưới để khởi động công cụ quản lý KVM**

## Bước 3: Sử dụng lệnh virt-manger để mở công cụ 

<img src="http://i.imgur.com/k2y7c7R.png">

### Tạo máy ảo từ file images có sẵn (giống như file ghost)

Như bài viết trước minh đã tải file img về rồi và để trong thư mục /var/lib/libvirt/images/

- Chọn New và nhập tên máy ảo 

<img src="http://i.imgur.com/D9QpmKH.png">

- Chọn Forward để sang bước tiếp

- Chọn Browse để tìm đến file images có sẵn

<img src ="http://i.imgur.com/3CgACf4.png">

- Chọn CPU và bộ nhớ ram

<img src="http://i.imgur.com/hVhEQzd.png">

- Lựa chọn vào mục Customize configuration before install 

- Advance Options để quan sát card mạng cho máy ảo, trong hướng dẫn này sử dụng card Bridge là minhnv

<img src="http://i.imgur.com/Fqbpt9m.png">

- Lựa chọn vào mục Boot Options
- Tích vào mục Hard Disk để thiết lập chế độ boot của máy ảo từ disk
- Lựa chọn Apply để chấp nhận các thiết lập.
- Sau đó chọn Begin Installation để bắt đầu khởi động máy ảo.

Cuối cùng màn hình console của máy ảo sẽ xuất hiện và có thể đăng nhập được vào máy ảo

### Tạo VM bằng file iso

Chúng ta thực hiện tương tự các bước như tạo VM bằng image. Nhưng chúng ta chọn ``local install media``

<img src="http://i.imgur.com/vtjEHCN.png">

Chọn đường dẫn đến file iso đã tải về trong máy.

<img src="http://i.imgur.com/st7I2Ms.png">

## Virsh Command Line Interfaces

- Các tùy chọn quản lý cơ bản :

 - help : Hiển thị trợ giúp
 - list : Hiển thị danh sách các domains
 - creat : Thiết lập 1 domain từ thư mục XML
 - start : Khởi động một domain đã hoạt động trước đó.
 - destroy : Xóa đi một domain
 - define : Định nghĩa một domain (không phải như start)
 - domid : chuyển từ dạng domain name hoặc UUID sang domain id
 - domuuid : chuyển đổi từ domain name hoặc domain id sang UUID
 - domname : chuyển đổi từ domain id hoặc UUID sang domain name.
 - dominfo : thông tin về domain
 - domstate : trạng thái của domain
 - quit : thoát khỏi Virsh CLI
 - reboot : khởi động lại domain
 - restore : quay lại một trạng thái nào đó của domain
 - resum : tiếp tục hoạt động một domain sau khi tạm ngưng
 - save : lưu trạng thái domain
 - shutdown : tắt domain
 - suppend : tạm ngưng hoạt động domain
 - undefine : Bỏ định nghĩa domain
 

- Thay đổi thông tin về domain

### Bước 1: Xuất file xml của domain sang 1 file khác 
 
``virsh dumpxml vm01> new.xml``

### Bước 2: Back up lại xml của vm01
``cp vm01.xml vm01.bka``

### Bước 3: Chỉnh sửa file new.xml. Ví dụ như thay đổi thông tin về ram, cpu, ...

### Bước 4: Đưa file new.xml vào thư mục ``/etc/libvirt/qemu.``. Và định nghĩa nó: 

``virsh define new.xml``





