# File hệ thống 

Hệ thống tập tin của Linux tổ chức theo cấu trúc phân cấp giống như một cây thư mục. Thư mục gốc (root directory) được biểu diễn bằng dấu gạch chéo (/) và là thư mục cao nhất trong cấu trúc tệp hệ thống.

Từ thư mục gốc, các thư mục và tệp tin khác được tổ chức theo cấu trúc phân cấp. Mỗi thư mục có thể chứa các thư mục con và/hoặc các tệp tin. Đường dẫn tuyệt đối đến một tệp tin hoặc thư mục bắt đầu từ thư mục gốc và liệt kê tất cả các thư mục trung gian trên đường đi.

- **/** (Root Directory): Là thư mục cao nhất trong hệ thống tập tin. Tất cả các thư mục và tệp tin khác đều nằm trong thư mục này.
	- Là điểm xuất phát cho mọi đường dẫn tuyệt đối. 

- **/bin** (Binary): Chứa các tệp lệnh cần thiết cho việc khởi động hệ thống và các lệnh cơ bản cho người dùng thông thường.

- **/boot**: Chứa các tệp liên quan đến quá trình khởi động, bao gồm cả các kernel của hệ điều hành.

- **/dev** (Device): Chứa các tệp đại diện cho các thiết bị phần cứng trên hệ thống.

- **/etc** (Etcetera): Chứa các tệp cấu hình của hệ thống và các ứng dụng.
	- Điều chỉnh hành vi của hệ thống. 
	- Tùy chọn các ứng dụng cụ thể, các quy tắc bảo mật.
	- Ví dụ: /etc/passwd và /etc/shadow: Chứa thông tin về người dùng hệ thống và mật khẩu của họ.
	- etc/network/: Chứa cấu hình mạng như các tập tin liên quan đến địa chỉ IP, DNS, cấu hình giao thức mạng.
	- /etc/apache2/ hoặc /etc/nginx/: Chứa cấu hình của máy chủ web Apache hoặc Nginx.


- **/home**: Thư mục cho cá nhân, nơi mà mỗi người dùng có thể có một thư mục con để lưu trữ dữ liệu và tệp cá nhân của họ.
	- Ví dụ: Có một người dùng tên "user1", thư mục cá nhân của họ sẽ nằm trong /home và được gọi là /home/user1. 

- **/lib** và **/lib64** (Library): Chứa các thư viện thực thi cần thiết cho các chương trình trong /bin và /sbin.
	- **/lib**: Cung cấp chức năng cơ bản và hỗ trợ các lệnh cần thiết để hệ thống hoạt động. 
	- **/lib64**: Chứa thư viện cần thiết nhưng dành riêng cho hệ thống 64bit.

- **/mnt** (Mount): Thư mục dùng để kết nối tạm thời với các thiết bị lưu trữ khác như ổ đĩa USB, ổ cứng di động.
	- Gắn kết các thiết bị lưu trữ từ những vùng lưu trữ khác vào hệ thống tệp tạm thời. Khi các thiết bị này được gắn kết vào **/mnt** , người dùng có thể truy cập và làm việc với dữ liệu trong chúng từ hệ thống tệp của mình.

- **/opt** (Optional): Thư mục dành cho các ứng dụng cài đặt thêm.
	- Lưu trữ các gói phần mềm không thuộc quản lý của hệ thống (như các gói phần mềm cài đặt bằng **apt** trong Ubuntu hoặc **yum** trong CentOS).

- **/proc**: Chứa các tệp tin tham chiếu đến thông tin hệ thống, quản lý bởi kernel.
	- Mỗi thư mục và tệp tin trong **/proc** không phải là tệp tin thực tế được lưu trữ trên đĩa cứng mà là các cơ chế mà kernel Linux cung cấp để truy cập và điều khiển thông tin về hệ thống và các tiến trình. 
	- Thông qua **/proc/** có thể truy cập thông tin hệ thống như tài nguyên phần cứng, thông tin về mạng,...

- **/sbin** (System Binary): Chứa các lệnh dành riêng cho quản trị hệ thống.
	- Các lệnh trong **/sbin** thường cần đặc quyền root để chạy và thường được sử dụng để thực hiện các tác vụ quản lý hệ thống như: **ifconfig**, **route**, **fdisk**, **shutdown**, **reboot**,...
	- Thư mục **/sbin** thường không được thêm vào biến môi trường PATH của người dùng thông thường, điều này nhằm ngăn chặn các lệnh quan trọng của hệ thống được sử dụng bởi người dùng không có quyền root

- **/tmp (Temporary)**: Chứa các tệp tạm thời được tạo bởi các chương trình khi chúng đang hoạt động.
	-  Các tệp tin trong thư mục này thường tồn tại trong thời gian ngắn và có thể bị xóa khi hệ thống khởi động lại.

- **/usr** (Unix System Resources): Chứa nhiều chương trình, thư viện, tài liệu và dữ liệu hỗ trợ cho hệ thống.

- **/var** (Variable): Chứa dữ liệu biến thiên như file log (/var/log), dữ liệu cơ sở dữ liệu, email và các tệp tin cache.

# Hệ thống tập tin

Hệ thống tệp (file system) là cách tổ chức và lưu trữ dữ liệu trên các thiết bị lưu trữ như ổ cứng, ổ đĩa SSD, thẻ nhớ, hoặc bất kỳ thiết bị nào có khả năng lưu trữ dữ liệu. Nó bao gồm cách dữ liệu được tổ chức thành tệp và thư mục, cũng như cách hệ thống truy cập, đọc và ghi dữ liệu trên thiết bị lưu trữ đó.

Trong CentOS, hệ thống tệp mặc định thường là XFS hoặc Ext4.
- **XFS**: Đây là một hệ thống tệp mạnh mẽ, hiệu suất tốt và được thiết kế để xử lý các tệp tin lớn. Nó hỗ trợ dung lượng lớn và có khả năng mở rộng tốt. XFS thường được sử dụng cho các ứng dụng yêu cầu lưu trữ lớn như máy chủ tập tin hoặc máy chủ dữ liệu.
- **Ext4**: Là một phiên bản cải tiến của hệ thống tệp Ext3 truyền thống. Nó cung cấp tính năng mở rộng, hiệu suất tốt và ổn định. Ext4 thường được sử dụng cho các hệ thống thông thường và cần một giải pháp lưu trữ ổn định.

Để sử dụng một tệp hệ thống như Ext4 hoặc XFS, bạn cần thực hiện các bước sau:
1. Tạo Phân Vùng với Hệ Thống Tệp Tương Ứng
- Trước tiên, bạn cần tạo một phân vùng trên ổ đĩa hoặc thiết bị lưu trữ mà bạn muốn sử dụng cho hệ thống tệp. Để làm điều này, bạn có thể sử dụng các công cụ như **fdisk**, **parted** hoặc **gparted** để tạo ra một phân vùng và định dạng nó với Ext4 hoặc XFS.
2. Định Dạng Phân Vùng với Hệ Thống Tệp Tương Ứng
- Định dạng với Ext4: 
	- Câu lệnh: `# mkfs.ext4 /đường_dẫn_đến_phân_vùng`
	- Ví dụ: `# mkfs.ext4 /dev/sda1`

- Định dạng với XFS:
	- Câu lệnh: `# mkfs.xfs /đường_dẫn_đến_phân_vùng`
	- Ví dụ: `# mkfs.xfs /dev/sda1`

3. Gắn kết phân vùng vào hệ thống 
Sau khi định dạng, bạn cần gắn kết phân vùng với một thư mục trên hệ thống của bạn để có thể sử dụng được.
- Câu lệnh: 
```sh
mkdir /mnt/mydata
mount /dev/sda1 /mnt/mydata
```
- Sử dụng lệnh mkdir để tạo thư mục mydata, sau đó mount phân vùng /dev/sda1 vào thư mục mydata để sử dụng. 

# Backup data
Để sao lưu dữ liệu trong Linux, có một số cách thức và công cụ khác nhau bạn có thể sử dụng. 

**rsync** là một công cụ mạnh mẽ trong Linux dùng để sao chép và đồng bộ dữ liệu giữa các thư mục, thư mục cục bộ và từ xa, hoặc giữa các máy chủ khác nhau.
- Câu lệnh: `# rsync [tùy_chọn] nguồn đích
1. Sao chép từ một thư mục đến một thư mục khác trên cùng một máy
- Câu lệnh: `# rsync -av /nguồn /đích`
- Trong đó: 
	- **-a**(archive mode) Chế độ sao lưu theo kiểu archive, bao gồm đồng bộ hóa tất cả các thuộc tính
	- **-v**(verbose) để hiển thị thông tin chi tiết về quá trình sao chép.

![Imgur](https://i.imgur.com/abvHcUG.png)

2. Sao lưu từ một máy đến máy khác thông qua SSH
- Câu lệnh: rsync -avh -e "ssh -i /đường/dẫn/đến/khoá/riêng" /đường/dẫn/nguồn username@địachost:/đường/dẫn/đích
- Trong đó: 
	- **-a**: Chế độ sao lưu theo kiểu archive, bao gồm đồng bộ hóa tất cả các thuộc tính.
	- **-v**: Hiển thị chi tiết khi đang sao chép dữ liệu.
	- **-h**: Hiển thị kích thước dữ liệu ở định dạng dễ đọc.
	- **-e**  "ssh -i /đường/dẫn/đến/khoá/riêng": Sử dụng SSH và cung cấp đường dẫn đến khóa riêng để kết nối.

Các tùy chọn phổ biến của rsync
1. **-v, --verbose**: Hiển thị thông tin chi tiết về quá trình sao chép.

2. **-a, --archive**: Chế độ lưu trữ, bảo tồn các thuộc tính như quyền truy cập, ngày giờ, thư mục, và các thuộc tính khác.

3. **-z, --compress**: Sử dụng nén để giảm kích thước dữ liệu khi truyền qua mạng.

4. **-r, --recursive**: Sao chép các thư mục và tệp tin bên trong các thư mục đó.

5. **-u, --update**: Chỉ sao chép các tệp tin từ nguồn sang đích nếu tệp tin ở nguồn có nội dung mới hoặc tệp tin ở đích không tồn tại.

6. **--exclude**: Loại trừ các tệp tin hoặc thư mục cụ thể từ quá trình sao chép.

7. **--progress**: Hiển thị tiến độ của quá trình sao chép.

8. **-h, --human-readable**: Hiển thị thông tin về kích thước dữ liệu ở dạng dễ đọc cho con người.


# System Information

**THÔNG TIN VỀ PHIÊN BẢN VÀ HĐH**
1. Xem và thay đổi thông tin hostname của hệ thống
- Câu lệnh: `# hostnamectl`
- Lệnh này sẽ hiển thị thông tin chi tiết về tên máy chủ, icon-name, kernel và nhiều thông tin khác.

![Imgur](https://i.imgur.com/Aysc67P.png)

Để thay đổi hostname, bạn có thể dùng **set-hostname**
- Câu lệnh: `# hostnamectl set-hostname new-hostname#

2. Hiển thị phiên bản của Linux
- Câu lệnh: `# cat /etc/*release`
- Lệnh này sẽ đọc và hiển thị nội dung của các tập tin trong thư mục /etc/ có tên chứa thông tin về phiên bản hệ điều hành.

![Imgur](https://i.imgur.com/LxnLFIG.png)

3. Hiển thị thông tin về kernel của hệ thống.
- Để hiển thị những thông tin về kernel của hệ thống ta sử dụng câu lệnh **uname**
- Câu lệnh: `# uname -a`
- Lệnh này sẽ hiển thị tất cả thông tin chi tiết kernel và hệ thống

![Imgur](https://i.imgur.com/TLhK0cY.png)

- Các tùy chọn khác phổ biến của lệnh **uname**
	- **uname -a**: Hiển thị tất cả các thông tin về kernel, bao gồm tên máy chủ, kernel name, version, release, machine, và platform.

	- **uname -s** hoặc **uname --kernel-name**: Chỉ hiển thị tên kernel.

	- **uname -r** hoặc **uname --kernel-release**: Hiển thị phiên bản của kernel.

	- **uname -v** hoặc **uname --kernel-version**: Hiển thị thông tin về phiên bản kernel và các thông tin mô tả khác.

	- **uname -m** hoặc **uname --machine**: Hiển thị thông tin về kiến trúc của máy (như x86_64 cho máy 64-bit).

	- **uname -o** hoặc **uname --operating-system**: Hiển thị tên hệ điều hành.

**THÔNG TIN VỀ PHẦN CỨNG**
1. Hiển thị thông tin về CPU
- Câu lệnh: ` lscpu`

![Imgur](https://i.imgur.com/Bd1LEah.png)

- Trong đó: 
	- Architecture: Kiến trúc của CPU (ví dụ: x86_64).
	- CPU op-mode(s): Chế độ hoạt động của CPU (ví dụ: 32-bit, 64-bit).
	- Byte Order: Thứ tự byte của CPU (ví dụ: Little Endian, Big Endian).
	- CPU(s): Số lượng CPU có sẵn trên hệ thống.
	- Thread(s) per core: Số luồng trên mỗi lõi.
	- Core(s) per socket: Số lõi trên mỗi socket.
	- Socket(s): Số lượng socket CPU trên hệ thống.
	- NUMA node(s): Số lượng NUMA node.
	- Vendor ID: ID của nhà sản xuất CPU.
	- CPU family, model, và stepping: Thông tin chi tiết về gia đình, mô hình và bước của CPU.
	- CPU MHz: Tốc độ xung nhịp của CPU.
	- CPU max MHz, min MHz: Giá trị tối đa và tối thiểu của tốc độ xung nhịp của CPU.
	- CPU flags: Các cờ hỗ trợ bởi CPU như SSE, AVX, ...
	- Virtualization: Hỗ trợ ảo hóa của CPU.
	- L1/L2/L3 cache: Kích thước của bộ nhớ cache.

2. Liệt kê các thông tin về ổ đĩa và phân vùng.
**df** Hiển thị thông tin về không gian đĩa đã sử dụng và còn trống trên các phân vùng đĩa.
- Câu lệnh : `# df -h`

![Imgur](https://i.imgur.com/nIyBYeB.png)

- Trong đó: 
	- **Filesystem**: Tên hệ thống tập tin hoặc đường dẫn đến phân vùng.
	- **Size**: Kích thước tổng của phân vùng.
	- **Used**: Số lượng không gian đã sử dụng.
	- **Available**: Số lượng không gian còn trống.
	- **Use%**: Phần trăm không gian đã sử dụng so với tổng không gian.
	- **Mounted on**: Đường dẫn mà phân vùng được gắn kết (mounted) vào hệ thống tập tin.

- Các tùy chọn phổ biến của lệnh **df**:
	- **-h, --human-readable**: Hiển thị kích thước dễ đọc cho con người (tính bằng MB, GB, ...).
	- **-T, --print-type**: Hiển thị kiểu hệ thống tập tin của các phân vùng.
	- **-a, --all**: Hiển thị thông tin của tất cả các hệ thống tập tin, bao gồm cả các hệ thống tập tin ảo.
	- **-i, --inodes**: Thay vì hiển thị thông tin về không gian đĩa, hiển thị thông tin về số lượng inode đã sử dụng và còn trống trên phân vùng.

	- **--total**: Hiển thị tổng cộng của tất cả các số liệu.


**lsblk**  Liệt kê các thiết bị lưu trữ và các phân vùng trên hệ thống
- Câu lệnh: `# lsblk`

![Imgur](https://i.imgur.com/lwrb24x.png)

- Trong đó:
	- **NAME**: Tên thiết bị hoặc phân vùng.
	- **MAJ:MIN**: Số hiệu (major và minor) của thiết bị.
	- **RM**: Số thứ tự (đối với các thiết bị có thể gỡ ra, như ổ đĩa USB).
	- **SIZE**: Kích thước của thiết bị hoặc phân vùng.
	- **RO**: Chế độ chỉ đọc (Read-Only) - '0' nếu không, '1' nếu có.
	- **TYPE**: Loại thiết bị hoặc phân vùng (disk, part - phân vùng, rom - đĩa CD/DVD).
	- **MOUNTPOINT**: Đường dẫn nơi thiết bị hoặc phân vùng được gắn kết (mounted) vào hệ thống tập tin.

- Các tùy chọn phổ biến với lệnh **lsblk**
	- **-a, --all**: Hiển thị tất cả các thiết bị, bao gồm cả các thiết bị loop và ram.
	- **-d, --nodep**s: Không hiển thị các thiết bị con (các phân vùng của thiết bị).
	- **-o, --output list**: Chỉ định các cột cụ thể để hiển thị (ví dụ: lsblk -o NAME,SIZE,TYPE,MOUNTPOINT).
	- **-p, --pairs**: Hiển thị đầu ra dưới dạng cặp key-value.
	- **-r, --raw**: Hiển thị dữ liệu nguyên thủy mà không sắp xếp cột theo định dạng ASCII.
	- **-S, --scsi**: Hiển thị thông tin với định dạng SCSI.
	- **-t, --fs**: Hiển thị thông tin về hệ thống tập tin trên các phân vùng.
	- **-h, --help**: Hiển thị trợ giúp về các tùy chọn của lệnh.

![Imgur](https://i.imgur.com/mGWuCD4.png)


**fdisk** Đây là các công cụ dùng để quản lý phân vùng đĩa. Bạn có thể sử dụng chúng để xem thông tin chi tiết về các phân vùng.
- Câu lệnh: `# fdisk -l`
- Trong đó: -l để hiển thị thông tin về các ổ đĩa cùng các phân vùng 

![Imgur](https://i.imgur.com/OjxMoUB.png)

- Trong đó: 
	- **Disk /dev/sdX**: Tên thiết bị ổ đĩa (vd: /dev/sda, /dev/nvme0n1).
	- **Disk identifier**: Định danh duy nhất của ổ đĩa.
	- **Device Boot**: Chỉ định xem phân vùng có khả năng khởi động không.
	- **Start**: Địa chỉ bắt đầu của phân vùng (trong sectors).
	- **End**: Địa chỉ kết thúc của phân vùng (trong sectors).
	- **Sectors**: Số lượng sectors của phân vùng.
	- **Size**: Kích thước của phân vùng.
	- **Type**: Kiểu phân vùng (Linux, NTFS, EFI, v.v.).
	- **Id**: Mã định danh kiểu phân vùng (ví dụ: 83 - Linux, 7 - NTFS).
	- **Boot**: Đánh dấu xem phân vùng có thể khởi động hay không.
	- **System**: Hệ thống tập tin của phân vùng (ví dụ: ext4, swap).

3. Hiển thị thông tin về bộ nhớ RAM
- Câu lệnh: `# free -h`

![Imgur](https://i.imgur.com/f3ndaDE.png)

- Trong đó: 
	- **total**: Tổng dung lượng bộ nhớ RAM và swap.
	- **used**: Dung lượng bộ nhớ đã được sử dụng.
	- **free**: Dung lượng bộ nhớ còn trống và chưa được sử dụng.
	- **shared**: Dung lượng bộ nhớ được chia sẻ giữa các tiến trình.
	- **buff/cache**: Dung lượng bộ nhớ được sử dụng cho bộ đệm (buffer) và bộ nhớ cache. Bộ đệm thường chứa dữ liệu đã được đọc từ đĩa, 	- **trong khi** bộ nhớ cache chứa dữ liệu được sử dụng gần đây.
	- **available**: Dung lượng bộ nhớ có sẵn để sử dụng mà không cần phải swap.

- Các tùy chọn phổ biến của lệnh **free**
	**-b, --bytes**: Hiển thị dung lượng bộ nhớ dưới dạng bytes.
	**-k, --kilo**: Hiển thị dung lượng bộ nhớ dưới dạng kilobytes (KB).
	**-m, --mega**: Hiển thị dung lượng bộ nhớ dưới dạng megabytes (MB).
	**-g, --giga**: Hiển thị dung lượng bộ nhớ dưới dạng gigabytes (GB).
	**-h, --human**: Hiển thị dung lượng bộ nhớ dưới dạng dễ đọc cho con người (ví dụ: KB, MB, GB).
	**-t, --total**: Hiển thị tổng cộng của các số liệu.
	**-s, --seconds <delay>**: Hiển thị thông tin về bộ nhớ sau mỗi khoảng thời gian <delay> giây.
	**-c, --count <count>**: Hiển thị thông tin về bộ nhớ theo số lần lặp lại <count>.

![Imgur](https://i.imgur.com/0yDd3Es.png)


**THÔNG TIN VỀ MẠNG**

1. Hiển thi thông tin về địa chỉ IP và giao diện mạng 
- Câu lệnh: `# ip addr show`
- Lệnh này sẽ hiển thị danh sách các giao diện mạng và các địa chỉ gồm: địa chỉ ip, địa chỉ MAC,..

![Imgur](https://i.imgur.com/RwREk3I.png)

2. Kiểm tra kết nội mạng với một địa chỉ ip hoặc tên miền 
- Câu lệnh: `ping <địa_chỉ_tên_miền>`

![Imgur](https://i.imgur.com/OqziDQa.png)

- Tùy chọn phổ biến của lệnh **ping**
	- **-c <số lần>**: Xác định số lượng gói tin để gửi đi trước khi dừng quá trình ping.
	- **-s <kích thước>**: Chỉ định kích thước gói tin được gửi đi (trong byte).
	- **-i <số giây>**: Thiết lập thời gian chờ giữa các gói tin ping.
	- **-w <thời gian>**: Đặt thời gian chờ để nhận phản hồi (timeout).
	- **-q**: Chế độ im lặng, chỉ hiển thị kết quả cuối cùng sau khi hoàn thành.
	- **-v**: Chế độ verbose, hiển thị thông tin chi tiết hơn về quá trình ping.
	- **-t**: Ping liên tục đến khi bị dừng bằng cách sử dụng Ctrl + C.
	- **-f**: Gửi các gói tin ping với cờ "don't fragment".
	- **-n**: Hiển thị kết quả ping với địa chỉ IP (không thử phân giải tên miền).
	- **-R**: Gửi các gói tin ping có chứa thông tin route.

![Imgur](https://i.imgur.com/l6w30lY.png)

**THÔNG TIN VỀ LOG**
1. Xem log của hệ thống
- Câu lệnh: `# journalctl`

![Imgur](https://i.imgur.com/lHF3esU.png)

