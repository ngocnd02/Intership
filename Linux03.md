# Mounting
`mounting` (gắn kết) đề cập đến quá trình kết nối một hệ thống tệp vào cây thư mục của hệ thống. Nó cho phép hệ thống tệp (file system) trở nên có sẵn để sử dụng, thường thông qua việc gắn nó vào một thư mục cụ thể trong cây thư mục của hệ thống.
## Mouting local file systems
### mount
- Để **mount** một phân vùng hoặc hệ thống tệp cục bộ, bạn có thể sử dụng lệnh `mount` trên hệ thống Linux. Ví dụ, để `mount` một phân vùng Ext4 từ /dev/sda1 vào một thư mục có tên là /mnt/data, bạn có thể sử dụng lệnh sau:
	```sh
	mount -t ext4 /dev/sda1 /mnt/data
	```
### umount
- Lệnh **umount** trong hệ điều hành Unix/Linux được sử dụng để ngắt kết nối (unmount) một hệ thống tệp hoặc phân vùng đã được mount trước đó khỏi cây thư mục của hệ thống.
	```sh
	umount /mnt/data
	```
## Mount temporary and permanent
- **Temporary mount**: Thực hiện bằng lệnh `mount` và sẽ mất khi hệ thống khởi động lại
- **Permanent mount**: Cấu hình trong `/etc/fstab` để tự động mount khi hệ thống khởi động lại.
# Troubleshooting tools
### lsof
- Lệnh **lsof** (list open files) trong Unix/Linux là một tiện ích mạnh mẽ cho phép xem thông tin về các tệp tin và các tài nguyên hệ thống đang được mở hoặc sử dụng bởi các tiến trình trên hệ thống.
- Cú pháp cơ bản: 
	```sh
	lsof [option]
	```
# UUID'S
-  **UUID** (Universally Unique Identifier) là một chuỗi định danh duy nhất được sử dụng để nhận diện các đối tượng như phân vùng đĩa, tệp tin, hoặc thiết bị với tính duy nhất trên hệ thống.
- Sử dụng trog linux Filesystem
	- `/etc/fstab` trong cấu hình này, UUID được sử dụng để mount phân vùng. Thay vì sử dụng đường dẫn /dev/sdXY, bạn có thể sử dụng UUID để mount phân vùng một cách duy nhất và an toàn hơn.
- Quản Lý Thiết Bị: Được sử dụng trong việc nhận diện và quản lý các thiết bị, cho phép các ứng dụng và hệ thống nhận biết chính xác từng đối tượng mà không bị nhầm lẫn.

# Introduction to RAID
- RAID (Redundant Array of Independent Disks) là một phương pháp kết hợp nhiều ổ đĩa cứng thành một tập hợp lưu trữ dữ liệu với mục tiêu tăng cường hiệu suất hoặc độ tin cậy.
- Mục tiêu của RAID
	- **Tăng Tốc Độ và Hiệu Suất**: Bằng cách chia nhỏ dữ liệu và phân phối chúng qua nhiều ổ đĩa, RAID có thể tăng tốc độ đọc và ghi dữ liệu.
	- **Bảo Vệ Dữ Liệu**: RAID cung cấp cơ chế dự phòng để đảm bảo dữ liệu không bị mất trong trường hợp một hoặc nhiều ổ đĩa gặp sự cố.
	- **Tăng Khả Năng** Tolerant Fault: Có khả năng tiếp tục hoạt động bình thường khi một hoặc nhiều ổ đĩa gặp sự cố.
- Cấp độ RAID phổ biến:
	- **RAID 0 (Striping)**: Tăng tốc độ bằng cách chia dữ liệu thành các phần nhỏ và ghi đồng thời lên các ổ đĩa khác nhau. Tuy nhiên, không có dự phòng dữ liệu, nếu một ổ đĩa gặp sự cố, toàn bộ dữ liệu có thể mất.
	- **RAID 1 (Mirroring)**: Lưu trữ bản sao chép dữ liệu trên các ổ đĩa khác nhau. Nếu một ổ đĩa gặp sự cố, dữ liệu vẫn được bảo vệ trên ổ đĩa còn lại.
	- **RAID 5 và RAID 6 (Striping with Parity)**: Sử dụng phương pháp chia dữ liệu và thông tin dự phòng (parity) để bảo vệ dữ liệu khi một ổ đĩa gặp sự cố. RAID 6 cung cấp mức độ bảo vệ cao hơn bằng cách sử dụng hai khối thông tin dự phòng.
	- **RAID 10 (Striping và Mirroring)**: Kết hợp cả phương pháp striping và mirroring. Dữ liệu được chia thành các phần nhỏ và được sao chép đồng thời lên các ổ đĩa khác nhau.
### mdadm
- Lệnh `mdadm` là công cụ quản lý RAID trong hệ thống Linux. Nó được sử dụng để tạo, quản lý và kiểm tra các thiết bị RAID trên hệ thống của bạn.
```sh
 mdadm --detail /dev/md0    # Hiển thị thông tin chi tiết về thiết bị RAID /dev/md0
 mdadm --query --detail /dev/md0  # Hiển thị thông tin cụ thể về thiết bị RAID /dev/md0
 mdadm --examine /dev/sda   # Xem thông tin về ổ đĩa cụ thể sử dụng trong RAID
```
# Logical volume management
`Logical Volume Management (LVM)` là một công cụ trong hệ điều hành Linux cho phép quản lý không gian lưu trữ ổ đĩa một cách linh hoạt hơn bằng cách tạo ra các logical volume từ các physical volume.
**Các khái niệm cơ bản**
- **Physical Volume (PV)**: Đây là các phân vùng hoặc ổ đĩa vật lý mà LVM sử dụng để tạo các logical volume.
- **Volume Group (VG)**: Là một nhóm các physical volume kết hợp lại với nhau. Từ VG, bạn có thể tạo ra các logical volume.
- **Logical Volume (LV)**: Là phần của không gian lưu trữ trong VG và có thể được coi như các phân vùng ảo. LV có thể được phân vùng, định dạng và sử dụng như các phân vùng thông thường.