# Tổng quan về chia mạng con IPv4
## Định nghĩa mạng con
- Một mạng con IP đơn giản chỉ là một phần của một mạng Class A, B hoặc C. Trong thực tế, thuật ngữ **"subnet"** là một phiên bản rút gọn của cụm từ **"subdivided network"** (mạng đã được phân chia). Ví dụ, một subnet của mạng Class B 172.16.0.0 có thể là tập hợp của tất cả các địa chỉ IP bắt đầu bằng 172.16.1 và sẽ bao gồm 172.16.1.0, 172.16.1.1, 172.16.1.2 và tiếp tục cho đến 172.16.1.255. Một subnet khác của cùng mạng Class B đó có thể là tất cả các địa chỉ bắt đầu bằng 172.16.2.

![Imgur](https://i.imgur.com/TBlFLrD.png)

## Phân tích mạng con và giải quyết nhu cầu.
### Quy tắc về máy chủ nào thuộc mạng con nào
Các địa chỉ IP phải được gán theo một số quy tắc cơ bản—và với những lý do hợp lý. Để làm cho quá trình định tuyến hoạt động hiệu quả, các quy tắc địa chỉ IP nhóm các địa chỉ thành các nhóm gọi là **subnets** (mạng con). Những quy tắc là như sau:
- Các địa chỉ trong cùng một mạng con không được tách biệt bởi một router.
- Các địa chỉ ở các mạng con khác nhau được tách biệt bởi ít nhất một router. 

![Imgur](https://i.imgur.com/lFQV6Em.png)

## Đưa ra lựa chọn thiết kế.
### Chose a Classful Network
#### Public IP Network
**Đặc điểm**:
- Là các mạng IP được đăng ký và quản lý toàn cầu bởi các tổ chức như ARIN (American Registry for Internet Numbers), RIPE (Réseaux IP Européens), APNIC (Asia-Pacific Network Information Centre), và các tổ chức quản lý IP khác.
- Các địa chỉ IP trong mạng này là duy nhất và có thể truy cập trực tiếp từ Internet.
- Được sử dụng để kết nối các thiết bị và máy tính trực tiếp với Internet.

Ví dụ:
- Địa chỉ IP công cộng có thể là các địa chỉ như 203.0.113.0, 8.8.8.8 (Google DNS),...

#### Growth Exhausts the Public IP Address Space
- Với sự phổ biến của các thiết bị kết nối, bao gồm máy tính, điện thoại thông minh, máy tính bảng, thiết bị IoT (Internet of Things), và nhiều hơn nữa, nhu cầu về địa chỉ IP đã vượt qua nguồn cung có sẵn. Sự cạn kiệt địa chỉ IP công cộng IPv4 này đặt ra một thách thức, khi các tổ chức và các nhà cung cấp dịch vụ Internet (ISP) đang đối mặt khó khăn trong việc cấp phát địa chỉ duy nhất cho các thiết bị mới.
- Để giải quyết vấn đề này 
	- Một phiên bản IP mới (IPv6), với giải địa chỉ lớn hơn (128 bit)
	- Phân chia một phần của mạng IP công cộng cho mỗi công ty, thay vì toàn bộ mạng IP công cộng, để giảm lãng phí, sử dụng một tính năng được gọi là 'Classless Interdomain Routing' (CIDR)
	- Network Address Translation (NAT), cho phép sử dụng private IP networks.

#### Private IP Network
**Đặc điểm**:
- Là các mạng IP được sử dụng nội bộ trong các tổ chức, doanh nghiệp, hoặc mạng cá nhân.
- Các địa chỉ IP trong mạng này thường được sử dụng trong mạng nội bộ và không trực tiếp truy cập từ Internet.
- Có một số dãy địa chỉ IP đã được quy định để sử dụng riêng tư, như dãy A: 10.0.0.0 - 10.255.255.255, dãy B: 172.16.0.0 - 172.31.255.255, và dãy C: 192.168.0.0 - 192.168.255.255.
**Ví dụ**:
- Địa chỉ IP riêng tư có thể là 10.0.0.1, 192.168.1.1, 172.16.0.2,...

### Chose The Mask
#### Classful IP Networks Before Subnetting
- Khi nghĩ về một mạng lớp chưa được chia, các địa chỉ trong mạng chỉ có hai phần: phần mạng và phần máy chủ. 

![Imgur](https://i.imgur.com/yPiflJy.png)

- N và H lần lượt đại diện cho số bit mạng và và số bit host
- Số lượng địa chỉ trong một mạng IP lớp có thể được tính bằng công thức 2H – 2. Cụ thể, kích thước của một mạng lớp A, B hoặc C chưa được chia là như sau: 
	- Class A: 2^24 – 2 = 16,777,214
	- Class B: 2^16 – 2 = 65,534
	- Class C: 2^8 – 2 = 25

#### Borrowing Host Bits to Create Subnet Bits (Mượn các bit máy chủ để tạo các bit mạng con)
- Để chia mạng con, người thiết kế xem xét phần mạng và phần máy chủ, như thể hiện trong hình dưới đây, và sau đó thêm một phần thứ ba ở giữa:the subnet part (phần mạng con). Tuy nhiên, người thiết kế không thể thay đổi kích thước của phần mạng hoặc kích thước của toàn bộ địa chỉ (32 bit). Để tạo một phần mạng con trong cấu trúc địa chỉ, phải mượn các bit từ phần máy chủ.

![Imgur](https://i.imgur.com/KKfVm5s.png)

#### Choosing Enough Subnet and Host Bits (Lựa chọn đủ bit mạng con và bit máy chủ)

![Imgur](https://i.imgur.com/SjA38yT.png)

#### Example Design: 172.16.0.0, 200 Subnets, 200 Hosts
Để chọn **the mask**, người thiết kế mạng cần hỏi những câu hỏi sau: 
**Cần bao nhiêu bit subnet (mạng con) để tạo ra 200 mạng con**
- Bạn có thể thấy rằng nếu s=7 thì không đủ lớn (2^7=128), nhưng S=8 thì đủ (2^8=256). Như vậy ta cần ít nhất 8 bit subnet.

**Cần bao nhiêu bit máy chủ để có đủ 200 host cho mỗi subnet.
- Bạn có thể thấy rằng H = 7 không đủ lớn (2^7 – 2 = 126), nhưng H = 8 là đủ (2^8 – 2 = 254).

![Imgur](https://i.imgur.com/mccWbZV.png)
