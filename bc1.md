#Chương 1: Giới thiệu về tiến trình
##1-Thuật ngữ. 
####1.1 Process
- Là tiến trình được biên dịch mã nguồn đang chạy trên hệ thống. 
####1.2 PID
- Tất cả các tiến trình đều có một process id or PID
####1.3 PPID
- Mỗi tiến trình có một tiến trình cha (với một PPID). Tiến trình con thường bắt đầu bởi tiến trình 
cha, ngoại trừ tiến trình gốc (PID 1) có thể không có cha, nhưng nó là tiến trình khởi đầu cho hệ
thống.
####1.4 Init
- Tiến trình init luôn luôn có process ID là 1. Tiến trình init được khởi động bởi chính kernal, nên 
về mặt kĩ thuật nó không có tiến trình cha. 
####1.5 Kill
- Khi một tiến trình ngừng chạy, tiến trình đó sẽ chết, khi bạn muốn loại bỏ một tiến trình, bạn sẽ
kill nó. 
- Cú pháp: kill [OPTIONS] PID
####1.6 Deamon
- Các tiến trình **daemon** là các tiến trình trong hệ thống máy tính chạy ở nền và không cần sự
can thiệp của người dùng để khởi động hoặc chạy. Chúng thường được thiết kế để cung cấp các 
dịch vụ, chức năng hệ thống hoặc tiện ích mà không yêu cầu sự tương tác trực tiếp từ người 
dùng.
- Một số tiến trình **daemon** có thể là các dịch vụ như máy chủ web (ví dụ: Apache), máy chủ email 
(ví dụ: Postfix), máy chủ cơ sở dữ liệu (ví dụ: MySQL), hoặc các tiện ích như cron (quản lý lịch 
trình) trong hệ thống Linux.
- Các tiến trình **daemon** thường khởi động cùng với hệ thống và tiếp tục chạy trong suốt thời gian 
hoạt động của hệ thống để cung cấp các dịch vụ hoặc chức năng liên tục mà người dùng có thể
truy cập hoặc sử dụng thông qua các ứng dụng khác.
####1.7 Zombie
- Khi một tiến trình bị kết thúc nhưng vẫn hiển thị trên hệ thống, thì tiến trình đó được gọi là 
**zombie**. Bạn không thể kill các tiến trình zombie vì chúng đã bị xóa.
##2-Quản lý tiến trình cơ bản (basic process management)
####2.1 $$ and $PPID
- Một số biến môi trường shell chứa thông tin về các tiến trình. Biến **$$** sẽ chứa ID tiến trình hiện 
tại của bạn và $PPID chứa PID gốc. Trên thực tế **$$** là tham số shell chứ không phải biến, bạn 
không thể gán giá trị cho nó. 
####2.2 pidof
- Bạn có thể tìm thấy tất cả id của tiến trình theo tên bằng lệnh pidof
- *Lưu ý*: lệnh này cần được chạy với quyền root
####2.3 Tiến trình cha và con
- Các tiến trình có mối quan hệ cha-con. Mỗi tiến trình đều có một tiến trình cha. Khi khởi động 
một bash mới, bạn có thể sử dụng lệnh echo để xác minh rằng PID từ trước đó chính là PPID của 
shell mới. Tiến trình con từ trước đó giờ đây trở thành tiến trình cha.
####2.4 fork and exec
Quá trình khởi động một tiến trình con trong hệ thống Unix/Linux thường diễn ra theo hai bước chính: 
**fork**và **exec**.
Fork:
- Trước hết, quá trình cha tạo một bản sao của chính nó. Điều này được gọi là **fork**. Khi fork xảy 
ra, một bản sao chính xác của quá trình cha được tạo ra, bao gồm toàn bộ bộ nhớ và trạng thái 
của quá trình cha tại thời điểm fork.
Exec:
- Sau khi quá trình con đã được tạo thông qua **fork**, quá trình con sử dụng hàm **exec** để thay thế
bản sao với một chương trình mới hoặc một quá trình con mục tiêu khác. Hàm exec thực hiện 
việc nạp một chương trình mới vào không gian bộ nhớ của quá trình con và thay thế mã máy chủ
yếu để thực thi chương trình mới này.
```sh
[paul@RHEL4b ~]$ echo $$
4224
[paul@RHEL4b ~]$ bash
[paul@RHEL4b ~]$ echo $$ $PPID
5310 4224
```
####2.5 exec
- Với lệnh exec, bạn có thể thực thi một tiến trình mà không cần tạo một tiến trình mới thông qua 
fork.
####2.6 ps
- Công cụ **ps** trong Linux là một công cụ mạnh mẽ để hiển thị thông tin về các tiến trình đang chạy 
trên hệ thống. Nó cung cấp một cách tiếp cận dễ dàng để xem danh sách các tiến trình, thông tin 
chi tiết về các tiến trình này, và các tài nguyên hệ thống mà chúng sử dụng.
- Lệnh: *ps fx*
ps: Là lệnh để hiển thị thông tin về các tiến trình.
f: Là một tùy chọn (option) trong ps để hiển thị thông tin dưới dạng cây (tree) về mối 
quan hệ cha-con giữa các tiến trình. Nó hiển thị các tiến trình theo cấu trúc cây, trong đó 
các tiến trình con được liệt kê dưới tiến trình cha của chúng.
x: Là tùy chọn để hiển thị tất cả các tiến trình không chỉ các tiến trình của người dùng 
hiện tại.
- Ngoài ra lệnh *ps fax* cũng thường được sử dụng 
####2. 7 pgrep
- Lệnh pgrep trong Linux được sử dụng để tìm kiếm và hiển thị các Process ID (PID) dựa trên tên 
của các tiến trình.
*pgrep <tên_tiến_trình>*
- Tương tự như lệnh ps -C
*ps -C <tên_tiến_trình>*
####2.8 top
- top là một công cụ mạnh mẽ trong hệ thống Linux được sử dụng để hiển thị thông tin động về
các tiến trình đang chạy, tài nguyên hệ thống, và thực hiện theo dõi hiệu suất hệ thống trực tiếp.
- Công cụ top có thể sắp xếp các tiến trình theo mức sử dụng CPU hoặc các thuộc tính khác. Bạn 
cũng có thể kết thúc các tiến trình từ bên trong top.
##3-Signalling process
####3.1 kill
- Câu lệnh **kill** sẽ dừng, hoặc xóa một tiến trình
*kill [tùy_chọn] <PID>*
####3.2 list signals
- Các tiến trình đang chạy có thể nhận tín hiệu từ nhau hoặc từ người dùng. Bạn có thể xem danh 
sách các tín hiệu bằng cách gõ lệnh *kill - l*
####3.3kill -1 (SIGHUP)
- Lệnh *kill -1* trên Linux có ý nghĩa gửi tín hiệu **SIGHUP** đến một tiến trình hoặc một nhóm các tiến trình
Khi bạn sử dụng **kill -1 <PID>**, nó gửi tín hiệu SIGHUP đến tiến trình có ID là **<PID>**,
thông thường để yêu cầu tiến trình đó đọc lại cấu hình của nó mà không cần khởi động lại.
- Với kill -1 1, nó gửi tín hiệu SIGHUP đến tiến trình init với PID 1, yêu cầu init đọc lại tệp cấu hình 
của mình mà không cần phải khởi động lại hệ thống.
####3.4 kill -15
- Lệnh **kill -15** trên Linux gửi một tín hiệu SIGTERM đến một tiến trình hoặc một nhóm tiến trình.
Khi bạn sử dụng **kill -15 <PID>**, nó gửi tín hiệu SIGTERM đến tiến trình có ID là **<PID>**, 
thông báo cho tiến trình đó là cần phải dừng lại (terminate)
-Khi một tiến trình nhận được tín hiệu SIGTERM, nó thông thường sẽ chấm dứt hoạt động của mình một cách tự quản lý.
Tiến trình có thể dọn dẹp các tài nguyên, lưu trạng thái hoặc thực hiện các công việc cần thiết trước khi kết thúc.
**SIGTERM** thường được sử dụng trong các trường hợp khi bạn muốn dừng một tiến trình một cách êm dịu, 
cho phép nó kết thúc các tác vụ đang thực hiện và thoát ra một cách kiểm soát hơn so với tín hiệu SIGKILL, 
tín hiệu khác mạnh mẽ hơn và ngay lập tức kết thúc tiến trình mà không cần cho phép tiến trình kết thúc các hoạt động đang thực hiện.
####3.5 kill -9
-Lệnh **kill -9** trên Linux gửi một tín hiệu SIGKILL đến một tiến trình hoặc một nhóm các tiến trình. 
Khi bạn sử dụng **kill -9 <PID>**, nó gửi tín hiệu SIGKILL đến tiến trình có ID là **<PID>**, 
buộc tiến trình đó kết thúc ngay lập tức mà không có cơ hội để xử lý hoặc dọn dẹp gì trước khi kết thúc.
- Tín hiệu **SIGKILL** là một tín hiệu mạnh mẽ và thường được sử dụng khi cần buộc kết thúc một tiến trình mà 
không cần phải xử lý các tài nguyên hoặc lưu trạng thái. Tuy nhiên, điều này cũng có thể gây ra mất mát dữ liệu 
hoặc trạng thái không mong muốn trong các tình huống không được xử lý cẩn thận. 
Do đó, thường khuyến khích sử dụng **SIGTERM** *(kill -15)* trước khi sử dụng **SIGKILL** nếu có thể, 
để cho tiến trình có cơ hội kết thúc một cách kiểm soát hơn.
####3.6 SIGSTOP  và SIGCONT
- **SIGSTOP** (tín hiệu số 19 trên Linux): Khi một tiến trình nhận được tín hiệu này, nó bị tạm dừng (stopped). 
Tiến trình tạm dừng không tiêu tốn CPU và không thực hiện bất kỳ hoạt động nào. 
Nó vẫn nằm trong bộ nhớ và không thể tiếp tục chạy cho đến khi nhận được tín hiệu SIGCONT.
- **SIGCONT** (tín hiệu số 18 trên Linux): Khi một tiến trình bị tạm dừng (stopped) nhận được tín hiệu này, 
nó sẽ tiếp tục hoạt động (continue). Nó cho phép tiến trình bị tạm dừng tiếp tục thực hiện công việc của mình 
từ vị trí nơi nó đã bị tạm dừng.
####3.7 pkill
- Lệnh **pkill** cho phép tìm và kết thúc các tiến trình dựa theo tên