# Cấu hình NIC trên RHEL 

### /etc/sysconfig/network
- Câu lệnh này dùng để hiển thị nội dung của tệp cấu hình mạng. Nó cho phép chúng ta xác định liệu chúng ta muốn có mạng hay không (NETWORKING = yes), hay hiển thị HOSTNAME hoặc GATEWAY.
- Câu lệnh: `# cat /etc/sysconfig/network`

![Imgur](https://i.imgur.com/9lGEYFr.png)

- Thông số **NOZEROCONF** thường được sử dụng trong cấu hình mạng để vô hiệu hóa Zeroconf (Zero Configuration Networking) trên hệ thống. Zeroconf là một bộ công nghệ mạng tự động hóa cho phép các thiết bị trong một mạng cục bộ tự động cấu hình IP, tìm kiếm tài nguyên mạng và giao tiếp với nhau mà không cần phải cấu hình thủ công.

### /etc/sysconfig/network-scripts/ifcfg-
Thư mục **/etc/sysconfig/network-scripts** chứa các tệp cấu hình cho các giao diện mạng trên hệ điều hành Linux, như CentOS hoặc RHEL. Cụ thể, tệp trong thư mục này thường được đặt tên theo tên của giao diện mạng, ví dụ: ifcfg-eth0, ifcfg-enp0s3, ifcfg-wlan0, tùy thuộc vào tên giao diện mạng cụ thể trên hệ thống.

- Câu lệnh: `# /etc/sysconfig/network-scripts/ifcfg-eth0`
- Câu lệnh này cung cấp tệp cấu hình của giao diện mạng eth0, nó bao gồm các thông số như địa chỉ IP, subnet mask, gateway, DNS, và các thông số mạng khác.

![Imgur](https://i.imgur.com/qd5Dqal.png)

- Trong đó: 
	- **DEVICE**: Tên của giao diện mạng (trong trường hợp này, eth0).

	- **BOOTPROTO**: Phương thức khởi động mạng (như dhcp cho DHCP hoặc static cho địa chỉ IP tĩnh).

	- **IPADDR**: Địa chỉ IP của giao diện.

	- **NETMASK**: Subnet mask của địa chỉ IP.

	- **GATEWAY**: Địa chỉ của gateway mạng.

	- **ONBOOT**: Xác định liệu giao diện sẽ được kích hoạt tự động khi hệ thống khởi động (yes hoặc no).

	- **USERCTL**: Xác định người dùng có quyền điều khiển giao diện không

	- **HWADDR**: Địa chỉ MAC của card mạng

### ifup và ifdown
Lệnh **ifup** và **ifdown** là các công cụ dòng lệnh trong hệ điều hành Linux để kích hoạt (ifup) hoặc ngắt kết nối (ifdown) cho các giao diện mạng.

- **ifup**: Lệnh này được sử dụng để kích hoạt một giao diện mạng cụ thể. Khi chạy ifup cùng với tên của giao diện mạng (ví dụ: ifup eth0), nó sẽ cố gắng kích hoạt kết nối cho giao diện đó.

- **ifdown**: Ngược lại, lệnh này được sử dụng để ngắt kết nối cho một giao diện mạng. Khi chạy ifdown cùng với tên giao diện (ví dụ: ifdown eth0), nó sẽ cố gắng ngắt kết nối và tắt giao diện mạng đó.

### ifconfig
- Lệnh **ifconfig** trong hệ điều hành Linux được sử dụng để hiển thị thông tin về các giao diện mạng trên máy tính.Thông qua **ifconfig**, bạn có thể xem các thông tin cơ bản về các giao diện mạng như địa chỉ IP, subnet mask, địa chỉ MAC, số gói tin đã nhận hoặc gửi qua giao diện đó.
- Câu lệnh: `# ifconfig`

![Imgur](https://i.imgur.com/6pSl8cD.png)

- Trong đó: 

	- **inet addr**: Địa chỉ IP của giao diện mạng.
	- **Bcast**: Địa chỉ broadcast của mạng.
	- **Mask**: Subnet mask của địa chỉ IP.
	- **inet6 addr**: Địa chỉ IPv6 của giao diện mạng.
	- **HWaddr**: Địa chỉ MAC (địa chỉ vật lý) của giao diện.
	- **MTU**: Độ lớn gói tin tối đa mà giao diện có thể chuyển.
	- **RX packets và TX packets**: Số lượng gói tin đã nhận và gửi qua giao diện.
	- **RX errors và TX errors**: Số lượng lỗi nhận và gửi qua giao diện.
	- **RX bytes và TX bytes**: Số lượng byte đã nhận và gửi qua giao diện.

Ngoài ra bạn cũng có thể sử dụng ifconfig để xem thông tin về một giao diện mạng cụ thể:
- Câu lệnh: `# ifconfig eth0`

![Imgur](https://i.imgur.com/nT1vD4D.png)

**Ngoài ra** một công cụ phổ biến hơn có chức năng như lệnh **ipconfig** đó là **ip a**
- Câu lệnh: `# ip a`

![Imgur](https://i.imgur.com/HomMWX9.png)

### arp
Lệnh **arp** trong hệ điều hành Linux được sử dụng để hiển thị hoặc thay đổi bảng ARP (Address Resolution Protocol). Bảng ARP là bảng ghi địa chỉ MAC và địa chỉ IP tương ứng của các thiết bị trong mạng cục bộ.

Lệnh **arp** hữu ích trong việc kiểm tra hoạt động mạng, xác định các thiết bị có kết nối với mạng local, và cũng có thể được sử dụng để giải quyết các vấn đề kết nối mạng bằng cách xóa hoặc thêm vào bảng ARP.

- Câu lệnh: `# arp`

![Imgur](https://i.imgur.com/f8Boh5L.png)

- Các tùy chọn phổ biến của lệnh **arp**:

	- **arp -a hoặc arp -n**: Hiển thị bảng ARP, liệt kê các địa chỉ IP và MAC đã được ghi nhận.

	- **arp -d <địa chỉ IP>**: Xóa một mục từ bảng ARP dựa trên địa chỉ IP cụ thể.

	- **arp -s <địa chỉ IP> <địa chỉ MAC>**: Thêm một mục vào bảng ARP với địa chỉ IP và MAC tương ứng.

	- **arp -i <tên giao diện>**: Xác định giao diện mạng cụ thể khi thực hiện thao tác ARP.

	- **arp -v hoặc arp --verbose**: Hiển thị thông tin chi tiết hơn.

	- **arp -n -d <địa chỉ IP>**: Xóa một mục từ bảng ARP mà không cần xác nhận tên miền (sử dụng địa chỉ IP).

	- **arp -e hoặc arp --device** <tên giao diện>: Hiển thị thông tin từ bảng ARP của giao diện cụ thể.

### route
Lệnh **route** trong hệ điều hành Linux được sử dụng để hiển thị hoặc thay đổi bảng định tuyến, cung cấp thông tin về định tuyến mạng và quản lý các route trên hệ thống. 
- Câu lệnh: `# route`

![Imgur](https://i.imgur.com/rKgXZku.png)

Ngoài ra một lệnh mạnh mẽ và hiện đại hơn so với lệnh **route** là lệnh **ip route**
- Câu lệnh:`# ip route`

![Imgur](https://i.imgur.com/lsaEitd.png)

- Giải thích: 
	- **default via 103.159.51.1 dev eth0**: Đây là route mặc định. Nó cho biết rằng mọi gói tin không khớp với bất kỳ route nào khác sẽ được gửi đến gateway có địa chỉ IP là 103.159.51.1 thông qua giao diện mạng eth0.

	- **103.159.51.0/24 dev eth0 proto kernel scope link src 103.159.51.170**: Đây là một route cụ thể. Nó xác định rằng mọi gói tin có địa chỉ đích thuộc vào mạng con 103.159.51.0/24 sẽ được gửi qua giao diện eth0 và địa chỉ nguồn (src) sẽ là 103.159.51.170. Đây là route nội bộ được tạo bởi kernel (proto kernel) và chỉ có tác dụng trong phạm vi nội bộ của hệ thống (scope link).

	- **169.254.169.254 via 103.159.51.11 dev eth0 proto static**: Đây là một route static. Nó xác định rằng gói tin có địa chỉ IP đích là 169.254.169.254 sẽ được gửi đến gateway có địa chỉ IP là 103.159.51.11 thông qua giao diện mạng eth0.

- Các tùy chọn phổ biến:

	- **ip route show hoặc ip route list**: Hiển thị bảng định tuyến, liệt kê các route mạng.

	- **ip route add <địa chỉ mạng> via <địa chỉ gateway>**: Thêm một route vào bảng định tuyến để định tuyến gói tin đến một mạng cụ thể thông qua một gateway.

	- **ip route del <địa chỉ mạng>**: Xóa một route khỏi bảng định tuyến dựa trên địa chỉ mạng.

	- **ip -6 route show hoặc ip -6 route list**: Hiển thị bảng định tuyến IPv6.

	- **ip route flush**: Xóa tất cả các route trong bảng định tuyến.

	- **ip route get <địa chỉ đích>**: Hiển thị route cụ thể mà gói tin sẽ được chuyển đến để đạt được địa chỉ đích đó.

	- **ip route show table <table-name>**: Hiển thị bảng định tuyến cho một bảng cụ thể.


# Network File System (NFS)
Trong Linux, **NFS** là một phần mềm cung cấp khả năng chia sẻ tệp tin và thư mục giữa các máy tính trong một mạng. Đây là cách tuyệt vời để chia sẻ tài nguyên lưu trữ giữa các máy chủ và các máy khách trong mạng nội bộ hoặc qua Internet. NFS cho phép các máy khách truy cập và làm việc trên tệp tin từ xa như chúng được lưu trữ trên máy local.

Lợi ích của NFS:
- **Chia sẻ tập tin và dữ liệu**: NFS cho phép chia sẻ tệp tin và thư mục trên mạng, giúp các máy tính trong mạng truy cập và sử dụng dữ liệu từ máy chủ NFS một cách dễ dàng.

- **Truy cập từ xa và đồng nhất**: Cho phép người dùng truy cập dữ liệu từ xa một cách thuận tiện và đồng nhất. Người dùng có thể truy cập tệp tin từ bất kỳ máy tính nào trong mạng mà không cần phải lưu trữ cục bộ.

- **Tối ưu hiệu suất**: NFS có thể cải thiện hiệu suất truy cập tệp tin trong mạng nội bộ, giúp giảm thời gian truy cập và truyền dữ liệu so với việc sử dụng các phương thức khác như FTP.

- **Quản lý dữ liệu tập trung**: Cho phép quản lý và duy trì tập tin, thư mục tập trung trên máy chủ NFS, giúp dễ dàng thực hiện sao lưu, phục hồi và quản lý dữ liệu.

- **Bảo mật và kiểm soát truy cập**: NFS cung cấp cơ chế kiểm soát truy cập dựa trên quyền hạn, cho phép người quản trị xác định ai có quyền truy cập vào những dữ liệu cụ thể.

- **Tính linh hoạt và mở rộng**: Dễ dàng mở rộng hệ thống bằng cách thêm các máy chủ NFS mới hoặc mở rộng dung lượng lưu trữ mà không gây ảnh hưởng đến sự liên tục của dịch vụ.

**Các cài đặt dịch vụ NFS trên server**
Bước 1: Cài đặt NFS Server
- Câu lệnh: `# yum install nfs-utils`

Bước 2: Xác định thư mục bạn muốn chia sẻ
- Chọn thư mục bạn muốn chia sẻ trên mạng. Ví dụ, thư mục /path/to/your/folder

Bước 3: Cấu hình NFS Server
- Mở file /etc/exports bằng trình soạn thảo văn bản như nano hoặc vi:
	- Câu lệnh: `# vi /etc/exports
- Thêm dòng sau vào cuối file **exports** (thay thế địa chỉ IP hoặc dải IP của client cụ thể và cấp quyền truy cập):
	- `/path/to/your/folder client_IP(rw,sync,no_root_squash)`
- Trong đó: 
	- **/path/to/your/folder** là đường dẫn đến thư mục bạn muốn chia sẻ.
	- **client_IP** là địa chỉ IP hoặc dải IP của máy client được phép truy cập.
	- **rw** cho phép ghi và đọc, **sync** đồng bộ dữ liệu, **no_root_squash** cho phép người dùng root trên client có quyền root trên server.

Bước 4: Khởi động dịch vụ NFS và Firewall
```sh
sudo systemctl enable nfs-server
sudo systemctl start nfs-server
sudo systemctl enable rpcbind
sudo systemctl start rpcbind
sudo systemctl enable nfs-lock
sudo systemctl start nfs-lock
sudo systemctl enable nfs-idmap
sudo systemctl start nfs-idmap
```

# Công cụ khắc phục sự cố
### lsof
**lsof** là một công cụ trong hệ điều hành Unix/Linux, viết tắt của "list open files" (liệt kê các tệp tin đang mở). Nó cho phép người dùng xem danh sách các tệp tin hoặc tài nguyên hệ thống hiện đang được sử dụng hoặc mở bởi các tiến trình đang chạy trên hệ thống.

- Khi được gọi mà không có tùy chọn thì **lsof** sẽ liệt kê tất cả các tệp tin đang mở. 
- Câu lệnh: `# lsof | head `

![Imgur](https://i.imgur.com/XCLRKQz.png)

- Trong đó: 
	- **COMMAND**: Tên của tiến trình hoặc lệnh mà đang sử dụng tài nguyên.

	- **PID**: Process ID, ID của tiến trình mà đang mở tài nguyên.

	- **USER**: Tên người dùng mà tiến trình đó thuộc về.

	- **FD**: File Descriptor, chỉ số của file descriptor đang được sử dụng hoặc kiểu của tài nguyên.

	- **TYPE**: Loại tài nguyên, ví dụ như REG (file), DIR (directory), IPv4 (một kết nối mạng IPv4), và nhiều loại khác.

	- **DEVICE**: Thiết bị hoặc số hiệu inode (iNode number) của tệp tin hoặc tài nguyên.

	- **SIZE/OFF**: Kích thước hoặc vị trí offset của tài nguyên.

	- **NODE**: Số inode của tệp tin hoặc tài nguyên.

	- **NAME**: Tên của tệp tin hoặc tài nguyên.

- Các tùy chọn **lsof** hay sử dụng: 
c <command>: Liệt kê các tệp tin mà các tiến trình của lệnh <command> đang sử dụng.

	- -u <user>: Hiển thị các tệp tin mà người dùng <user> đã mở. Ví dụ:  lsof -u paul | grep home

	- -p <PID>: Liệt kê các tệp tin mà tiến trình có ID là <PID> đang sử dụng.

	- -i: Hiển thị các kết nối mạng mà tiến trình đang sử dụng.

	- -t: Hiển thị thời gian (timestamp) khi tệp tin hoặc tài nguyên được mở.

	- -n: Không resolve địa chỉ IP thành tên máy chủ hoặc tên miền.

	- -a: Hiển thị thông tin chi tiết về các tệp tin (bao gồm cả các tệp mở, tệp đóng, các tệp đã mở từ trước, v.v).

### iostat
**iostat** là một công cụ trong hệ điều hành Linux dùng để theo dõi và hiển thị thông tin về hiệu suất của hệ thống I/O (Input/Output - Nhập/Xuất) như tốc độ đọc/ghi, tình trạng sử dụng các thiết bị lưu trữ (ổ cứng, ổ đĩa SSD, vv) và tình trạng của các bộ đệm.

Khi được chạy mà không có bất kỳ tùy chọn nào, **iostat** sẽ hiển thị thông tin về tốc độ đọc/ghi (ký tự trên giây) cho từng thiết bị lưu trữ trong hệ thống.

- Câu lệnh: `# iostat`

![Imgur](https://i.imgur.com/xiJ8H0m.png)

- Trong đó: 
	- **tps (Transactions per second)**: Số giao dịch hoàn thành trên mỗi giây (số lần đọc hoặc ghi được thực hiện trên thiết bị trong mỗi giây).
	- **kB_read/s**: Tốc độ đọc dữ liệu từ thiết bị (ký tự trên giây).
	- **kB_wrtn/s**: Tốc độ ghi dữ liệu vào thiết bị (ký tự trên giây).
	- **kB_read**: Tổng lượng dữ liệu đã được đọc từ thiết bị (kilobyte).
kB_written: Tổng lượng dữ liệu đã được ghi vào thiết bị (kilobyte).

- Cú pháp có thêm các tùy chọn: `iostat [options] [interval [count]]`
	- **options**: Các tùy chọn để xác định đầu ra cụ thể hoặc chức năng cụ thể.
	- **interval**: Khoảng thời gian giữa các báo cáo (trong giây). Nếu chỉ định, iostat sẽ tạo ra các báo cáo liên tục sau mỗi khoảng thời gian này.
	- **count**: Số lượng báo cáo sẽ được tạo ra trước khi iostat dừng lại. Nếu không chỉ định, nó sẽ tiếp tục tạo báo cáo liên tục.

![Imgur](https://i.imgur.com/mVS5qkN.png)

- Các tùy chọn phổ biến của lệnh **iostat**
	- **-c**: Hiển thị thông tin về sử dụng CPU (tương tự như lệnh mpstat).
	- **-d**: Hiển thị thông tin chi tiết về các thiết bị lưu trữ.
	- **-k**: Hiển thị thông tin theo đơn vị kilobyte (thay vì đơn vị mặc định là byte).
	- **-m**: Hiển thị thông tin theo đơn vị megabyte (thay vì đơn vị mặc định là byte).
	- **-N**: Chỉ định các tên thiết bị lưu trữ cụ thể để theo dõi.

### vmstat
**vmstat** là một công cụ trong hệ thống Linux dùng để hiển thị thông tin về sự sử dụng của bộ nhớ (memory), CPU và swap space. Tên vmstat là viết tắt của "virtual memory statistics". Khi được chạy mà không có tham số, nó hiển thị thông tin tổng quan về sự sử dụng tài nguyên hệ thống.
- Câu lệnh: `vmstat [options] [delay [count]]`
- Trong đó: 
	- **options**: Các tùy chọn để hiển thị thông tin cụ thể (ví dụ: -a, -d, -s).
	- **delay**: Khoảng thời gian giữa các báo cáo (trong giây).
	- **count**: Số lượng báo cáo sẽ được tạo ra trước khi vmstat dừng lại. Nếu không chỉ định, nó sẽ tiếp tục tạo báo cáo liên tục.

- Thông tin chính mà vmstat cung cấp bao gồm:
	- **Procs**: Số lượng tiến trình và thông tin về việc xử lý các tiến trình.
	- **Memory**: Thông tin về sử dụng bộ nhớ và swap.
	- **Swap**: Thông tin về sử dụng không gian swap.
	- **IO**: Thống kê về hoạt động đọc/ghi trên đĩa.
	- **System**: Thông tin về hệ thống và kernel.
	- **CPU**: Thống kê về sử dụng CPU.
	- **r**: Số tiến trình đang chạy (running).
	- **b**: Số tiến trình đang bị chặn (blocked).
	- **swpd**: Số lượng bộ nhớ đã được sử dụng trong phần swap.
	- **free**: Số lượng bộ nhớ không được sử dụng.
	- **buff**: Số lượng bộ nhớ được sử dụng cho các dữ liệu buffer.
	- **cache**: Số lượng bộ nhớ được sử dụng cho cache.
	- **si**: Số lượng dữ liệu được ghi từ RAM vào swap space (swap in).
	- **so**: Số lượng dữ liệu được ghi từ swap space vào RAM (swap out).
	- **bi**: Số lượng block dữ liệu được ghi từ thiết bị đọc vào RAM.
	- **bo**: Số lượng block dữ liệu được ghi từ RAM ra thiết bị.
	- **in**: Số lượng truy cập (interrupts) vào kernel mỗi giây.
	- **cs**: Số lượng context switches (chuyển đổi ngữ cảnh) mỗi giây.
	- **us**: Tỷ lệ thời gian CPU sử dụng cho các tiến trình người dùng.
	- **sy**: Tỷ lệ thời gian CPU sử dụng cho các tiến trình hệ thống.

![Imgur](https://i.imgur.com/Ws0sEkd.png)


# Tìm kiếm bằng grep
Lệnh `grep` trong hệ điều hành Unix/Linux được sử dụng để tìm kiếm các dòng trong tệp tin có chứa các mẫu (patterns) phù hợp với mẫu cụ thể mà bạn định chỉ định.

- Câu lệnh: `# grep [tùy chọn] [mẫu] [tệp...]`
- Trong đó: 
	- **[tùy chọn]**: Là các cờ hoặc tùy chọn để tùy chỉnh việc tìm kiếm, ví dụ -i để tìm kiếm không phân biệt chữ hoa, chữ thường.
	- **[mẫu]**: Là chuỗi hoặc biểu thức chính quy mà bạn muốn tìm kiếm trong tệp tin.
	- **[tệp...]**: Là danh sách các tệp tin hoặc đường dẫn mà bạn muốn tìm kiếm.

- Các tùy chọn phổ biến: 

	- -i: Không phân biệt chữ hoa, chữ thường khi tìm kiếm.
	- -r hoặc --recursive: Tìm kiếm đệ quy trong tất cả các thư mục con.
	- -v hoặc --invert-match: Hiển thị các dòng không chứa mẫu tìm kiếm.
	- -n hoặc --line-number: Hiển thị số dòng của kết quả tìm kiếm.
	- -l hoặc --files-with-matches: Chỉ hiển thị tên tệp tin chứa mẫu tìm kiếm.
	- -E hoặc --extended-regexp: Sử dụng biểu thức chính quy mở rộng (Extended Regular Expressions).
	- -f file hoặc --file=file: Đọc các mẫu tìm kiếm từ tệp tin được chỉ định.
	- -w hoặc --word-regexp: Tìm kiếm chỉ các từ nguyên (whole words) thay vì chuỗi con.
	- -A num hoặc --after-context=num: Hiển thị num dòng văn bản sau mỗi kết quả tìm kiếm.
	- -B num hoặc --before-context=num: Hiển thị num dòng văn bản trước mỗi kết quả tìm kiếm.
	- -C num hoặc --context=num: Hiển thị num dòng văn bản trước và sau mỗi kết quả tìm kiếm.

- Các ví dụ:
	- grep hello file.txt: Tìm kiếm từ "hello" trong tệp tin "file.txt".
	- grep -i hello file.txt: Tìm kiếm từ "hello" mà không phân biệt chữ hoa, chữ thường trong tệp tin "file.txt".
	- grep "error message" *.log: Tìm kiếm chuỗi "error message" trong tất cả các tệp có đuôi là .log trong thư mục hiện tại.

- Cách sử dụng khác:
	- Câu lệnh: `# cat intro.txt | grep -F Michale
	- Hoặc: `# dmesg | grep -n enabled

STDIN, STDOUT, STDERR
**3 lệnh sau có ý nghĩa như nhau:**
- `# grep text file.txt`
- `# cat file.txt | grep text`
- `# grep text < file.txt`

**Những ví dụ khác**
- `# ls > result.txt` ls thư mục hiện tại và ghi kết quả vào file result.txt
- `# ls ff 2> result.txt` vì đây là 1 câu lệnh không đúng lên sẽ ghi kết quả báo lỗi vào file result.txt


# Systemctl
**Systemctl** là một công cụ quản lý dịch vụ (service) trên hệ thống Linux. Nó được sử dụng để kiểm soát các dịch vụ, các quá trình (processes) và các đơn vị (units) của hệ thống init (init system). Systemctl cho phép người dùng thực hiện các hoạt động như khởi động, dừng, khởi động lại, kiểm tra trạng thái của các dịch vụ, cũng như xem logs và quản lý các thành phần khác của hệ thống.

Nó thường được sử dụng để thay thế cho các lệnh cũ như service trên một số bản phân phối Linux mới, như systemd-based Linux distributions (ví dụ: Ubuntu từ phiên bản 15.04 trở đi, CentOS/RHEL từ phiên bản 7 trở đi).

Cú pháp cơ bản khi sử dụng systemctl:

- **Khởi động dịch vụ**: sudo systemctl start <tên_dịch_vụ>
- **Dừng dịch vụ**: sudo systemctl stop <tên_dịch_vụ>
- **Khởi động lại dịch vụ**: sudo systemctl restart <tên_dịch_vụ>
- **Kiểm tra trạng thái của dịch vụ**: sudo systemctl status <tên_dịch_vụ>
- **Bật dịch vụ để khởi chạy cùng hệ thống**: sudo systemctl enable <tên_dịch_vụ>
- **Tắt dịch vụ không khởi chạy cùng hệ thống**: sudo systemctl disable <tên_dịch_vụ>
