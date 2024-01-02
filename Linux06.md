# Các lệnh cơ bản với hệ thống.
- Lệnh thoát khỏi trạng thái đăng nhập: `# exit`, hoặc `# logout`
## Lệnh khởi động lại hệ thống
- Lệnh **reboot** trong hệ thống Linux được sử dụng để khởi động lại hệ thống máy tính. Dưới đây là một số tùy chọn thường đi kèm với lệnh reboot:
	- reboot: Khởi động lại hệ thống ngay lập tức mà không cần bất kỳ tùy chọn nào khác.
	- reboot -f: Yêu cầu hệ thống khởi động lại ngay lập tức mà không cần đợi các tiến trình hoặc ứng dụng đang chạy lưu trữ dữ liệu của chúng.
	- reboot -h now: Tắt hệ thống ngay lập tức. Tùy chọn này cũng có thể được thực hiện bằng cách sử dụng lệnh halt hoặc poweroff.
	- reboot -t seconds: Cho phép người dùng đặt thời gian trì hoãn trước khi hệ thống khởi động lại (ví dụ: reboot -t 5 sẽ khởi động lại hệ thống sau 5 giây).
	- reboot -d: Chỉ định hệ thống để khởi động lại sau khi hoàn tất kiểm tra quyền truy cập.
## Lệnh hiển thị về các tiến trình đang chạy trên hệ thống. 
- Lệnh `# ps` trong hệ điều hành Unix/Linux được sử dụng để hiển thị thông tin về các tiến trình đang chạy trên hệ thống. Dưới đây là một số tùy chọn thường được sử dụng cùng với lệnh ps:
1. ps: Hiển thị các tiến trình đang chạy của người dùng hiện tại trên terminal hiện tại.
![Imgur](https://i.imgur.com/nrpO38G.png)

Trong đó: 
	- **PID (Process ID)**: ID của tiến trình.
	- **TTY**: Terminal mà tiến trình đang chạy.
	- **TIME**: Thời gian CPU tiêu tốn bởi tiến trình.
	- **CMD**: Tên của lệnh hoặc chương trình.
2. ps -e: Liệt kê tất cả các tiến trình trên hệ thống.

![Imgur](https://i.imgur.com/uiSCWTP.png)

3. ps -ef: Hiển thị thông tin chi tiết về tất cả các tiến trình, bao gồm cả các thông tin về môi trường.
4. ps -aux: Tương tự như ps -ef, nhưng hiển thị một số thông tin thêm về CPU và bộ nhớ (RSS, %CPU, %MEM).
5. ps -u username: Liệt kê các tiến trình của một người dùng cụ thể theo tên người dùng.

## Lệnh được sử dụng để tạm dừng thực thi chương trình trong một khoảng thời gian xác định 
- Lệnh `# sleep <số giây> với <số giây> là thời gian muốn tạm ngừng có thể là số nguyên hoặc số thập phân (tùy chọn), đơn vị là giây.

## Thêm người dùng vào hệ thống
- Sử dụng lệnh: `# useradd <tên_user>`
- Thiết lập mật khẩu cho người dùng: `passwd <tên_user>`
![Imgur](https://i.imgur.com/6SiNdiO.png)
- Sau khi thêm người dùng ta kiểm tra xem trên hệ thống có chưa bằng câu lệnh: `# cat /etc/passwd`
![Imgur](https://i.imgur.com/fc6nwUS.png)

Lệnh này sẽ hiển thị nội dung của tệp /etc/passwd, trong đó chứa thông tin về các người dùng trong hệ thống. Mỗi dòng trong tệp này đại diện cho một người dùng và các thông tin liên quan như tên người dùng, ID người dùng, ID nhóm, thư mục home, shell mặc định, v.v.

## Hiển thị các tiến trình đang chạy
- Lệnh top trong Unix/Linux được sử dụng để hiển thị danh sách các tiến trình đang chạy và thông tin về tài nguyên hệ thống như CPU, bộ nhớ, thời gian hoạt động
- Câu lệnh: `# top`

![Imgur](https://i.imgur.com/1SWGblx.png)

Trong đó: 
	- PID (Process ID): ID của tiến trình, mỗi tiến trình có một PID duy nhất.
	- USER: Người dùng sở hữu tiến trình.
	- PR (Priority): Độ ưu tiên của tiến trình, mức độ ưu tiên này được kernel quản lý.
	- NI (Nice value): Giá trị "nice" của tiến trình, thể hiện mức độ ưu tiên khi sử dụng CPU.
	- VIRT (Virtual memory): Tổng lượng bộ nhớ ảo được sử dụng bởi tiến trình.
	- RES (Resident memory): Lượng bộ nhớ thực sự được sử dụng bởi tiến trình.
	- SHR (Shared memory): Lượng bộ nhớ chia sẻ được sử dụng bởi tiến trình.
	- %CPU (CPU utilization): Phần trăm thời gian CPU sử dụng bởi tiến trình từ lần cuối cùng top cập nhật.
	- %MEM (Memory utilization): Phần trăm bộ nhớ RAM được sử dụng bởi tiến trình.
	- TIME+: Tổng thời gian CPU tiêu tốn bởi tiến trình kể từ khi bắt đầu.
	- COMMAND: Tên của lệnh hoặc chương trình đang chạy.
- Các tùy chọn của lệnh top hay sử dụng: 
1. `-d seconds`: Cập nhật màn hình top mỗi số giây được chỉ định. Ví dụ: top -d 5 để cập nhật mỗi 5 giây.
2. `-c`: Hiển thị tên lệnh hoàn chỉnh, không chỉ hiển thị tên tiến trình. Ví dụ: top -c.
3. `-u username`: Chỉ hiển thị các tiến trình của một người dùng cụ thể. Ví dụ: top -u user.
4. `-p PID`: Hiển thị thông tin chỉ với các tiến trình có PID cụ thể. Ví dụ: top -p 1234,5678.
5. `-n number`: Chỉ định số lượng các vòng lặp trước khi top tự đóng. Ví dụ: top -n 10 để chạy top 10 lần và sau đó thoát.
6. `-H`: Hiển thị các tiến trình con (threads) như là các dòng riêng biệt.
7. `-i`: Không hiển thị các tiến trình không hoạt động.
8. `-o field`: Sắp xếp đầu ra theo trường (field) được chỉ định. Ví dụ: top -o +%CPU để sắp xếp theo CPU sử dụng cao nhất.
9. `-b`: Chạy top ở chế độ batch, cho phép xuất đầu ra thành file.

## Đăng nhập bằng tài khoản khác khi vào hệ thống: 
- Để đăng nhập vào một tài khoản người dùng khác trên hệ điều hành Unix/Linux, ta có thể sử dụng lệnh su hoặc sudo tùy thuộc vào cấu hình và quyền hạn của bạn.
- Sử dụng lệnh **su**: `# su - username`
Điền tên người dùng vào phần username. Nếu không nhập tên người dùng cụ thể, su mặc định sẽ đăng nhập vào tài khoản root.
Sau khi nhập lệnh, hệ thống sẽ yêu cầu bạn nhập mật khẩu của tài khoản người dùng đó.

# Thao tác trên tập tin
## Liệt kê nội dung các thư mục
- Lệnh **ls** trong Unix/Linux được sử dụng để liệt kê nội dung của thư mục hiện tại hoặc một thư mục cụ thể. Dưới đây là một số tùy chọn phổ biến đi kèm với ls:
1. **-l**: Hiển thị danh sách các tệp tin và thư mục dưới dạng danh sách chi tiết, bao gồm thông tin về quyền truy cập, chủ sở hữu, nhóm, kích thước, thời gian sửa đổi và tên tệp tin.

Câu lệnh: `# ls -l`

![Imgur](https://i.imgur.com/tiJUuT1.png)

2. **-a**: Hiển thị tất cả các tệp tin, bao gồm cả các tệp tin ẩn (bắt đầu bằng dấu chấm).

Câu lệnh: `# ls -a`

![Imgur](https://i.imgur.com/x2cRY7l.png)

3. **-h**: Hiển thị kích thước của các tệp tin và thư mục dưới dạng dễ đọc, như "K", "M" cho kilobyte và megabyte.

Câu lệnh: `# ls -h`

4. **-t**: Sắp xếp các tệp tin theo thời gian sửa đổi, hiển thị tệp mới nhất trước.

Câu lệnh: `#ls -t`

5. **-R**: Hiển thị cả nội dung của các thư mục con (đệ quy).

Câu lệnh: `#ls -R`

![Imgur](https://i.imgur.com/Ei1uqEH.png)

## Chuyển thư mục
- **cd /duong/dan/tuyet/doi** : chuyển tới thư mục /doi/
- **cd** : chuyển về thư mục chính của người dùng
- **cd A && ls** : chuyển tới thư mục A và hiện danh sách các file của nó.

![Imgur](https://i.imgur.com/kuci6mS.png)

- **cd -**: chuyển về thư mục đang làm việc trước đó.
- **cd ..** : chuyển về thư mục cha.
- **cd /**: Chuyển đến thư mục gốc (root directory) của hệ thống tệp.

## Tạo thư mục
- Để tạo một thư mục mới trong dòng lệnh có thể sử dụng lệnh mkdir (make directory). 
	- Câu lệnh: `# mkdir <tên_folder>`
- Nếu bạn muốn tạo một thư mục con bên trong thư mục hiện tại, bạn có thể chỉ định đường dẫn tương đối hoặc tuyệt đối

![Imgur](https://i.imgur.com/N4lEvZy.png)

- Nếu bạn muốn tạo nhiều thư mục cùng một lúc, chỉ cần liệt kê chúng sau lệnh mkdir:
	- Câu lệnh: `mkdir folder1 folder2 folder3`

- Các tùy chọn phổ biến: 
1. **-p**: Tạo các thư mục cha nếu chúng chưa tồn tại. Điều này hữu ích khi bạn muốn tạo một thư mục con nhưng thư mục cha của nó chưa tồn tại.
Ví dụ: `# mkdir mkdir -p parent_folder/child_folder/grandchild_folder` sẽ tạo parent_folder, child_folder trong parent_folder, và grandchild_folder trong child_folder nếu chúng không tồn tại.

![Imgur](https://i.imgur.com/G9oF6Kj.png)

2. **-m**: Đặt quyền truy cập cho thư mục được tạo mới.
Ví dụ: `# mkdir -m 775 new_folder`

## Tạo tệp tin 
Để tạo một tệp tin mới trong dòng lệnh Unix/Linux, bạn có thể sử dụng một số lệnh như **touch**, **echo** kết hợp với redirection hoặc **cat** . Dưới đây là một số cách để tạo một tệp tin mới:
- Sử dụng lệnh **touch**:
	- Câu lệnh: `# touch new_file.txt`

- Sử dụng lệnh **cat** kết hợp với **redirection >**:
	- Câu lệnh: `# cat > filename.txt`
Nhập nội dung cho tệp tin và ấn **Ctrl + D** khi hoàn thành việc nhập để lưu tệp

- Sử dụng lệnh **echo** kết hợp với **redirection >**:
	- Câu lệnh: `# echo "Hello, world!" > filename.txt`
Lệnh trên sẽ tạo một tệp tin có tên filename.txt và ghi nội dung "Hello, world!" vào tệp.

- Các tùy chọn hay sử dụng cùng lệnh touch: 
1. **-c**: Nếu tệp tin không tồn tại, không tạo tệp mới. Không thông báo lỗi.
	- Câu lệnh: `# touch -c filename.txt`

2. **-m**: Chỉ cập nhật thời gian sửa đổi của tệp tin, không tạo tệp mới nếu tệp chưa tồn tại.
	- Câu lệnh: `# touch -m filename.txt`
3. **-a**: Chỉ cập nhật thời gian truy cập của tệp tin, không tạo tệp mới nếu tệp chưa tồn tại.
	- Câu lệnh: `# touch -a filename.txt`
4. **touch -d** trong Linux được sử dụng để đặt thời gian truy cập và sửa đổi của một tệp tin hoặc nó có thể được sử dụng để tạo một tệp tin mới với thời gian xác định.
	- Câu lệnh: `# touch -d "2023-01-01 08:00:00" myfile.txt`

## Lệnh xóa tập tin
- Để xóa một tập tin trong Linux, có thể sử dụng lệnh **rm** (remove)
	- Câu lệnh: `# rm filename.txt`

- Nếu bạn muốn xóa nhiều tập tin cùng một lúc, bạn có thể liệt kê chúng:
	- Câu lệnh: rm file1 file2 file3

![Imgur](https://i.imgur.com/FsRo30Q.png)

- Các tùy chọn có thể dùng cùng lệnh **rm**

1. **-f**: `Xóa tập tin` mà không yêu cầu xác nhận từ người dùng. Thường được sử dụng để gỡ bỏ các tệp không thể xóa bình thường hoặc để xóa nhanh chóng mà không cần xác nhận.
	- Câu lệnh: `rm -f filename.txt`
2. **-i**: Yêu cầu xác nhận từ người dùng trước khi xóa mỗi tập tin
	- Câu lệnh: `rm -i filename.txt`

## Lệnh xóa thư mục:
- Để xóa một thư mục ta sử dụng **rmdir**
	- Câu lệnh: `# rmdir my_folder`
Tuy nhiên lệnh này chỉ có thể xóa được những thư mục rỗng. Nếu thư mục chứa các thư mục con lệnh này sẽ không hoạt động

1. **-r, -R** : `Xóa thư mục` và nội dung bên trong nó một cách đệ quy (recursive).
	- Câu lệnh: `# rm -r parent_folder`

![Imgur](https://i.imgur.com/dFc7Us9.png)

2. Nếu muốn xóa nhanh một thư mục mà k cần xác nhận xóa từng thư mục một, ta kết hợp `rm -rf`
	- Câu lệnh: `# rm -rf parent_folder`

![Imgur](https://i.imgur.com/oXV8afv.png)

## Mở tập tin
Để có thể mở các tập tin ta có thể dùng các lệnh sau: 
- Sử dụng lệnh **cat**, nó sẽ hiển thị nội dung trên terminal
	- Câu lệnh:`# cat filename.txt`

![Imgur](https://i.imgur.com/LMri9Hs.png)

Các tùy chọn đi cùng phổ biến với lệnh **cat**
1. **-n**: Hiển thị số dòng trên mỗi dòng.
	- Câu lệnh: `# cat -n filename.txt`

![Imgur](https://i.imgur.com/AAOuypB.png)

2. **-E**: Hiển thị ký tự dấu $ ở cuối mỗi dòng.
	- Câu lệnh: `# cat -E filename.txt`

3. **-A**: Hiển thị tất cả các ký tự điều khiển, bao gồm cả tab và dấu xuống dòng.

	- Câu lệnh: `# cat -A filename.txt`
4. **-b** Hiển thị số dòng cho dòng không trống .
	- Câu lệnh: `# cat -b filename.txt`

![Imgur](https://i.imgur.com/DUepji4.png)

5. **-s**: Kết hợp nhiều dòng trống thành một dòng trống.
	- Câu lệnh: `# cat -s filename.txt`

- Sử dụng lệnh **less* để xem tập tin theo trang về có thể di chuyển qua lại dễ dàng 
	- Câu lệnh: `# less filename.txt`

![Imgur](https://i.imgur.com/HNCfX2v.png)

Cách sử dụng trong **less**:
	- Dùng mũi tên lên xuống để đọc file
	- Muốn di chuyển đến cuối văn bản: **shift g**
	- Muốn chuyển đến đầu văn bản: **g**
	- Nhấn q để thoát 
	- Tìm kiếm: Nhấn **/** và gõ kí tự muốn tìm kiếm, sử dụng **n** để di chuyển đến lần xuất hiện tiếp theo, và **N** để xuất hiện đến lần trước đó. Nếu bạn muốn tìm kiếm từ cuối file lên đầu, bạn có thể sử dụng dấu **?** thay vì **/**, sau đó thực hiện tìm kiếm như thông thường.

Các tùy chọn trong lệnh less:
1. **less filename**: Mở tệp tin để xem nội dung.
2. **less +F filename**: Mở tệp và chuyển sang chế độ theo dõi (tương tự tail -f), đọc tệp tin khi có thêm dữ liệu được thêm vào.
3. **less -N filename**: Hiển thị số dòng trên mỗi dòng.
4. **less -S filename**: Ngăn không cho các dòng quá dài tự động quấn xuống dòng mới.
5. **less -X filename**: Tắt chế độ phím tắt.

- Sử dụng lệnh **more** để xem tập tin 
	- Câu lệnh: `# more filename.txt`

- Sử dụng lệnh **head** để hiện thị phần đầu của tập tin
	- Câu lệnh: `# head filename.txt`
Mặc định lệnh **head** sẽ hiển thị 10 dòng đầu tiên của file, bạn cũng có thể chỉ định số lượng dòng bằng tùy chọn **n**
	- Câu lệnh: `# head -n 15 filename.txt`

- Sử dụng lệnh **tail** để hiện thị phần cuối của tập tin
	- Câu lệnh: `# tail filename.txt`
Mặc định lệnh **tail** sẽ hiển thị 10 dòng cuối cùng.

Cả head và tail cũng có khả năng theo dõi dữ liệu đến khi có thêm thông tin được thêm vào tệp tin bằng cách sử dụng tùy chọn -f (theo dõi, tương tự như tail -f)
	- Câu lệnh: `# tail -f filename.txt`

- Ngoài ra chúng ta có thể sử dụng các trình soạn thảo như ** vi** để đọc dữ liệu. 


