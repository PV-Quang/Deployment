## 1. HƯỚNG DẪN CÀI ĐẶT CLUSTERCONTROL TRÊN UBUNTU 24.04

> Cài đặt Ubuntu Server 24.04 và update hệ thống.

``` shell
apt update -y
apt upgrade -y
```

> Link hướng dẫn cài đặt từ trang chủ ClusterControl: https://docs.severalnines.com/clustercontrol/latest/getting-started/quickstart/


### BƯỚC 1: Download và chạy script để tiến hành cài đặt ClusterControl.

``` shell
wget https://severalnines.com/downloads/cmon/install-cc  
chmod +x install-cc  
sudo ./install-cc 
```
<img width="1321" height="701" alt="Image" src="https://github.com/user-attachments/assets/5b5a95e6-b702-47c4-9998-f2cda4720605" />

### BƯỚC 2: Mở trình duyệt lên và truy cập vào *https://clustercontrol-url* để thực hiện tiếp các bước thiết lập ban đầu cho ClusterControl.

<img width="1300" height="672" alt="Image" src="https://github.com/user-attachments/assets/9281a178-d6ca-40ed-bb10-d96d44d39d7d" />

<img width="1299" height="671" alt="Image" src="https://github.com/user-attachments/assets/50915158-aea6-43ac-984b-b417cbf1f602" />

### BƯỚC 3: Cấu hình SSL Certificate cho WEB UI.
> cd đến thư mục **_/usr/share/ccmgr_** rồi thay cert và key tương ứng vào file _**server.crt**_ và **_server.key_** sau đó restart service cmon.

``` shell
systemctl restart cmon-* 
```
<img width="1257" height="278" alt="Image" src="https://github.com/user-attachments/assets/41e4c521-c800-41a7-9667-e6b9834e85c6" />

<img width="1438" height="583" alt="Image" src="https://github.com/user-attachments/assets/7718f7f2-d56a-4432-9e4e-4a8409879bd9" />

### BƯỚC 4: Tạo SSH Key.
> ClusterControl sử dụng ssh key ssh đến các node DB để deploy DB.

``` shell
ssh-keygen -t rsa
```
<img width="1440" height="688" alt="Image" src="https://github.com/user-attachments/assets/10c940dc-663a-4cff-80a2-27fc3d94587a" />

> Copy public key đến file **_/root/.ssh/authorized_keys_** các node DB.

``` shell
ssh-copy-id -i ~/.ssh/id_rsa {target_node_IP_address}
```

<img width="1378" height="357" alt="Image" src="https://github.com/user-attachments/assets/16da4b2b-c55d-4b3b-8d38-7a4cc69d832c" />

--------------

## 2. TRIỂN KHAI SQL SERVER DB CLUSTER
> Cài đặt Ubuntu Server 22.04 và update hệ thống (SQL SERVER chưa hỗ trợ Ubuntu Server 24.04).

``` shell
apt update -y
apt upgrade -y
```
> Tại giao diện ClusterControl chọn **Clusters** -> **Deploy a cluster**

<img width="1370" height="513" alt="Image" src="https://github.com/user-attachments/assets/8586748a-d829-4d3e-845a-b0124059d3e8" />

> **Create a database cluster**

<img width="1364" height="832" alt="Image" src="https://github.com/user-attachments/assets/4f5eea27-8dc1-4138-953b-e3a907c942c5" />

> Chọn **SQL SERVER**

<img width="1363" height="828" alt="Image" src="https://github.com/user-attachments/assets/8d3653db-a907-4ac1-a535-a88c0ff3b8a4" />

> Nhập tên cho cluster DB

<img width="1363" height="716" alt="Image" src="https://github.com/user-attachments/assets/c86f05aa-fd30-4172-aa28-b9c8a34b1e78" />

> Cấu hình SSH đến DB Node

<img width="1353" height="800" alt="Image" src="https://github.com/user-attachments/assets/e570cedb-504b-4174-92ce-303651de89d8" />

> **Node configuration** (lưu lại  Admin username và password để login DB)

<img width="1356" height="860" alt="Image" src="https://github.com/user-attachments/assets/67e8b0d7-dc7d-4799-ba67-97e607f241bb" />

> **Add node** (SQL Server chỉ chấp nhận nhập node FQDN  -  đặt file host trong VM nếu không có DNS server) 

<img width="1339" height="712" alt="Image" src="https://github.com/user-attachments/assets/4a81c38c-9fdf-44d4-84dd-37ab6d970685" />

> Preview lại thông tin và nhấn **Finish** để tiến hành cài đặt

<img width="1368" height="893" alt="Image" src="https://github.com/user-attachments/assets/434aa9fa-830e-4f89-a607-56c65e8b9e74" />

### Truy cập và sử dụng SQL Server
> Sử dụng SQL Server Management Studio để login và sử dụng DB
> Server name: nhập đúng server name của VM DB
> User Name và Password ở bước **Node configuration**

<img width="1314" height="869" alt="Image" src="https://github.com/user-attachments/assets/5958f044-ff06-4177-86c9-904341a7df79" />

> Test Restore DB (File Backup DB phải nằm ở máy Chủ SQL Server)

<img width="1310" height="700" alt="Image" src="https://github.com/user-attachments/assets/ae057619-171d-4fa9-aa08-95fb27a96fe5" />

<img width="1237" height="852" alt="Image" src="https://github.com/user-attachments/assets/739078d3-2567-4161-9726-0341d196ea5f" />

<img width="1287" height="533" alt="Image" src="https://github.com/user-attachments/assets/a43f7c80-6318-460d-8566-c93d451748e0" />
