# Tìm kiếm file
Các công cụ tìm kiếm được sử dụng để tìm file trên hệ thống: 
- **locate**- Tìm kiếm file theo tên
- **find**- Tìm kiếm các tập tin trong một hệ thống phân cấp thư mục 

### locate
Lệnh **locate** thực hiện một tìm kiếm cơ sở dữ liệu nhanh chóng của các đường dẫn tệp và sau đó xuất ra tất cả các tên phù hợp với một chuỗi con cụ thể đã cho.
Cho ví dụ, chúng ta muốn tìm tất cả các chương trình có tên bắt đầu bằng "zip". Vì chúng ta đang tìm kiếm các chương trình, có thể giả định rằng tên của thư mục chứa các chương trình sẽ kết thúc bằng "bin/"
- Câu lệnh: `# locate bin | grep zip`
- Lệnh này tìm kiếm trong cơ sở dữ liệu của locate tất cả các đường dẫn chứa từ "bin" và sau đó lọc kết quả này để chỉ hiển thị những dòng chứa từ "zip" bằng grep

![Imgur](https://i.imgur.com/baT7ieu.png)

- Các tùy chọn phổ biến của lệnh **locate**
	- **-i, --ignore-case**: Cho phép tìm kiếm không phân biệt chữ hoa chữ thường.
	- **-c, --count**: Chỉ hiển thị số lượng kết quả thay vì danh sách các tệp tin.
	- **-l, --limit**: Xác định số lượng kết quả tối đa để hiển thị.
	- **-b, --basename**: Chỉ tìm kiếm dựa trên tên tệp, bỏ qua đường dẫn.
	- **-S, --statistics**: Hiển thị thống kê về cơ sở dữ liệu locate, bao gồm thông tin về thời gian cập nhật gần nhất.

### find
Trong khi chương trình **locate** có thể tìm thấy một tệp chỉ dựa trên tên của nó, chương trình **find** tìm kiếm trong một thư mục cụ thể (và các thư mục con của nó) các tệp tin dựa trên nhiều thuộc tính khác nhau

- Cú pháp cơ bản: `# find /đường/dẫn/tìm/kiếm -option(s) pattern`
- Ví dụ: `# find . -name intro.txt`
- Lệnh này sẽ tìm kiếm tất cả các tệp có tên là "intro.txt" trong thư mục hiện tại (.) và trong các thư mục con của nó. Nếu có bất kỳ tệp nào cùng tên này hoặc mẫu tên tương tự, chúng sẽ được liệt kê ra trong kết quả.

![Imgur](https://i.imgur.com/twFrqyr.png)

- Một số tùy chọn phổ biến: 
	- **-name**: Tìm kiếm theo tên của tệp hoặc thư mục.
	- **-type**: Tìm kiếm theo loại của đối tượng (d: thư mục, f: tệp thực thể, l: liên kết, v.v.).
	- **-size**: Tìm kiếm theo kích thước của tệp.
	- **-mtime, -atime, -ctime**: Tìm kiếm theo thời gian sửa đổi (-mtime), thời gian truy cập (-atime), và thời gian thay đổi inode (-ctime).
	- **-exec**: Thực thi một lệnh trên mỗi kết quả tìm kiếm.


# Redundant Array of Independent Disks (RAID)
**RAID** là một phương pháp kết hợp nhiều ổ đĩa cứng để tạo thành một hệ thống lưu trữ dữ liệu. Mục tiêu của RAID là cung cấp tính sẵn sàng và tăng cường hiệu suất hoặc độ an toàn của dữ liệu thông qua việc phân chia, sao chép hoặc mã hóa dữ liệu qua nhiều ổ đĩa.

**Mục tiêu của RAID**
- Tăng Tốc Độ và Hiệu Suất: Bằng cách chia nhỏ dữ liệu và phân phối chúng qua nhiều ổ đĩa, RAID có thể tăng tốc độ đọc và ghi dữ liệu.
- Bảo Vệ Dữ Liệu: RAID cung cấp cơ chế dự phòng để đảm bảo dữ liệu không bị mất trong trường hợp một hoặc nhiều ổ đĩa gặp sự cố.
Tăng Khả Năng Tolerant Fault: Có khả năng tiếp tục hoạt động bình thường khi một hoặc nhiều ổ đĩa gặp sự cố.

**Một số cấu hình RAID phổ biến**
1. **RAID 0 (Striping)**: Phân chia dữ liệu thành các khối nhỏ và ghi lần lượt lên các ổ đĩa. Tăng tốc độ đọc/ghi vì dữ liệu được phân tán trên nhiều ổ đĩa, nhưng không có tính dự phòng. Nếu một ổ đĩa hỏng, toàn bộ dữ liệu trong hệ thống RAID 0 có thể bị mất.
2. **RAID 1 (Mirroring)**: Tạo bản sao chép (mirror) của dữ liệu trên một hoặc nhiều ổ đĩa. Tính dự phòng cao, dữ liệu vẫn tồn tại nếu một ổ đĩa hỏng, nhưng chi phí lưu trữ sẽ tăng do cần nhiều ổ đĩa hơn.
3. **RAID 5**: Phân chia dữ liệu thành các khối và lưu trữ thông tin kiểm tra dư thừa (parity) trên các ổ đĩa khác nhau. Tính dự phòng cho phép khôi phục dữ liệu khi một ổ đĩa hỏng, nhưng hiệu suất có thể giảm trong quá trình ghi dữ liệu.
4. **RAID 6**: Tương tự như RAID 5, nhưng lưu trữ hai thông tin kiểm tra dư thừa. Cung cấp dự phòng mạnh mẽ hơn khi có nhiều ổ đĩa hỏng cùng một lúc.
5. **RAID 10 (RAID 1+0)**: Kết hợp RAID 1 và RAID 0. Dữ liệu được sao chép (mirrored) trước khi phân chia và ghi lên các ổ đĩa khác nhau, cung cấp cả dự phòng cao và hiệu suất tốt.


# Quá trình khởi động của Linux
### 1. BIOS (Basic Input/Output System) & POST (Power-On Self Test)
- Máy tính bắt đầu quá trình khởi động ngay sau khi bạn bật nguồn điện. Quá trình đầu tiên này được gọi là **post** hoặc **power on self test**. Nếu mọi thứ diễn ra suôn sẻ, quá trình này dẫn đến BIOS. Nếu mọi thứ không êm đẹp, bạn có thể không nghe thấy gì, nghe thấy tiếng "beep" (bíp), hoặc thấy một thông báo lỗi trên màn hình. 

- **BIOS** là một chương trình nhúng trong firmware của máy tính.
	- Tất cả các máy tính Intel x86 sẽ có một hệ thống cơ bản đầu vào/đầu ra hoặc BIOS để phát hiện, xác định và khởi tạo phần cứng. BIOS sau đó tìm kiếm một thiết bị khởi động. Điều này có thể là ổ đĩa mềm, ổ cứng, đĩa CD, thẻ mạng hoặc ổ đĩa USB.

### 2. MBR (Master Boot Record)
- **MBR** là thông tin lưu trữ trong sector đầu tiên của ổ cứng.
- Nó chứa thông tin về nơi GRUB2 được lưu trữ để có thể tải vào RAM của máy tính.

### 3. GRUB2 (Grand Unified Boot Loader v2)
- GRUB2 là bootloader được tải từ MBR vào bộ nhớ RAM.
- Nó cung cấp một menu cho người dùng chọn hệ điều hành hoặc phiên bản cụ thể của Linux để khởi động.
- GRUB2 tải và khởi động kernel Linux.

### 4. Kernel (Nhân)
- **Nhân (Kernel)** là trái tim của hệ điều hành.
- Kernel tải các trình điều khiển cần thiết từ initrd.img (initial ramdisk) vào bộ nhớ.
- Sau đó, nó khởi động quá trình đầu tiên của hệ điều hành, thường là systemd.
### 5. Systemd (PID #1)
- Systemd là một hệ thống khởi động và quản lý tiến trình trong Linux.
- Nó khởi động tất cả các tiến trình cần thiết để hệ thống hoạt động.
- Systemd đọc file /etc/systemd/system/default.target để xác định run-level mặc định để đưa hệ thống vào.
### Run Levels
- Linux có 7 run levels (0 đến 6) mô tả trạng thái khác nhau của hệ thống, ví dụ: 0 là tắt hệ thống, 3 là chế độ đa nhiệm với dòng lệnh, 5 là chế độ đồ họa, và 6 là khởi động lại hệ thống.

Quá trình khởi động của Linux qua các bước này để chuẩn bị và khởi chạy hệ điều hành, cho phép người dùng tương tác với hệ thống một cách hiệu quả.

# Iptables
**iptables** là một công cụ quản lý tường lửa mạng mạnh mẽ được sử dụng để quản lý các luật tường lửa trên hệ thống

Chức năng của iptables
- **Kiểm Soát Truy Cập Mạng**: iptables cho phép bạn kiểm soát truy cập mạng bằng cách cho phép hoặc chặn các gói tin dựa trên các tiêu chí như địa chỉ IP nguồn, địa chỉ IP đích, cổng giao thức, giao thức, và nhiều tiêu chí khác.

- **Bảo Vệ Mạng**: Nó cung cấp các biện pháp bảo vệ mạng bằng cách chặn các cuộc tấn công từ xa hoặc ngăn chặn các gói tin có hành vi không mong muốn như SYN-flood hoặc ping of death.

- **Tạo Một Tường Lửa**: Bằng cách sử dụng iptables, bạn có thể tạo và cấu hình một tường lửa mạnh mẽ để bảo vệ hệ thống khỏi các mối đe dọa từ internet hoặc mạng nội bộ.

- **Chuyển Hướng Gói Tin**: iptables cũng cho phép chuyển hướng gói tin, có thể dùng để ánh xạ cổng (port mapping), dẫn hướng gói tin từ một cổng đến cổng khác trên cùng hoặc một máy chủ khác.

- **Kiểm Tra Tình Trạng Giao Tiếp Mạng**: Bạn có thể sử dụng iptables để kiểm tra tình trạng kết nối mạng, xem danh sách các quy tắc hiện tại và các gói tin đang được xử lý.

- **Tạo Các Quy Tắc Mạng Tùy Chọn**: iptables cung cấp khả năng tạo ra các quy tắc mạng tùy chỉnh, cho phép bạn điều chỉnh chi tiết các quy tắc tường lửa dựa trên nhu cầu cụ thể của mạng hoặc ứng dụng.

### Cách cài đặt iptables
Nếu iptables chưa được cài đặt, bạn có thể cài đặt gói iptables-services bằng lệnh sau:
- Câu lệnh: `# yum install iptables-services`
Khởi động dịch vụ iptable: 
- Câu lệnh: `# systemctl start iptables`
Kích hoạt khởi động cùng hệ thống
- Câu lệnh: `# systemctl enable iptables`

![Imgur](https://i.imgur.com/a6Hwmsf.png)


# SSH Client and Server
- **SSH (Secure Shell)** trong Linux là một giao thức mạng cung cấp cách thức an toàn để truy cập và quản lý các thiết bị từ xa. Nó cung cấp cơ chế mã hóa để bảo vệ thông tin truyền qua mạng.
- Thông qua SSH, người dùng có thể kết nối và làm việc từ xa với máy chủ hoặc thiết bị Linux từ bất kỳ nơi đâu, cho phép thực hiện các tác vụ như đăng nhập, thiết lập kết nối, truyền tệp và thực thi các lệnh từ xa một cách an toàn.
- Một kết nối ssh luôn bắt đầu bằng một bước bắt tay mật mã hóa, tiếp theo là việc mã hóa lớp vận chuyển sử dụng một thuật toán mã hóa đối xứng. Nói cách khác, kênh được mã hóa trước khi bạn bắt đầu nhập bất cứ điều gì.
- Sau đó, quá trình xác thực diễn ra (sử dụng user id/mật khẩu hoặc khóa công khai/tư nhân) và việc truyền thông có thể bắt đầu qua kết nối được mã hóa.
- Giao thức ssh sẽ ghi nhớ các máy chủ mà nó đã kết nối (và cảnh báo bạn trong trường hợp xảy ra điều gì đáng ngờ).

**Public and Private keys**
- **Khóa Công Khai (Public Key)**: Đây là phần của cặp khóa được chia sẻ rộng rãi và được lưu trữ trên máy chủ SSH. Khóa công khai được sử dụng để mã hóa thông tin trước khi gửi đi và cũng được sử dụng để xác thực người dùng. Khóa công khai không bao giờ được giữ bí mật và có thể được chia sẻ một cách an toàn với bất kỳ ai.

- **Khóa Riêng Tư (Private Key)**: Đây là phần của cặp khóa chỉ được lưu trữ trên máy tính cá nhân của người dùng. Khóa riêng tư được sử dụng để giải mã thông tin đã được mã hóa bằng khóa công khai và cũng để xác thực người dùng khi kết nối với máy chủ. Điều quan trọng là giữ cho khóa riêng tư một cách an toàn và không chia sẻ nó với bất kỳ ai.

Quá trình sử dụng khóa công khai và khóa riêng tư trong SSH diễn ra như sau:

1. Người dùng tạo cặp khóa công khai và khóa riêng tư trên máy tính của họ.
2. Khóa công khai được sao chép vào máy chủ mà người dùng muốn kết nối.
3. Khi người dùng kết nối với máy chủ, máy chủ sử dụng khóa công khai để mã hóa một tin nhắn ngẫu nhiên và gửi nó đến người dùng.
4. Người dùng sử dụng khóa riêng tư của mình để giải mã tin nhắn và gửi lại một phản hồi mã hóa cho máy chủ để chứng minh xác thực.
5. Nếu máy chủ có thể giải mã được tin nhắn, nó xác minh xác thực và cho phép người dùng kết nối.

### Đăng nhập vào máy chủ từ xa
- Để đăng nhập vào một máy chủ từ xa sử dụng SSH, bạn cần có thông tin đăng nhập và kết nối mạng đến máy chủ đó. Đầu tiên, mở terminal trên máy tính của bạn và sử dụng lệnh sau:
- Câu lệnh: `ssh username@remote_server_ip`
- Trong đó: 
	- **username** tên người dùng trên máy chủ
	- **remote_server_ip**: địa chỉ ip hoặc tên miền của máy chủ từ xa
- Nhập Mật khẩu Người Dùng: Sau khi nhập lệnh, bạn sẽ được yêu cầu nhập mật khẩu của người dùng trên máy chủ từ xa.
- Xác thực và Đăng Nhập: Sau khi nhập mật khẩu đúng, nếu thông tin đăng nhập hợp lệ, bạn sẽ đăng nhập vào máy chủ từ xa và có thể thực hiện các thao tác từ xa thông qua kết nối SSH.

Nếu máy chủ sử dụng cổng SSH không phải là cổng mặc định (22), bạn có thể chỉ định cổng khi kết nối bằng cách sử dụng -p:
- Câu lệnh: `ssh -p port_number username@remote_server_ip`

Một số tùy chọn phổ biến của lệnh **ssh**:
- **-p port**: Xác định cổng kết nối. Ví dụ: ssh -p 2222 username@remote_server_ip (để kết nối qua cổng 2222).

- **-i key_file**: Sử dụng khóa riêng tư khác thay vì khóa mặc định. Ví dụ: ssh -i /path/to/private_key username@remote_server_ip.

- **-l username**: Xác định người dùng trên máy chủ từ xa. Ví dụ: ssh -l username remote_server_ip.

- **-X**: Kích hoạt chế độ forwarding X11 để chạy các ứng dụng đồ họa từ xa.

- **-v**: Hiển thị thông tin chi tiết (verbose) về quá trình kết nối. Đây có thể giúp khi gặp sự cố kết nối.

- **-N**: Kết nối mà không mở cửa sổ terminal sau khi đăng nhập. Thường được sử dụng khi thiết lập tunnel hoặc chuyển tiếp cổng.

- **-T**: Để chỉ định rằng không cần shell sau khi đăng nhập, thường sử dụng với kết nối tunneling.

- **-C**: Kích hoạt nén dữ liệu trên kết nối SSH.

### sshd
- **sshd** là một phần mềm hoặc dịch vụ trên hệ thống Linux/Unix, đóng vai trò là máy chủ SSH (Secure Shell Server). Nó là daemon (tiến trình chạy nền) chịu trách nhiệm cho việc xử lý kết nối SSH đến hệ thống.
- **sshd** chấp nhận các yêu cầu kết nối từ xa qua giao thức SSH và quản lý việc xác thực người dùng, sau đó cho phép người dùng đăng nhập và sử dụng dịch vụ từ xa vào hệ thống.
- Khi một người dùng từ xa muốn kết nối đến hệ thống thông qua SSH, sshd sẽ nghe (listen) trên cổng mạng SSH (mặc định là cổng 22) và xử lý các yêu cầu kết nối đến từ người dùng, sau đó tiến hành xác thực và cho phép hoặc từ chối kết nối dựa trên thông tin đăng nhập cung cấp.


# Network Time Protocol (NTP)
- **NTP (Network Time Protocol)** trong Linux là một giao thức mạng được sử dụng để đồng bộ hóa thời gian trên các máy tính trong mạng. Đồng bộ hóa thời gian là quan trọng để đảm bảo rằng các máy tính trong mạng hoạt động theo cùng một thời gian chuẩn.
- Trong hệ điều hành Linux, bạn có thể cấu hình NTP bằng cách sử dụng các công cụ và dịch vụ như ntpd hoặc chronyd để quản lý và đồng bộ hóa thời gian.

### Cấu hình NTP với 'ntpd'
- Câu lệnh: `# yum install ntp`
- **Cấu hình NTP**: Sau khi cài đặt, bạn có thể chỉnh sửa tệp cấu hình của ntpd. Tệp cấu hình chính thường là /etc/ntp.conf. Bạn có thể chỉ định các máy chủ NTP khác để đồng bộ thời gian từ chúng.
- Khởi động và kích hoạt dịch vụ NTP: 
	```sh
	systemctl start ntpd
	systemctl enable ntpd
	```
### Cấu hình NTP với `chronyd`
- **Cài đặt chronyd**: `# yum install chrony`
- **Cấu hình chrony**: Chỉnh sửa tệp cấu hình chính /etc/chrony.conf để cấu hình máy chủ NTP.
- **Khởi động và kích hoạt chronyd**:
	```sh
	systemctl start chronyd
	systemctl enable chronyd
	```

