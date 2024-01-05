# Swap memory
### 1. Swap memory là gì?
- **Swap memory** được sử dụng để bổ sung cho bộ nhớ vật lý (RAM). Khi RAM của máy tính đã đầy hoặc cạn kiệt do sử dụng quá nhiều ứng dụng hoặc quá trình, hệ điều hành có thể sử dụng swap memory để lưu trữ dữ liệu tạm thời, giải phóng RAM cho các ứng dụng khác.

- **Swap memory** thường là một phần trên ổ cứng được cấu hình để hoạt động như bộ nhớ ảo. Khi RAM đầy, dữ liệu không còn được sử dụng thường xuyên sẽ được chuyển từ RAM sang swap memory để tạo không gian cho các ứng dụng và quá trình khác cần sử dụng RAM.

- Tuy nhiên, việc sử dụng swap memory có thể làm giảm hiệu suất hệ thống do tốc độ truy cập dữ liệu trên ổ cứng thấp hơn nhiều so với RAM. Khi hệ thống phải thường xuyên truy cập swap memory để lấy dữ liệu trở lại RAM, điều này có thể gây chậm trễ và làm giảm trải nghiệm người dùng.

### 2. Tạo Swap File
**Tạo một file sử dụng làm swap**
- Câu lệnh: `# fallocate -l 2G /mnt/swapfile`
- Câu lệnh này tạo một file với kích thước cụ thể là 2G và đặt tên là swapfile trong thư mục /mnt
- Trong đó: 
	- **fallocate** Là một công cụ trong hệ thống Linux dùng để cấp phát không gian cho file.
	- **-l 2G** chỉ định dung lượng cho file mới được tạo là 2GB
	- Lưu ý: khi sử dụng **fallocate** để tạo file swap, không có dữ liệu nào thực sự được ghi vào file này ngay lập tức. Thay vào đó, không gian trống được cấp phát trên ổ đĩa để sử dụng khi cần thiết, và file sẽ chứa dữ liệu khi swap được kích hoạt để lưu trữ thông tin từ RAM khi RAM đầy.

- Các tùy chọn phổ biến đi cùng lệnh **fallocate**
	- **-l, --length**: Sử dụng để chỉ định kích thước của file mới. Ví dụ: -l 1G sẽ tạo một file có dung lượng 1GB.

	- **-o, --offset**: Cho phép bạn chỉ định vị trí bắt đầu cấp phát không gian trong file hiện có. Đây không phải là tùy chọn thường xuyên được sử dụng khi tạo swap file.

	- **--keep-size**: Tạo file với dung lượng được chỉ định nhưng không cấp phát không gian thực tế cho file ngay lập tức. Tùy chọn này có thể hữu ích khi bạn muốn giữ trước kích thước của file nhưng chỉ cấp phát không gian khi cần thiết sau này.

	- **--punch-hole**: Xóa không gian không cần thiết từ file. Điều này cho phép giảm dung lượng thực tế của file mà không cần xóa file hoặc di chuyển dữ liệu.

	- **--dig-holes**: Tạo ra các "lỗ" (holes) trong file, là không gian không cần thiết không chiếm dung lượng thực tế trên ổ đĩa. Điều này thường được sử dụng để tạo file sparse (thưa) để tiết kiệm dung lượng đĩa.

**Định dạng file swap**
- Câu lệnh: 
	```sh
	chmod 600 /mnt/swapfile
	mkswap /mnt/swapfile
	```
- Câu lệnh `chmod 600 /mnt/swapfile` sử dụng **chmod** để đặt quyền cho file, ở đây 600 có nghĩa chỉ có chủ sử hữu mới có quyền đọc và ghi file, còn lại không ai có quyền truy cập file này
- Câu lệnh `mkswap /mnt/swapfile` sử dụng **mkswap** để định dạng một file để sử dụng như swap space.

**Kiểm tra swap đã hoạt động hay chưa**
- Câu lệnh: `# swapon --show`

- Các tùy chọn phổ biến của **swapon**:
	- **-a, --all**: Kích hoạt tất cả các phân vùng hoặc tệp swap được chỉ định trong /etc/fstab.

	- **-s, --summary**: Hiển thị thông tin tổng quan về các phân vùng hoặc tệp swap đang hoạt động.

	- **-v, --verbose**: Hiển thị thông tin chi tiết về quá trình kích hoạt swap.

![Imgur](https://i.imgur.com/189NIWz.png)


### 3. Tạo Swap Partition

**Sử dụng công cụ quản lý ổ đĩa (như fdisk hoặc parted) để tạo partition mới có loại là swap**
- Câu lệnh: `# fdisk /dev/sdX`

Tạo một partition mới
- Nhấn **n** và chọn loại **p** (primary partition) hoặc **e** (extended partition) tùy thuộc vào loại phân vùng bạn muốn tạo.
- Chọn số thứ tự cho partition (ví dụ: 1).
- Chọn dung lượng cho partition swap (ví dụ: nhập +42 để tạo partition 2GB).

Đặt loại của partition là 82 (Linux swap)
- Nhấn **t** để thay đổi loại cua partition
- Chọn số thứ tự của partition đã tạo (ví dụ: 1).
- Nhập 82 để đặt loại là Linux swap.

**Định dạng partition mới thành swap**
- Câu lệnh: `# mkswap /dev/sdX1`

**Kích hoạt swap partition**
- Câu lệnh: `# swapon /dev/sdX1`

### 4. Xóa file swap

**Vô hiệu hóa swap**
- Câu lệnh: `# swapoff /mnt/swapfile`

**Xóa swap file**
- Câu lệnh: `# rm /mnt/swapfile`

**Loại bỏ thông tin swap trong /etc/fstab (nếu cần)**
Nếu thông tin về swap file đã được thêm vào file /etc/fstab để tự động kích hoạt sau khi khởi động, bạn cũng nên loại bỏ dòng liên quan đến swap file trong file này.

Mở file /etc/fstab với trình soạn thảo văn bản như nano hoặc vi.Tìm và xóa dòng chứa đường dẫn đến swap file. Sau khi xóa, lưu lại và đóng file.

# Logical Volume Management
Logical Volume Management (LVM) là một công cụ quản lý không gian lưu trữ trên hệ thống Linux, cho phép quản lý và phân chia ổ đĩa cứng một cách linh hoạt hơn so với việc sử dụng phân vùng truyền thống.

**Các thành phần chính của LVM bao gồm:**
1. **Physical Volumes (PVs)**: Đây là các ổ đĩa vật lý hoặc phân vùng trên các ổ đĩa được sử dụng để tạo thành không gian lưu trữ.

2. **Volume Groups (VGs)**: Physical Volumes được nhóm lại thành Volume Groups, tạo thành một không gian lưu trữ lớn hơn bằng cách kết hợp các PVs.

3. **Logical Volumes (LVs)**: LVs là phần được sử dụng để lưu trữ dữ liệu. Chúng được tạo ra từ không gian lưu trữ có sẵn trong các Volume Groups và có thể co giãn hoặc thu nhỏ linh hoạt theo nhu cầu.

**Quy trình sử dụng LVM bao gồm các bước sau**:

1. **Tạo Physical Volumes (PVs)**: Định dạng các ổ đĩa hoặc phân vùng để sử dụng với LVM.

2. **Tạo Volume Groups (VGs)**: Tạo các nhóm từ các PVs đã tạo, tổng hợp chúng để tạo ra không gian lưu trữ lớn hơn.

3. **Tạo Logical Volumes (LVs)**: Tạo các phân vùng logic từ không gian lưu trữ trong các VGs. Các LVs có thể được co giãn hoặc thu nhỏ dễ dàng.

4. **Định dạng và gán file system**: Định dạng LVs và gán file system để có thể sử dụng như các phân vùng thông thường.

5. **Quản lý và vận hành**: LVM cung cấp các công cụ để mở rộng không gian lưu trữ, thay đổi kích thước LVs, thậm chí là di chuyển dữ liệu giữa các PVs một cách an toàn.

**Tạo Physical Volumes (PVs), Volume Groups (VGs) và Logical Volumes (LVs)**

1. Xác định ổ đĩa hoặc phân vùng để sử dụng
- Câu lệnh: `# fdisk -l`
- **fdisk** là một câu lệnh quản lý ổ đĩa. 
- Các thông số đầu ra trong lệnh `fdisk -l`:
	- **Device**: Định danh của thiết bị, chẳng hạn như /dev/sda, /dev/sdb,...

	- **Boot**: Có phải là phân vùng khởi động hay không.

	- **Start**: Vị trí bắt đầu của phân vùng trong ổ đĩa (được hiển thị theo đơn vị sectors).

	- **End**: Vị trí kết thúc của phân vùng trong ổ đĩa (cũng được hiển thị theo đơn vị sectors).

	- **Sectors**: Số lượng sectors của phân vùng.

	- **Size**: Kích thước của phân vùng, thường được hiển thị dưới dạng sectors hoặc dưới dạng dung lượng thực tế (MB, GB, TB).

	Type: Loại phân vùng, chẳng hạn như Linux, NTFS, FAT32, và nhiều loại khác.

	Id: Mã định danh cho loại phân vùng.

LINK

- Các tùy chọn phổ biến với lệnh **fdisk**
	- **fdisk -l**: Hiển thị thông tin về các ổ đĩa và phân vùng hiện có trong hệ thống.

	- **fdisk /dev/sdx**: Mở fdisk để thao tác với ổ đĩa cụ thể (/dev/sdx là địa chỉ của ổ đĩa, ví dụ: /dev/sda).

	- **n**: Tạo một phân vùng mới.

	- **d**: Xóa một phân vùng.

	- **p**: Hiển thị danh sách các phân vùng.

	- **t**: Thay đổi loại phân vùng.

	- **w**: Lưu các thay đổi và thoát khỏi fdisk.

	- **q**: Thoát khỏi fdisk mà không lưu thay đổi.

2. Tạo Physical Volumes
- Câu lệnh: `# pvcreate /dev/sdX`
- Lệnh này sẽ tạo một Physical Volumes trên thiết bị đĩa /dev/sdX
- Các tùy chọn phổ biến lệnh **pvcreate**

	**-v hoặc --verbose**: Hiển thị thông tin chi tiết hơn về quá trình tạo Physical Volume.

	**-ff hoặc --force**: Bắt buộc tạo Physical Volume trên các thiết bị mà đã được sử dụng trước đó và có dấu vết LVM còn tồn tại.

	**-y hoặc --yes**: Tự động đồng ý với các xác nhận hoặc thông báo.

	**-u <Mega|Giga|Tera>**: Xác định kích thước PE (Physical Extent) mặc định cho Physical Volume được tạo.

	**--dataalignment <number>[:physical|none]**: Thiết lập định vị dữ liệu (data alignment) cho Physical Volume.

	**--labelsector <number>**: Chỉ định sector bắt đầu cho dấu vết metadata của LVM.
3. Tạo Volume Groups
- Câu lệnh: `sudo vgcreate vg_name /dev/sdX `
- Tạo ra một Volume Group có tên vg_name từ Physical Volume trên thiết bị /dev/sdX
- Thay vg_name bằng tên của Volume Group và /dev/sdX bằng ổ đĩa đã tạo PV trên
- Các tùy chọn phổ biến cho lệnh **vgcreate**:

	- **-v hoặc --verbose**: Hiển thị thông tin chi tiết về quá trình tạo Volume Group.

	- **-s <size> hoặc --physicalextentsize <size>**: Xác định kích thước Physical Extent (PE) cho Volume Group. Đây là đơn vị cơ bản cho việc phân bố không gian lưu trữ trong LVM.

	- **--maxlogicalvolumes <number>**: Đặt giới hạn số Logical Volume tối đa có thể tạo trong Volume Group.

	- **--physicalextentsize <size>**: Xác định kích thước PE cho VG.

4. Tạo Logical Volume
- Câu lệnh:` #lvcreate -n lv_name -L sizeG vg_name`
- Lệnh này sẽ tạo một Logical Volume (LV) mới có tên là "my_lv" có kích thước 10GB trong Volume Group "my_vg".
- Trong đó lv_name là tên của Logical Volume, sizeG là dung lượng (VD: 10G) và vg_name là tên của Volume Group
- Các tùy chọn phổ biến của lệnh **lvcreate**:

	- **-n <LV_name>**: Chỉ định tên cho Logical Volume mới.

	- **-L <size> hoặc --size <size>**: Xác định kích thước của Logical Volume, ví dụ: 10G cho 10GB, 100M cho 100MB.

	- **-l <number_of_extents>**: Thay vì kích thước cụ thể, bạn có thể xác định số lượng extents (đơn vị lưu trữ cơ bản) để sử dụng cho LV.

	- **-C y hoặc --contiguous y**: Tạo Logical Volume có không gian lưu trữ liên tục.

	- **-i <number_of_stripes> hoặc --stripes <number_of_stripes>**: Xác định số lượng stripes (đối với RAID).

	- **-I <size> hoặc --stripesize <size>**: Xác định kích thước stripe cho Logical Volume.

	- **-Z y hoặc --zero y**: Làm sạch dữ liệu trên Logical Volume bằng cách ghi các giá trị 0.

	- **-Zn hoặc --zero n**: Không làm sạch dữ liệu.

	- **-v hoặc --verbose**: Hiển thị thông tin chi tiết hơn về quá trình tạo Logical Volume.

	--type <type>: Xác định loại của Logical Volume (vd: linear, raid1, snapshot).

5. Định dạng và Mount Logical Volume
Định dạng Logical Volume bằng một hệ thống tệp (filesystem), ví dụ như ext4
- Câu lệnh: `# mkfs.ext4 /dev/my_vg/my_lv`
- Lệnh này tạo một hệ thống tệp ext4 trên Logical Volume (LV) đã được tạo trong Volume Group (VG) có tên là "my_vg".

Tạo một thư mục để mount Logical Volume và mount nó
- Câu lệnh:
	```sh
	mkdir /mnt/my_volume
	mount /dev/my_vg/my_lv /mnt/my_volume
	```
- `mkdir /mnt/my_volume`: Tạo một thư mục có tên là my_volume trong thư mục /mnt. Thư mục này sẽ được sử dụng làm điểm gắn kết cho Logical Volume.
- `mount /dev/my_vg/my_lv /mnt/my_volume`: Gắn kết (mount) Logical Volume có tên là my_lv trong Volume Group my_vg vào thư mục /mnt/my_volume. Điều này cho phép bạn truy cập và làm việc với dữ liệu trong LV thông qua đường dẫn /mnt/my_volume.

## Thay đổi kích thước của Logical Volume
1. Kiểm tra thông tin hiện tại của Logical Volume
- Câu lệnh: `# lvdisplay /dev/vg_name/lv_name`
- vg_name và lv_name là tên của Volume Group và Logical Volume tương ứng.
- Các thông số khi dùng lệnh **lvdisplay**:
	- **Logical Volume Path**: Đường dẫn của Logical Volume, ví dụ: /dev/my_vg/my_lv.

	- **LV Name**: Tên của Logical Volume.

	- **VG Name**: Tên của Volume Group mà LV thuộc về.

	- **LV UUID**: UUID (Universal Unique Identifier) của Logical Volume.

	- LV Size**: Kích thước của Logical Volume.

	- Allocated PE**: Số lượng Physical Extents (PE) đã được phân bổ cho Logical Volume.

	- Current LE**: Số lượng Logical Extents (LE) hiện tại.

	- Segments**: Thông tin về các segment của Logical Volume, chẳng hạn như vị trí trên Physical Volumes.

	- LV Status**: Trạng thái của Logical Volume (active, inactive, suspended, ...).


2. Thay đổi kích thước của LV
Để mở rộng kích thước của Logical Volume, bạn có thể sử dụng lệnh **lvextend**
- Câu lệnh: `# lvextend -L +5G /dev/vg_name/lv_name`
- Lệnh này sẽ mở rộng kích thước của LV thêm 5GB 

- Câu lệnh: `lvextend -L new_size /dev/vg_name/lv_name`
- Lệnh này sẽ thay đổi kích thước của LV bằng một kích thước mới cụ thể. 

3. Thay đổi kích thước của hệ thống tệp (filesystem):
Nếu Logical Volume đang chứa một hệ thống tệp (filesystem) như ext4, bạn cần phải thay đổi kích thước của hệ thống tệp để phản ánh sự thay đổi dung lượng. Đối với ext4, bạn có thể sử dụng resize2fs:
- Câu lệnh: `# resize2fs /dev/vg_name/lv_name`

## Xóa Logical Volume
1. Xóa Logical Volume
Đầu tiên, bạn cần unmount LV nếu nó đang được sử dụng
- Câu lệnh: `umount /dev/vg_name/lv_name`
- Lệnh này để tháo gỡ (unmount) một hệ thống tệp (file system) được gắn kết (mounted) với Logical Volume (LV) trong Volume Group (VG).

Sau đó, xóa LV
- Câu lệnh: `# lvremove /dev/vg_name/lv_name`
- Lệnh này để xóa một Logical Volume (LV) cụ thể từ Volume Group (VG) trong LVM (Logical Volume Manager).
- Các tùy chọn phổ biến của **lvremove**:

	- **-f hoặc --force**: Xóa LV mà không cần xác nhận từ người dùng. Lệnh này làm cho quá trình xóa không yêu cầu xác nhận từ người dùng.

	- **-v hoặc --verbose**: Hiển thị thông tin chi tiết hơn về quá trình xóa LV.

	- **--select** : Chọn các LV cần xóa dựa trên tiêu chí cụ thể, ví dụ: lvremove --select 'lv_name=my_lv'.

	- **--yes hoặc -y** : Tự động đồng ý với các xác nhận hoặc thông báo.

2. Xóa Volume Group
Nếu bạn đã xóa tất cả các LV trong VG và muốn xóa VG:
- Câu lệnh: `# vgremove vg_name`

3. Xóa Physical Volume
- Câu lệnh: `# sudo pvremove /dev/sdX`
