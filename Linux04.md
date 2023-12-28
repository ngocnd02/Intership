# Thực hành thao tác các câu lệnh trên CentOS
- Thông tin hệ điều hành: `# cat /etc/*release`

<a href="https://imgur.com/GX5G06D"><img src="https://i.imgur.com/GX5G06D.png" title="source: imgur.com" />
- Thông tin bộ nhớ: `# head /proc/meminfo`

<a href="https://imgur.com/AUcWX2R"><img src="https://i.imgur.com/AUcWX2R.png" title="source: imgur.com" /></a>
- File hệ thống: `# df -h`

<a href="https://imgur.com/jPItDA8"><img src="https://i.imgur.com/jPItDA8.png" title="source: imgur.com" /></a>
- Thông tin về cpu: `# cat /proc/cpuinfo | grep model`

<a href="https://imgur.com/wh2gaeB"><img src="https://i.imgur.com/wh2gaeB.png" title="source: imgur.com" /></a>
- Hiển thị thông tin về các tiến trình đang chạy và tài nguyên hệ thống: `# top`

<a href="https://imgur.com/85ggiyr"><img src="https://i.imgur.com/85ggiyr.png" title="source: imgur.com" /></a>
- Liệt kê các phân vùng ổ cứng trong hệ thống : `fdisk -l`

<a href="https://imgur.com/bU1QGnK"><img src="https://i.imgur.com/bU1QGnK.png" title="source: imgur.com" /></a>

# Logical volume management
`Logical Volume Management (LVM)` là một công cụ trong hệ điều hành Linux cho phép quản lý không gian lưu trữ ổ đĩa một cách linh hoạt hơn bằng cách tạo ra các logical volume từ các physical volume.
**Các khái niệm cơ bản**
- **Physical Volume (PV)**: Đây là các phân vùng hoặc ổ đĩa vật lý mà LVM sử dụng để tạo các logical volume.
- **Volume Group (VG)**: Là một nhóm các physical volume kết hợp lại với nhau. Từ VG, bạn có thể tạo ra các logical volume.
- **Logical Volume (LV)**: Là phần của không gian lưu trữ trong VG và có thể được coi như các phân vùng ảo. LV có thể được phân vùng, định dạng và sử dụng như các phân vùng thông thường.
### Tạo Physical Volume (PV)
- Tạo 2 Physical Volume từ 2 ổ sdb và sdc: `# pvcreate /dev/sdb /dev/sdc`
```sh
[root@localhost ~]# pvcreate /dev/sdb /dev/sdc
Physical volume "/dev/sdb" successfully created.
Physical volume "/dev/sdc" successfully created.
```
- Hiển thị thông tin về Physical Volumes
Câu lệnh: `# pvdisplay`

<a href="https://imgur.com/WjcwRat"><img src="https://i.imgur.com/WjcwRat.png" title="source: imgur.com" /></a>
### Tạo Volume Groups (VG)
- Lệnh kiểm tra những VG hiện có: `#vgs`

<a href="https://imgur.com/PJfVdpw"><img src="https://i.imgur.com/PJfVdpw.png" title="source: imgur.com" /></a>
- Lệnh tạo Volume Group
Câu lệnh: `# vgcreate my_vg /dev/sdb1 /dev/sdc1`

- Xem thông tin về VG: 
Câu lệnh: `# vgdisplay`

<a href="https://imgur.com/Yrh5u6b"><img src="https://i.imgur.com/Yrh5u6b.png" title="source: imgur.com" /></a>

### Tạo Logical Volume (LV)
- Lệnh kiếm tra xem có những  LV nào: 
Câu lệnh: `# lvs`
- Lệnh tạo LV:
Câu lệnh: `lvcreate -n <tên_logical_volume> -L +<kích_thước> <tên_volume_group>`
- Lệnh kiểm tra thông tin:
Câu lệnh: ` # lvdisplay`

# System management
## logging
- Lệnh xem ai đang đăng nhập: `# who`

- Lệnh hiển thị lịch sử đăng nhập của người dùng vào hệ thống: `# last`

<a href="https://imgur.com/M1IuZ4m"><img src="https://i.imgur.com/M1IuZ4m.png" title="source: imgur.com" /></a>
- Lệnh hiển thị thông tin đăng nhập cuối cùng của tất cả người dùng trên hệ thống: `# lastlog`

<a href="https://imgur.com/W4pm6Bp"><img src="https://i.imgur.com/W4pm6Bp.png" title="source: imgur.com" /></a>
- Lệnh hiển thị danh sách các nỗ lực đăng nhập không hơp lệ: `# lastb`

<a href="https://imgur.com/6E2hgpw"><img src="https://i.imgur.com/6E2hgpw.png" title="source: imgur.com" /></a>


# Memory management
## Display memory and cache
- Lệnh xem thông tin về bộ nhớ: `# cat /proc/meminfo`

<a href="https://imgur.com/mFBpQol"><img src="https://i.imgur.com/mFBpQol.png" title="source: imgur.com" /></a>
- Lệnh hiện thị thông tin về RAM và Swap

<a href="https://imgur.com/UJBXa00"><img src="https://i.imgur.com/UJBXa00.png" title="source: imgur.com" /></a>

## Management swap space
- Swap space cho phép hệ thống sử dụng không gian trên ổ đĩa làm bộ nhớ tạm thời khi bộ nhớ vật lý (RAM) không đủ để đáp ứng nhu cầu của các tiến trình hoặc chương trình đang chạy. Khi RAM đã đầy, dữ liệu không sử dụng hoặc ít sử dụng từ RAM được di chuyển vào swap space, giải phóng RAM cho các tiến trình quan trọng hơn.
- Lệnh tạo ra phân vùng swap mới: `# mkswap /dev/hda1`
- Kích hoạt vùng swap đã tạo: `# mkswap /dev/hda1`
- Hiển thị thông tin về các vùng swap: `# cat /proc/swaps`