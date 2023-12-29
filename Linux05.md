# Resource monitoring
- Lệnh `free` hiển thị thông tin về bộ nhớ: `# free`
![Imgur](https://i.imgur.com/5VjbJ66.png)

- Lệnh `watch` theo dõi và thực hiện lặp lại một lệnh hoặc một chuỗi lệnh trong khoảng thời gian cố định 
![Imgur](https://i.imgur.com/dEXElFf.png)

- Lệnh `vmstat` xem các thông tin chi tiết về chỉ số quan trọng như như tốc độ CPU, sử dụng bố nhớ swap,...
![Imgur](https://i.imgur.com/flZLblO.png)

- Lệnh `iostat` hiển thị thông tin về sự sử dụng của hệ thống. 
	- Cú pháp cơ bản: iostat [options] [interval] [count]

![Imgur](https://i.imgur.com/7JPaTtE.png)

- Lệnh `mpstat` hiển thị thông tin về sử dụng CPU cho tất cả hoặc từng CPU, core riêng lẻ trên hệ thống
![Imgur](https://i.imgur.com/w4JrQHf.png)

# Packet Management
## Packet terminology
**Repository**
- `Repository` đề cập đến một kho lưu trữ trực tuyến hoặc offline chứa các gói phần mềm đã được đóng gói sẵn để cài đặt và quản lý trên một hệ thống Linux. `Repository` chứa các gói phần mềm, các tệp tin mô tả và các thông tin khác về các ứng dụng, thư viện, hoặc các thành phần hệ thống khác.
**.deb packages**
- Các tệp gói có đuôi `.deb` là định dạng gói dành cho các bản phân phối hệ điều hành Linux như Debian, Ubuntu và các hệ thống dẫn xuất từ Debian. Định dạng này chứa các file được đóng gói, bao gồm mã nguồn, mã thực thi, tệp tin cấu hình, và thông tin khác cần thiết cho việc cài đặt phần mềm trên hệ thống.
**.rpm packages
- Các tệp gói có đuôi .rpm là định dạng gói dành cho các bản phân phối hệ điều hành Linux như Red Hat Enterprise Linux (RHEL), CentOS, Fedora và các hệ thống dựa trên RPM (Red Hat Package Manager). 
- Gói .rpm chứa các file cần thiết để cài đặt phần mềm, bao gồm mã thực thi, tệp tin cấu hình, tài liệu, và các thông tin khác. Các gói .rpm thường được quản lý và cài đặt thông qua các công cụ như rpm và yum hoặc dnf.
**Dependency**
- `Dependency` (phụ thuộc) đề cập đến mối quan hệ giữa các gói phần mềm. Một phụ thuộc là một gói phần mềm cần phải tồn tại trên hệ thống để một gói phần mềm khác có thể hoạt động đúng cách.
- Có hai phụ thuộc chính: 
	- **Phụ thuộc tùy chọn (Optional dependencies)**: Đây là các phần mềm mà không cần thiết cho việc cài đặt hoặc chạy chương trình, nhưng nếu có, nó có thể cải thiện hoặc mở rộng chức năng của nó.
	- **Phụ thuộc bắt buộc (Required dependencies)**: Đây là các phần mềm mà phải có trên hệ thống để chương trình hoạt động đúng cách. Nếu một gói phần mềm không có các phụ thuộc bắt buộc, việc cài đặt hoặc sử dụng chương trình đó có thể gặp sự cố.

## Các lệnh cơ bản với rpm
- Lệnh liệt kê các gói phần mềm đã được cài đặt trên hệ thống: `# rpm -qa`
![Imgur](https://i.imgur.com/vobRWfZ.png)

- Lệnh truy vấn thông tin về một gói cụ thể đã được cài đặt: `# rpm -q`
![Imgur](https://i.imgur.com/FveuDxH.png)

- Lệnh `rpm -Uvh` được sử dụng để nâng cấp (hoặc cài đặt) một gói phần mềm trên hệ thống dựa trên hệ thống quản lý gói RPM (Red Hat Package Manager).
```sh
root@RHELv4u4:~# rpm -Uvh gcc-3.4.6-3
```
- Lệnh gỡ bỏ phần mềm đã được cài đặt: `# rpm -e`

- Thư mục `/var/lib/rpm` trên hệ thống dựa trên RPM chứa cơ sở dữ liệu RPM, nơi thông tin về các gói phần mềm đã cài đặt trên hệ thống được lưu trữ. Thư mục này bao gồm các tệp cơ sở dữ liệu quan trọng cho quản lý gói, bao gồm thông tin về các gói đã cài đặt, tệp tin cấu hình, và các thông tin khác.

## Yum
- `Yum` (Yellowdog Updater Modified) là một công cụ quản lý gói phần mềm trên các hệ thống dựa trên RPM (Red Hat Package Manager) như CentOS, Fedora, và Red Hat Enterprise Linux (RHEL). Yum được sử dụng để quản lý việc cài đặt, cập nhật, xóa và tìm kiếm các gói phần mềm trên hệ thống.
### yum install
- Để cài đặt một ứng dụng, sử dụng `yum install $package`, `yum` sẽ cài đặt tất cả các gói phụ thuộc cần thiết
![Imgur](https://i.imgur.com/PsFGmzE.png)

### yum update
- Để cập nhật tất cả các ứng dụng lên phiên bản mới nhất bằng cách tải xuống và cài đặt chúng, sử dụng lệnh `yum update`. Tất cả phần mềm cài đặt thông qua `yum` sẽ được cập nhật lên phiên bản mới nhất có sẵn trong kho lưu trữ.

### /etc/yum.conf and repositories
- Cấu hình các kho lưu trữ `yum` được thực hiện trong `/etc/yum/yum.conf` và `/etc/yum/repos.d/`.
- Việc cấu hình `yum` chính nó được thực hiện trong `/etc/yum.conf`. Tệp này sẽ chứa địa chỉ của một tệp nhật ký và một thư mục cache cho yum và cũng có thể chứa một danh sách các kho lưu trữ.
- Gần đây, `yum` đã bắt đầu chấp nhận nhiều tệp repo, mỗi tệp chứa một danh sách các kho lưu trữ. Các tệp repo này được đặt trong thư mục `/etc/yum.repos.d/`.
![Imgur](https://i.imgur.com/IdAYEsk.png)

### Practice with yum
- Verify whether gcc, sudo and wesnoth are installed
![Imgur](https://i.imgur.com/jcPZRvV.png)

- Use yum or aptitude to search for and install the scp, tmux, and man-pages packages. 
![Imgur](https://i.imgur.com/zPl7j80.png)

![Imgur](https://i.imgur.com/tNXpASS.png)

![Imgur](https://i.imgur.com/Fwx9ncy.png)

# Network management
## Network layers
- Trong mô hình OSI gồm có 7 tầng: Application, Presentation, Session, Transport, Network, Data link, Physical.
- Tuy nhiên mô hình TCP/IP chỉ gồm 4 tầng: Application, Transport, Internet, Network access
![Imgur](https://i.imgur.com/jxq0nNo.png)

## unicast, multicast, broadcast, anycast
- **Unicast**: Là cách gửi dữ liệu từ một nguồn đến một đích duy nhất, nghĩa là một gói tin được gửi từ một điểm đến một điểm khác. Gói tin Unicast được gửi và nhận giữa một máy chủ và một thiết bị cụ thể trên mạng.

- **Multicast**: Đây là cách gửi dữ liệu từ một nguồn đến một nhóm thiết bị cùng lúc. Gói tin Multicast được gửi từ một nguồn đến nhiều thiết bị đích trong một nhóm được xác định trước. Điều này hữu ích khi bạn muốn gửi dữ liệu đến nhiều người nhận mà không cần phải gửi từng người một cách riêng lẻ.

- **Broadcast**: Là cách gửi dữ liệu từ một nguồn đến tất cả các thiết bị trong mạng. Gói tin Broadcast được gửi từ một nguồn và được nhận bởi tất cả các thiết bị trong mạng.

- **Anycast**: Là cách gửi dữ liệu từ nguồn đến nhiều đích, nhưng chỉ gửi đến đích đầu tiên hoặc đích gần nhất trong một nhóm thiết bị có khả năng xử lý yêu cầu. Điều này giúp tối ưu hóa dịch vụ và tập trung giao tiếp đến đích gần nhất.

## LAN, MAN, WAN
- **LAN (Local Area Network)**: Đây là một mạng máy tính phạm vi nhỏ, bao gồm các thiết bị nằm trong một vùng như trong một văn phòng, một căn hộ, hoặc một tòa nhà. LAN thường có tốc độ truyền dữ liệu nhanh và được quản lý bởi một tổ chức hay cá nhân.

- **MAN (Metropolitan Area Network)**: MAN là một mạng có quy mô lớn hơn so với LAN, bao gồm nhiều vùng LAN lân cận trong một thành phố hoặc khu vực đô thị. MAN thường được sử dụng để kết nối các vị trí văn phòng hoặc cơ sở sản xuất cách nhau trong phạm vi thành phố.

- **WAN (Wide Area Network)**: Đây là một loại mạng có quy mô lớn hơn, kết nối các máy tính và mạng máy tính ở các vị trí xa nhau, thậm chí là trên các khu vực, quốc gia hoặc châu lục khác nhau. Internet là một ví dụ điển hình của WAN, cung cấp kết nối truy cập cho người dùng ở khắp nơi trên thế giới.

## Internet, Intranet, Extranet
- **Internet**: Đây là mạng lưới toàn cầu được kết nối bởi hàng triệu mạng và thiết bị trên khắp thế giới. Internet cho phép truy cập vào các tài nguyên thông tin và dịch vụ trực tuyến, bao gồm trang web, email, trò chuyện trực tuyến, và nhiều ứng dụng khác. Đây là một mạng công cộng và mở, cho phép mọi người truy cập thông tin trên toàn cầu.

- **Intranet**: Là một mạng nội bộ của một tổ chức, công ty hoặc doanh nghiệp. Intranet được xây dựng dựa trên cơ sở hạ tầng mạng và giao thức Internet, nhưng chỉ dành riêng cho nhân viên, thành viên hoặc đối tác của tổ chức. Nó cung cấp các dịch vụ và tài nguyên nội bộ như cơ sở dữ liệu, tài liệu nội bộ, thông tin và ứng dụng nội bộ.

- **Extranet**: Extranet là một phần mở rộng của Intranet, cho phép các bên bên ngoài tổ chức (thường là các đối tác, nhà cung cấp hoặc khách hàng) truy cập vào một phần nhất định của mạng Intranet. Nó cung cấp khả năng chia sẻ thông tin hoặc tài nguyên được ủy quyền cho các bên bên ngoài tổ chức một cách an toàn và kiểm soát.

## TCP/IP protocol
- Giao thức TCP/IP (Transmission Control Protocol/Internet Protocol) là một bộ giao thức được sử dụng rộng rãi trong mạng máy tính để truyền thông dữ liệu giữa các thiết bị trên mạng. Nó bao gồm hai phần chính:
	- TCP (Transmission Control Protocol - Giao Thức Điều Khiển Truyền Tải): TCP là một trong những giao thức chính trong giao thức TCP/IP. Nó cung cấp việc truyền dữ liệu đáng tin cậy qua mạng, đảm bảo rằng dữ liệu được chia thành các gói nhỏ và gửi một cách có thứ tự, đồng thời kiểm tra lỗi và đảm bảo dữ liệu được truyền đến đích một cách đáng tin cậy.
	- IP (Internet Protocol - Giao Thức Internet): IP là một phần khác của giao thức TCP/IP. Nó quản lý việc định tuyến dữ liệu trên mạng, xác định cách dữ liệu được gửi từ điểm này đến điểm khác qua địa chỉ IP, đồng thời chịu trách nhiệm cho việc chia dữ liệu thành các gói tin và định danh các thiết bị trên mạng thông qua địa chỉ IP.

# Interface configuation
- File cấu hình card mạng trên CentOS: `/etc/sysconfig/network-scripts/ifcfg-<interface_name>`
![Imgur](https://i.imgur.com/hRUag5B.png)

- Lệnh hiển thị các interfaces mạng đang hoạt động: `# ifconfig`
![Imgur](https://i.imgur.com/EgVUBeM.png)

- Lệnh ngưng hoạt động một interface mạng cụ thể: `# ifdown eth0`
- Lệnh kích hoạt một interface mạng cụ thể: `# ifup eth0`
- Lệnh hiển thị các interfaces mạng trên hệ thống: `# ip a`
![Imgur](https://i.imgur.com/rg4Qc4M.png)

- Lệnh hiển thị bảng ARP: `# arp -a`

![Imgur](https://i.imgur.com/awCUuq5.png)