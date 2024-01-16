# TÌM HIỂU VỀ DNS SERVER
## Mục Lục
[DNS](#dns)

[DNS là gì](#dns-la-gi)

[DNS hoạt động như thế nào](#dns-hoat-dong-nhu-the-nao)

[Có 4 DNS server liên quan đến việc tải một trang web](#co-4-dns-server-lien-quan-den-viec-tai-mot-trang-web)

[Sự khác biệt giữa authoritative DNS server và recursive DNS resolver](#su-khac-biet-giua-authoritative-dns-server-va-recursive-dns-resolver)

 - [Recursive DNS resolver](#recursive-dns-resolver)
 - [Authoritative DNS server](#authoritative-dns-server)

[Tám bước tra cứu DNS](#tam-buoc-tra-cuu-dns)

[DNS Resolver](#dns-resolver)

[Các loại truy vấn DNS](#cac-loai-truy-van-dns)

[DNS server](#dns-server)

[DNS record](#dns-record)

[Các loại bản ghi DNS phổ biến](#cac-loai-ban-ghi-dns-pho-bien)

[DNS A Record](#dns-a-record)

[DNS CNAME Record](#dns-cname-record)

[DNS MX Record](#dns-record)

[DNS TXT Record](#dns-txt-record)

[DNS NS Record](#dns-ns-record)

[DNS SOA Record](#dns-soa-record)

[DNS glossary](#dns-glossary)

[DNS Zone](#dns-zone)

[Primary vs secondary DNS](#primary-vs-secondary-dns)

[Top level domain](#top-level-domain)


# DNS
## DNS là gì?
- **Hệ Thống Tên Miền (DNS)** là danh bạ của Internet. Con người truy cập thông tin trực tuyến thông qua tên miền, như nytimes.com hoặc espn.com. Trình duyệt web tương tác thông qua địa chỉ IP. DNS chuyển đổi tên miền thành địa chỉ IP để trình duyệt có thể tải tài nguyên trực tuyến.
- Mỗi thiết bị kết nối với Internet đều có một địa chỉ IP duy nhất mà các máy khác sử dụng để tìm thiết bị đó. Các máy chủ DNS loại bỏ nhu cầu cho con người nhớ địa chỉ IP như 192.168.1.1 (trong IPv4) hoặc địa chỉ IP chữ số chữ cái phức tạp hơn như 2400:cb00:2048:1::c629:d7a2 (trong IPv6).

## DNS hoạt động như thế nào?
- Quá trình giải quyết DNS liên quan đến chuyển đổi một tên máy chủ (như www.example.com) thành một địa chỉ IP thân thiện với máy tính (như 192.168.1.1). Mỗi thiết bị trên Internet được cấp một địa chỉ IP duy nhất và địa chỉ đó là cần thiết để tìm thiết bị Internet tương ứng - giống như địa chỉ nhà được sử dụng để tìm một ngôi nhà cụ thể. Khi người dùng muốn tải một trang web, một sự chuyển đổi phải xảy ra giữa những gì người dùng gõ vào trình duyệt web của họ (ví dụ.com) và địa chỉ thân thiện với máy tính cần thiết để định vị trang web example.com.

## Có 4 DNS server liên quan đến việc tải một trang web
- **DNS Recursor** - DNS Recursor có thể được coi như một người thư viện được yêu cầu đi tìm một cuốn sách cụ thể nào đó trong thư viện. DNS Recursor là một máy chủ được thiết kế để nhận các truy vấn từ các máy khách thông qua ứng dụng như trình duyệt web. Thông thường, Recursor sau đó chịu trách nhiệm thực hiện các yêu cầu bổ sung để đáp ứng truy vấn DNS của máy khách.

- **Root Nameserver** - Root Server là bước đầu tiên trong việc chuyển đổi (giải quyết) tên máy chủ dễ đọc của con người thành địa chỉ IP. Nó có thể được coi như một chỉ mục trong một thư viện chỉ đến các kệ sách khác nhau - thường nó phục vụ như một tham chiếu đến các vị trí cụ thể khác.

- **TLD Nameserver** - Máy chủ Top-Level Domain (TLD) có thể được coi như một kệ sách cụ thể trong một thư viện. Máy chủ này là bước tiếp theo trong quá trình tìm kiếm một địa chỉ IP cụ thể và nó chứa phần cuối cùng của một tên máy chủ (trong example.com, máy chủ TLD là "com").

- **Authoritative Nameserver** - Máy chủ cuối cùng này có thể được coi như một từ điển trên một kệ sách, trong đó một tên cụ thể có thể được dịch thành định nghĩa của nó. Máy chủ ủy quyền là điểm dừng cuối cùng trong truy vấn máy chủ DNS. Nếu máy chủ tên uy quyền có quyền truy cập vào bản ghi được yêu cầu, nó sẽ trả lại địa chỉ IP cho tên máy chủ được yêu cầu trở lại cho DNS Recursor (người thư viện) đã thực hiện yêu cầu ban đầu.

## Sự khác biệt giữa authoritative DNS server và recursive DNS resolver
### Recursive DNS resolver
- Máy tính phản hồi một yêu cầu đệ quy từ một máy khách và dành thời gian để theo dõi bản ghi DNS. Điều này được thực hiện thông qua việc thực hiện một loạt các yêu cầu cho đến khi nó đạt được máy chủ DNS ủy quyền cho bản ghi được yêu cầu (hoặc hết thời gian hoặc trả lại một lỗi nếu không tìm thấy bản ghi). Bộ giải quyết DNS đệ quy không luôn cần phải thực hiện nhiều yêu cầu để theo dõi các bản ghi cần thiết để phản hồi cho một máy khách; caching là một quy trình duy trì dữ liệu giúp rút ngắn các yêu cầu cần thiết bằng cách phục vụ bản ghi tài nguyên được yêu cầu trước đó trong quá trình tra cứu DNS.

![Imgur](https://i.imgur.com/s5bgc5D.png)

### Authoritative DNS server
- Một máy chủ DNS ủy quyền là một máy chủ thực sự giữ và chịu trách nhiệm về các bản ghi tài nguyên DNS. Đây là máy chủ ở dưới cùng của chuỗi tra cứu DNS sẽ phản hồi với bản ghi tài nguyên được truy vấn, cuối cùng cho phép trình duyệt web đang thực hiện yêu cầu đạt được địa chỉ IP cần thiết để truy cập một trang web hoặc các nguồn web khác. Một máy chủ DNS ủy quyền có thể đáp ứng các truy vấn từ dữ liệu của mình mà không cần truy vấn nguồn khác, vì nó là nguồn thông tin chính xác cuối cùng cho một số bản ghi DNS cụ thể.

## Tám bước tra cứu DNS

1. Một người dùng nhập 'example.com' vào trình duyệt web và truy vấn đi vào Internet, được nhận bởi một bộ giải quyết DNS đệ quy.

2. Bộ giải quyết sau đó truy vấn một máy chủ tên miền gốc DNS (.).

3. Máy chủ gốc sau đó phản hồi cho bộ giải quyết với địa chỉ của một máy chủ DNS Top Level Domain (TLD) (ví dụ như .com hoặc .net), nơi lưu trữ thông tin cho các miền của nó. Khi tìm kiếm example.com, yêu cầu của chúng ta được chỉ đến TLD .com.

4. Bộ giải quyết sau đó thực hiện một yêu cầu đến TLD .com.

5. Máy chủ TLD sau đó phản hồi với địa chỉ IP của máy chủ tên miền, example.com.

6. Cuối cùng, bộ giải quyết đệ quy gửi một truy vấn đến máy chủ tên miền.

7. Địa chỉ IP cho example.com sau đó được trả về cho bộ giải quyết từ máy chủ tên miền.

8. Bộ giải quyết DNS sau đó phản hồi trình duyệt web với địa chỉ IP của tên miền được yêu cầu ban đầu.

Sau khi 8 bước của tra cứu DNS đã trả về địa chỉ IP cho example.com, trình duyệt có thể thực hiện yêu cầu cho trang web:

9. Trình duyệt gửi một yêu cầu HTTP đến địa chỉ IP.

10. Máy chủ tại địa chỉ IP đó trả lại trang web để hiển thị trong trình duyệt (bước 10).

![Imgur](https://i.imgur.com/wV6JuYa.png)

## DNS Resolver
- Trình phân giải DNS (DNS resolver) là điểm dừng đầu tiên trong quá trình tra cứu DNS và nó chịu trách nhiệm xử lý ứng dụng khách đã đưa ra yêu cầu ban đầu. Trình phân giải bắt đầu chuỗi truy vấn mà cuối cùng dẫn đến việc dịch URL sang địa chỉ IP cần thiết.

Lưu ý: Tra cứu DNS không được lưu vào bộ nhớ đệm thông thường sẽ bao gồm cả truy vấn đệ quy và truy vấn lặp lại.

- Điều quan trọng là phải phân biệt giữa truy vấn DNS đệ quy (recusive DNS query) và trình phân giải DNS đệ quy (recusive DNS resolver). Truy vấn đề cập đến yêu cầu được gửi tới trình phân giải DNS yêu cầu giải quyết truy vấn. Trình phân giải đệ quy DNS là máy tính chấp nhận truy vấn đệ quy và xử lý phản hồi bằng cách thực hiện các yêu cầu cần thiết.

![Imgur](https://i.imgur.com/NtGsRLj.png)

## Các loại truy vấn DNS

## Bộ nhớ đệm DNS (DNS caching)
Mục đích của bộ nhớ đệm là lưu trữ dữ liệu tạm thời ở một vị trí nhằm cải thiện hiệu suất và độ tin cậy cho các yêu cầu dữ liệu. Bộ nhớ đệm DNS liên quan đến việc lưu trữ dữ liệu gần hơn với máy khách yêu cầu để có thể giải quyết truy vấn DNS sớm hơn và có thể tránh được các truy vấn bổ sung trong chuỗi tra cứu DNS, từ đó cải thiện thời gian tải và giảm mức tiêu thụ băng thông/CPU. Dữ liệu DNS có thể được lưu vào bộ đệm ở nhiều vị trí khác nhau, mỗi vị trí sẽ lưu trữ bản ghi DNS trong một khoảng thời gian nhất định được xác định bởi thời gian tồn tại (TTL).

### Bộ đệm DNS của trình duyệt (Brower DNS caching)
Các trình duyệt web hiện đại được thiết kế theo mặc định để lưu trữ các bản ghi DNS trong một khoảng thời gian nhất định. Mục đích ở đây rất rõ ràng; Bộ đệm DNS càng xuất hiện gần trình duyệt web thì càng phải thực hiện ít bước xử lý hơn để kiểm tra bộ đệm và thực hiện các yêu cầu chính xác tới địa chỉ IP. Khi yêu cầu bản ghi DNS được thực hiện, bộ đệm của trình duyệt là vị trí đầu tiên được kiểm tra cho bản ghi được yêu cầu.

### Operating system (OS) level DNS caching (OS level DNS caching)
- Trình phân giải DNS cấp hệ điều hành là điểm dừng cục bộ thứ hai và cuối cùng trước khi truy vấn DNS rời khỏi máy của bạn. Quá trình bên trong hệ điều hành của bạn được thiết kế để xử lý truy vấn này thường được gọi là “trình phân giải sơ khai” hoặc máy khách DNS. Khi trình phân giải sơ khai nhận được yêu cầu từ một ứng dụng, trước tiên nó sẽ kiểm tra bộ đệm của chính nó để xem liệu nó có bản ghi hay không. Nếu không, nó sẽ gửi một truy vấn DNS (với bộ cờ đệ quy), bên ngoài mạng cục bộ tới trình phân giải đệ quy DNS bên trong nhà cung cấp dịch vụ Internet (ISP).

- Khi trình phân giải đệ quy bên trong ISP nhận được một truy vấn DNS, giống như tất cả các bước trước đó, nó cũng sẽ kiểm tra xem liệu bản dịch từ địa chỉ máy chủ sang địa chỉ IP được yêu cầu đã được lưu trữ bên trong lớp lưu trữ cục bộ hay chưa.

- Trình phân giải đệ quy cũng có chức năng bổ sung tùy thuộc vào loại bản ghi có trong bộ đệm của nó:

	- Nếu trình phân giải không có bản ghi A nhưng có bản ghi NS cho máy chủ tên có thẩm quyền thì nó sẽ truy vấn trực tiếp các máy chủ tên đó, bỏ qua một số bước trong truy vấn DNS. Phím tắt này ngăn chặn việc tra cứu từ máy chủ tên gốc và .com (trong tìm kiếm của chúng tôi cho example.com) và giúp quá trình giải quyết truy vấn DNS diễn ra nhanh hơn.
	- Nếu trình phân giải không có bản ghi NS, nó sẽ gửi truy vấn đến máy chủ TLD (.com trong trường hợp của chúng tôi), bỏ qua máy chủ gốc.
	- Trong trường hợp hiếm gặp là trình phân giải không có bản ghi trỏ đến máy chủ TLD, thì nó sẽ truy vấn máy chủ gốc. Sự kiện này thường xảy ra sau khi bộ đệm DNS đã bị xóa.

# DNS server
Hệ thống tên miền (DNS) là danh bạ của Internet. Khi người dùng nhập tên miền như ‘google.com’ hoặc ‘nytimes.com’ vào trình duyệt web, DNS chịu trách nhiệm tìm địa chỉ IP chính xác cho các trang web đó. Sau đó, các trình duyệt sử dụng những địa chỉ đó để liên lạc với máy chủ gốc hoặc máy chủ biên CDN để truy cập thông tin trang web. Tất cả điều này xảy ra nhờ vào máy chủ DNS: máy chuyên trả lời các truy vấn DNS.

# DNS record
- Bản ghi DNS (còn gọi là tệp vùng) là các hướng dẫn tồn tại trong các máy chủ DNS có thẩm quyền và cung cấp thông tin về miền, bao gồm địa chỉ IP nào được liên kết với miền đó và cách xử lý các yêu cầu đối với miền đó. Những bản ghi này bao gồm một loạt các tệp văn bản được viết bằng cú pháp DNS. Cú pháp DNS chỉ là một chuỗi ký tự được sử dụng làm lệnh cho máy chủ DNS biết phải làm gì. Tất cả các bản ghi DNS cũng có 'TTL', viết tắt của thời gian tồn tại và cho biết tần suất máy chủ DNS sẽ làm mới bản ghi đó.

- Bạn có thể coi một tập hợp các bản ghi DNS giống như danh sách doanh nghiệp trên Yelp. Danh sách đó sẽ cung cấp cho bạn nhiều thông tin hữu ích về doanh nghiệp như địa điểm, giờ làm việc, dịch vụ được cung cấp, v.v. Tất cả các tên miền đều phải có ít nhất một vài bản ghi DNS cần thiết để người dùng có thể truy cập trang web của họ bằng cách sử dụng một tên miền và có một số bản ghi tùy chọn phục vụ các mục đích bổ sung.

## Các loại bản ghi DNS phổ biến:
- **Bản ghi** - Bản ghi chứa địa chỉ IP của miền.

- **Bản ghi AAAA** - Bản ghi chứa địa chỉ IPv6 cho một miền (trái ngược với bản ghi A liệt kê địa chỉ IPv4).

- **Bản ghi CNAME** - Chuyển tiếp một tên miền hoặc tên miền phụ sang tên miền khác, KHÔNG cung cấp địa chỉ IP.

- **Bản ghi MX** - Chuyển thư đến máy chủ email. Tìm hiểu thêm về bản ghi MX.

- **Bản ghi TXT** - Cho phép quản trị viên lưu trữ ghi chú văn bản trong bản ghi. Những hồ sơ này thường được sử dụng để bảo mật email. 

- **Bản ghi NS** - Lưu trữ máy chủ tên cho mục nhập DNS. Tìm hiểu thêm về bản ghi NS.

- **Bản ghi SOA** - Lưu trữ thông tin quản trị viên về một miền.

- **Bản ghi SRV** - Chỉ định cổng cho các dịch vụ cụ thể.

- **Bản ghi PTR** - Cung cấp tên miền khi tra cứu ngược.

## DNS A Record
- Chữ "A" là viết tắt của "Address" và đây là loại bản ghi DNS cơ bản nhất: nó cho biết địa chỉ IP của một miền nhất định. Ví dụ: nếu bạn lấy bản ghi DNS của cloudflare.com thì bản ghi A hiện trả về địa chỉ IP là: 104.17.210.9.
- Ví dụ về bản ghi A:

| example.com | record type | value: | TTL |
|-------------|-------------|--------|-----|
| @ | A | 192.0.2.1 | 14400 |

- Ký hiệu **"@"** trong ngữ cảnh này thường được sử dụng để đại diện cho tên miền chính hoặc miền gốc. Do đó, bản ghi này áp dụng cho tên miền gốc của bạn hoặc tên miền chính mà nó đang mô tả.
- **192.168.1.1**: Đây là địa chỉ IPv4 mà tên miền được ánh xạ tới. Trong ví dụ này, tên miền chính hoặc tên miền gốc (được đại diện bởi "@") được ánh xạ đến địa chỉ IPv4 192.168.1.1.
- **TTL 14400**: TTL (Time to Live) là thời gian mà bản ghi DNS này sẽ được lưu trong bộ nhớ cache trước khi cần phải được cập nhật từ nguồn gốc. Giá trị 14400 giây tương ứng với 4 giờ. Sau thời gian này, máy chủ DNS sẽ phải thực hiện một truy vấn mới để kiểm tra xem bản ghi có sự thay đổi hay không.

### BẢn ghi A được sử dụng khi nào?
- Cách sử dụng phổ biến nhất của bản ghi A là tra cứu địa chỉ IP: khớp tên miền (như "cloudflare.com") với địa chỉ IPv4. Điều này cho phép thiết bị của người dùng kết nối và tải một trang web mà không cần người dùng ghi nhớ và nhập địa chỉ IP thực tế. Trình duyệt web của người dùng sẽ tự động thực hiện việc này bằng cách gửi truy vấn đến trình phân giải DNS.

## DNS CNAME Record
- Bản ghi "tên chuẩn" (CNAME) trỏ từ miền bí danh đến miền "chuẩn". Bản ghi CNAME được sử dụng thay cho bản ghi A khi tên miền hoặc tên miền phụ là bí danh của tên miền khác. Tất cả bản ghi CNAME phải trỏ đến một miền, không bao giờ trỏ tới địa chỉ IP.

- Ví dụ: giả sử blog.example.com có bản ghi CNAME có giá trị "example.com" (không có "blog"). Điều này có nghĩa là khi máy chủ DNS truy cập các bản ghi DNS cho blog.example.com, nó thực sự kích hoạt một tra cứu DNS khác cho example.com, trả về địa chỉ IP của example.com thông qua bản ghi A của nó. Trong trường hợp này, chúng tôi sẽ nói rằng example.com là tên chuẩn (hoặc tên thật) của blog.example.com.
- Khi các trang web có tên miền phụ như blog.example.com hoặc shop.example.com, những tên miền phụ đó sẽ có bản ghi CNAME trỏ đến tên miền gốc (example.com). Bằng cách này, nếu địa chỉ IP của máy chủ thay đổi, chỉ bản ghi DNS A cho tên miền gốc cần được cập nhật và tất cả các bản ghi CNAME sẽ tuân theo bất kỳ thay đổi nào được thực hiện đối với tên miền gốc.
- Ví dụ của bản ghi CNAME:

| blog.example.com | record type | value: | TTL |
|-------------|-------------|--------|-----|
| @ | CNAME | is an alias of example.com | 32600 |

Trong ví dụ này, bạn có thể thấy rằng blog.example.com trỏ đến example.com.

### Bản ghi CNAME có thể trỏ tới bản ghi CNAME khác không?
- Việc trỏ bản ghi CNAME vào bản ghi CNAME khác là không hiệu quả vì nó yêu cầu nhiều lần tra cứu DNS trước khi có thể tải miền — điều này làm chậm trải nghiệm người dùng — nhưng điều đó là có thể. Ví dụ: blog.example.com có thể có bản ghi CNAME trỏ đến bản ghi CNAME của www.example.com, sau đó bản ghi này trỏ tới bản ghi A của example.com.

![Imgur](https://i.imgur.com/8qsBpIB.png)

- Cấu hình này bổ sung thêm một bước vào quá trình tra cứu DNS và nên tránh nếu có thể. Thay vào đó, bản ghi CNAME cho cả blog.example.com và www.example.com phải trỏ trực tiếp đến example.com.

### Những hạn chế của việc sử dụng bản ghi CNAME
Bản ghi MX và NS không thể trỏ tới bản ghi CNAME; họ phải trỏ đến bản ghi A (đối với IPv4) hoặc bản ghi AAAA (đối với IPv6). Bản ghi MX là bản ghi trao đổi thư hướng email đến máy chủ thư. Bản ghi NS là bản ghi "máy chủ tên" và cho biết máy chủ DNS nào có thẩm quyền cho tên miền đó.

## DNS MX Record
- Bản ghi 'trao đổi thư' (MX) DNS sẽ chuyển email đến máy chủ thư. Bản ghi MX cho biết cách định tuyến thư email theo Giao thức truyền thư đơn giản (SMTP, giao thức chuẩn cho tất cả email). Giống như bản ghi CNAME, bản ghi MX phải luôn trỏ đến một tên miền khác.
- Ví dụ của bản ghi MX:

![Imgur](https://i.imgur.com/n3NhAtI.png)

- Số 'priority' trước tên miền của các bản ghi MX này biểu thị mức độ ưu tiên; giá trị 'priority' thấp hơn được ưu tiên. Máy chủ sẽ luôn thử mailhost1 trước vì 10 nhỏ hơn 20. Trong trường hợp gửi tin nhắn không thành công, máy chủ sẽ mặc định là mailhost2.

- Dịch vụ email cũng có thể định cấu hình bản ghi MX này để cả hai máy chủ đều có mức độ ưu tiên như nhau và nhận được lượng thư như nhau:

![Imgur](https://i.imgur.com/8KxmeuM.png)

Cấu hình này cho phép nhà cung cấp email cân bằng tải giữa hai máy chủ.

### Quá trình truy vấn bản ghi MX
- Message Tranfer Agent (MTA) chịu trách nhiệm truy vấn các bản ghi MX. Khi người dùng gửi email, MTA sẽ gửi truy vấn DNS để xác định máy chủ thư cho người nhận email. MTA thiết lập kết nối SMTP với các máy chủ thư đó, bắt đầu bằng các miền được ưu tiên (trong ví dụ đầu tiên ở trên, mailhost1).

## DNS TXT Record
- Bản ghi 'văn bản' (TXT) DNS cho phép quản trị viên tên miền nhập văn bản vào Hệ thống tên miền (DNS). Bản ghi TXT ban đầu được dự định là nơi dành cho các ghi chú mà con người có thể đọc được. Tuy nhiên, hiện nay cũng có thể đưa một số dữ liệu máy đọc được vào bản ghi TXT. Một tên miền có thể có nhiều bản ghi TXT.
- Ví dụ bản ghi MX:

![Imgur](https://i.imgur.com/ydUToRk.png)

- Ngày nay, hai trong số những ứng dụng quan trọng nhất đối với bản ghi DNS TXT là ngăn chặn spam email và xác minh quyền sở hữu tên miền, mặc dù ban đầu bản ghi TXT không được thiết kế cho những mục đích sử dụng này.

## DNS NS Record
- NS là viết tắt của 'Nameserver' và bản ghi máy chủ tên cho biết máy chủ DNS nào có thẩm quyền cho tên miền đó (tức là máy chủ nào chứa bản ghi DNS thực tế). Về cơ bản, bản ghi NS cho Internet biết nơi cần tìm để tìm địa chỉ IP của tên miền. Một miền thường có nhiều bản ghi NS có thể chỉ ra máy chủ tên chính và phụ cho miền đó. Nếu không cấu hình đúng bản ghi NS, người dùng sẽ không thể tải trang web hoặc ứng dụng.
- Ví dụ về bản ghi NS:

![Imgur](https://i.imgur.com/O7FcGKv.png)

- **NOTE**: Lưu ý rằng bản ghi NS không bao giờ có thể trỏ tới bản ghi CNAME.

### Nameserver là gì?
- Nameserver là một loại máy chủ DNS. Đây là máy chủ lưu trữ tất cả các bản ghi DNS cho một tên miền, bao gồm bản ghi A, bản ghi MX hoặc bản ghi CNAME.

- Hầu hết tất cả các miền đều dựa vào nhiều nameserver để tăng độ tin cậy: nếu một nameserver ngừng hoạt động hoặc không khả dụng, các truy vấn DNS có thể chuyển sang một nameserver khác. Thông thường có một máy chủ tên chính và một số máy chủ tên phụ lưu trữ các bản sao chính xác của bản ghi DNS trong máy chủ chính. Việc cập nhật máy chủ tên chính cũng sẽ kích hoạt cập nhật máy chủ tên phụ.

- Khi sử dụng nhiều máy chủ tên (như trong hầu hết các trường hợp), bản ghi NS sẽ liệt kê nhiều máy chủ

### Khi nào hồ sơ NS nên được cập nhật hoặc thay đổi?
- Quản trị viên tên miền nên cập nhật bản ghi NS của họ khi họ cần thay đổi máy chủ định danh của tên miền. Ví dụ: một số nhà cung cấp đám mây cung cấp máy chủ tên và yêu cầu khách hàng trỏ tới chúng.

- Quản trị viên cũng có thể muốn cập nhật bản ghi NS của mình nếu họ muốn một tên miền phụ sử dụng các máy chủ tên khác nhau. Trong ví dụ trên, máy chủ tên cho example.com là ns1.exampleserver.com. Thay vào đó, nếu quản trị viên example.com muốn blog.example.com giải quyết thông qua ns2.exampleserver.com thì họ có thể thiết lập điều này bằng cách cập nhật bản ghi NS.

- Khi bản ghi NS được cập nhật, có thể mất vài giờ để các thay đổi được sao chép trên toàn bộ DNS.

## DNS SOA record
- Bản ghi 'start of authority' (SOA) DNS lưu trữ thông tin quan trọng về miền hoặc vùng, chẳng hạn như địa chỉ email của quản trị viên, thời điểm miền được cập nhật lần cuối và máy chủ sẽ đợi bao lâu giữa các lần làm mới.

- Tất cả các vùng DNS đều cần bản ghi SOA để tuân thủ các tiêu chuẩn IETF. Các bản ghi SOA cũng rất quan trọng đối với việc chuyển vùng.

![Imgur](https://i.imgur.com/4WTE3rG.png)

- Trong đó:
	- MNAME: đại diện cho tên miền của máy chủ chính quản lý (Primary Master Server). Nó chỉ định tên miền của máy chủ chính, nơi mà mọi sự thay đổi trên tên miền được thực hiện và nơi mà các bản sao của dữ liệu tên miền được đồng bộ hóa từ.
	- RNAME: đại diện cho địa chỉ email của người quản trị tên miền. Thông số này thường được sử dụng để liên lạc với người quản trị nếu có vấn đề kỹ thuật hoặc thông tin quan trọng về tên miền.
	- SERIAL: Số này được tăng lên mỗi khi có sự thay đổi trên tên miền, và nó giúp xác định phiên bản hiện tại của dữ liệu tên miền.
	- REFRESH: xác định khoảng thời gian mà các máy chủ tên khác nhau nên chờ trước khi truy vấn máy chủ chính để lấy bản sao mới nhất của dữ liệu tên miền. Thông số này được đo bằng giây và ảnh hưởng đến tần suất mà các máy chủ tên cần liên lạc với máy chủ chính để đồng bộ hóa dữ liệu.
	- RETRY:định nghĩa thời gian mà các máy chủ tên khác nhau nên chờ trước khi cố gắng liên lạc lại với máy chủ chính nếu họ không thể kết nối được trong khoảng thời gian "Refresh". Thông số này được đo bằng giây và ảnh hưởng đến tần suất mà các máy chủ tên sẽ thử kết nối lại sau mỗi thời gian Retry.
	- EXPIRE:xác định thời gian tối đa mà dữ liệu tên miền có thể được sử dụng trước khi được coi là không còn hợp lệ. Nếu một máy chủ tên không thể cập nhật dữ liệu từ máy chủ chính trong khoảng thời gian "Expire", nó sẽ không còn được sử dụng để đáp ứng các truy vấn về tên miền đó.(Đo bằng giây)

## DNS PTR Record
Hệ thống tên miền hoặc DNS tương quan tên miền với địa chỉ IP. Bản ghi con trỏ DNS (viết tắt là PTR) cung cấp tên miền được liên kết với địa chỉ IP. Bản ghi DNS PTR hoàn toàn trái ngược với bản ghi 'A', bản ghi này cung cấp địa chỉ IP được liên kết với một tên miền.

Bản ghi DNS PTR được sử dụng trong tra cứu DNS ngược. Khi người dùng cố gắng truy cập một tên miền trong trình duyệt của họ, quá trình tra cứu DNS sẽ diễn ra, khớp tên miền với địa chỉ IP. Tra cứu DNS ngược là quy trình ngược lại với quy trình này: đó là truy vấn bắt đầu bằng địa chỉ IP và tra cứu tên miền.

### Bản ghi DNS PTR được lưu trữ như thế nào?
Trong IPv4:
- Trong khi các bản ghi DNS A được lưu trữ dưới tên miền nhất định, các bản ghi DNS PTR được lưu trữ dưới địa chỉ IP — đảo ngược và được thêm ".in-addr.arpa". Ví dụ: bản ghi PTR cho địa chỉ IP 192.0.2.255 sẽ được lưu trữ trong "255.2.0.192.in-addr.arpa".

- "in-addr.arpa" phải được thêm vì bản ghi PTR được lưu trữ trong miền cấp cao nhất .arpa trong DNS. .arpa là miền được sử dụng chủ yếu để quản lý cơ sở hạ tầng mạng và là tên miền cấp cao nhất đầu tiên được xác định cho Internet. (Tên "arpa" có từ những ngày đầu tiên của Internet: nó lấy tên từ Cơ quan Dự án Nghiên cứu Nâng cao (ARPA), cơ quan đã tạo ra ARPANET, tiền thân quan trọng của Internet.)

- in-addr.arpa là không gian tên trong .arpa để tra cứu DNS ngược trong IPv4.

### Một số ứng dụng chính của bản ghi PTR là gì?
- Bản ghi PTR được sử dụng để tra cứu DNS ngược; cách sử dụng phổ biến cho DNS ngược bao gồm:

- Chống thư rác: Một số bộ lọc chống thư rác email sử dụng DNS ngược để kiểm tra tên miền của địa chỉ email và xem liệu các địa chỉ IP được liên kết có thể được sử dụng bởi các máy chủ email hợp pháp hay không.

- Khắc phục sự cố gửi email: Vì các bộ lọc chống thư rác thực hiện các bước kiểm tra này nên sự cố gửi email có thể xảy ra do bản ghi PTR bị định cấu hình sai hoặc bị thiếu. Nếu một miền không có bản ghi PTR hoặc nếu bản ghi PTR chứa miền không đúng thì dịch vụ email có thể chặn tất cả email từ miền đó.

- Ghi nhật ký: Nhật ký hệ thống thường chỉ ghi lại địa chỉ IP; tra cứu DNS ngược có thể chuyển đổi chúng thành tên miền cho nhật ký dễ đọc hơn.

# DNS Glossary

## DNS Zone
- DNS được chia thành nhiều vùng khác nhau. Các vùng này phân biệt giữa các vùng được quản lý rõ ràng trong không gian tên DNS. Vùng DNS là một phần của không gian tên DNS được quản lý bởi một tổ chức hoặc quản trị viên cụ thể. Vùng DNS là không gian quản trị cho phép kiểm soát chi tiết hơn các thành phần DNS, chẳng hạn như máy chủ tên có thẩm quyền. Không gian tên miền là một cây phân cấp, với tên miền gốc DNS ở trên cùng. Vùng DNS bắt đầu tại một miền trong cây và cũng có thể mở rộng xuống các miền phụ để một thực thể có thể quản lý nhiều miền phụ.

- Một lỗi phổ biến là liên kết vùng DNS với một tên miền hoặc một máy chủ DNS. Trên thực tế, một vùng DNS có thể chứa nhiều tên miền phụ và nhiều vùng có thể tồn tại trên cùng một máy chủ. Các vùng DNS không nhất thiết phải tách biệt về mặt vật lý với nhau, các vùng được sử dụng nghiêm ngặt để phân quyền kiểm soát.

- Ví dụ: hãy tưởng tượng một vùng giả định cho miền cloudflare.com và ba tên miền phụ của nó: support.cloudflare.com, Community.cloudflare.com và blog.cloudflare.com. Giả sử blog là một trang web độc lập, mạnh mẽ cần quản trị riêng nhưng các trang cộng đồng và hỗ trợ được liên kết chặt chẽ hơn với cloudflare.com và có thể được quản lý trong cùng vùng với tên miền chính. Trong trường hợp này, cloudflare.com cũng như các trang hỗ trợ và cộng đồng đều sẽ nằm trong một vùng, trong khi blog.cloudflare.com sẽ tồn tại trong vùng riêng của nó.

![Imgur](https://i.imgur.com/gtyqHKw.png)

### Reverse Lookup Zone
- Reverse lookup zone (vùng tra cứu ngược) chứa ánh xạ từ địa chỉ IP đến máy chủ (chức năng ngược lại của hầu hết các vùng DNS). Các vùng này được sử dụng để khắc phục sự cố, lọc thư rác và phát hiện bot.

### DNS zone file
- Tệp vùng là một tệp văn bản thuần túy được lưu trữ trong máy chủ DNS chứa đại diện thực tế của vùng và chứa tất cả các bản ghi cho mọi miền trong vùng. Các tệp vùng phải luôn bắt đầu bằng bản ghi SOA, chứa thông tin quan trọng bao gồm thông tin liên hệ của quản trị viên vùng.

## Primary vs secondary DNS
### Primary DNS server
- DNS, hay Hệ thống tên miền, dịch tên miền thành địa chỉ IP để người dùng có thể dễ dàng điều hướng đến các trang web trên Internet mà không cần phải ghi nhớ các chuỗi số và chữ cái cụ thể, dài dòng.

- Trong hệ thống này, máy chủ DNS chính là máy chủ lưu trữ tệp vùng chính của trang web. Đây là tệp cơ sở dữ liệu văn bản chứa tất cả thông tin đáng tin cậy cho một tên miền, bao gồm địa chỉ IP, danh tính của quản trị viên tên miền và các bản ghi tài nguyên khác nhau. Bản ghi tài nguyên liệt kê tên miền cùng với địa chỉ IP tương ứng của chúng và có thể có nhiều dạng khác nhau: A record, AAAA record, MX record, NS record. 

- Các máy chủ chính cũng chịu trách nhiệm thực hiện mọi thay đổi cần thiết đối với bản ghi DNS của vùng. Sau khi máy chủ chính hoàn tất cập nhật, nó có thể chuyển các yêu cầu thay đổi đến máy chủ phụ.

### Secondary DNS server

- Máy chủ DNS chính chứa tất cả các bản ghi tài nguyên có liên quan và xử lý các truy vấn DNS cho một miền. Ngược lại, máy chủ DNS thứ cấp chứa các bản sao tệp vùng ở chế độ chỉ đọc, nghĩa là chúng không thể sửa đổi được. Thay vì lấy thông tin từ các tệp cục bộ, họ nhận được thông tin thích hợp từ máy chủ chính trong quy trình liên lạc được gọi là chuyển vùng.

- Việc chuyển vùng trở nên phức tạp hơn khi chúng được hoàn thành giữa nhiều máy chủ phụ. Nếu một số máy chủ phụ đang được sử dụng, một máy chủ có thể được chỉ định là máy chủ phụ cấp cao hơn để nó có khả năng sao chép các bản sao tệp vùng sang nhóm máy chủ phụ còn lại.

### Lợi ích của việc dùng máy chủ phụ
Có hai lợi ích chính của việc sử dụng máy chủ DNS phụ:
- Dự phòng và khả năng phục hồi: Chỉ dựa vào một máy chủ DNS sẽ tạo ra một điểm lỗi duy nhất. Nếu máy chủ chính bị lỗi hoặc bị xâm phạm do một cuộc tấn công, khách truy cập tiềm năng sẽ không thể truy cập vào miền mong muốn nữa. Việc sử dụng máy chủ thứ cấp sẽ tạo ra sự dự phòng và khiến người dùng ít gặp phải tình trạng gián đoạn dịch vụ hơn.
- Cân bằng tải: Máy chủ DNS phụ có thể chia sẻ gánh nặng của các yêu cầu đến miền để máy chủ chính không bị quá tải và gây ra tình trạng từ chối dịch vụ. Họ thực hiện việc này bằng cách sử dụng DNS luân chuyển, một kỹ thuật cân bằng tải được thiết kế để gửi lượng lưu lượng truy cập gần bằng nhau đến mỗi máy chủ.

## Top level domain
Trong hệ thống phân cấp DNS, tên miền cấp cao nhất (TLD) đại diện cho điểm dừng đầu tiên sau vùng gốc. Nói một cách đơn giản hơn, TLD là tất cả những gì nằm sau dấu chấm cuối cùng của tên miền. Ví dụ: trong tên miền ‘google.com’, ‘.com’ là TLD. Một số TLD phổ biến khác bao gồm ‘.org’, ‘.uk’ và ‘.edu’.

TLD đóng vai trò quan trọng trong quá trình tra cứu DNS. Đối với tất cả các yêu cầu không được lưu trong bộ nhớ đệm, khi người dùng nhập tên miền như ‘google.com’ vào cửa sổ trình duyệt của họ, trình phân giải DNS sẽ bắt đầu tìm kiếm bằng cách liên lạc với máy chủ TLD. Trong trường hợp này, TLD là ‘.com’, do đó trình phân giải sẽ liên hệ với máy chủ DNS TLD, sau đó máy chủ này sẽ cung cấp cho trình phân giải địa chỉ IP của máy chủ gốc của Google.

Tập đoàn Internet cấp số và tên miền (ICANN) có thẩm quyền đối với tất cả các TLD được sử dụng trên Internet và ủy quyền trách nhiệm của các TLD này cho các tổ chức khác nhau. Ví dụ: một công ty Hoa Kỳ có tên VeriSign vận hành tất cả các TLD ‘.com’ và ‘.net’.

Một mục đích khác của TLD là giúp phân loại và truyền đạt mục đích của tên miền. Mỗi TLD sẽ cho bạn biết điều gì đó về miền đứng trước nó; Hãy xem một số ví dụ:

'.com' dành cho các doanh nghiệp thương mại.
'.gov' dành cho các tổ chức chính phủ Hoa Kỳ.
'.uk' dành cho các miền từ Vương quốc Anh.
Bản thân TLD cũng được phân loại thành một trong một số nhóm.
