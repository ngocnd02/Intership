# Thao tác trên tập tin
## Trình soạn thảo vi
Trình soạn thảo vi là một công cụ mạnh mẽ trong linux. Vi có 2 chế độ làm việc chính 
- 1. **Command Mode (Chế độ lệnh)**: Đây là chế độ mặc định khi bạn mở vi. Trong chế độ này, bạn có thể di chuyển trong file, xóa, sao chép, dán và thực hiện các thao tác chỉnh sửa khác. Bạn cũng có thể chuyển sang chế độ Insert Mode để nhập văn bản mới.
- 2. **Insert Mode (Chế độ chèn)**: Chế độ này cho phép bạn nhập văn bản vào file. Trong chế độ này, bạn có thể nhập và chỉnh sửa văn bản theo cách thức thông thường như các trình soạn thảo văn bản khác.

Để chuyển giữa hai chế độ này:

- **Từ Command Mode sang Insert Mode**: Nhấn phím i để bắt đầu nhập văn bản từ vị trí con trỏ hiện tại.
- **Từ Insert Mode sang Command Mode**: Khi bạn đã hoàn thành việc nhập văn bản, nhấn Esc để trở lại Command Mode.

Cách sử dụng vi
- Câu lệnh: `# vi <tên_file>`, nếu file chưa tồn tại vi sẽ tạo ra một file mới, nếu file đã tồn tại vi sẽ mở file trong trang làm việc
- Trong trình soạn thảo vi ta có thể dùng mũi tên lên xuống để di chuyển giữa các dòng. 
- Nếu ta muốn **copy** bất kì dòng nào, ta di chuyển con trỏ đến dòng đó, sau đó gõ **yy** để copy. Sau đó ta di chuyển con trỏ đến dòng muốn copy, sau đó nhấp **p** để paste.
- Muốn **xóa** một dòng văn bản trong vi, di chuyển trỏ chuyện đến dòng muốn xóa và gõ **dd**. Giả sử sau khi khóa xong ta muốn khôi phục thì ta gõ chữ *u* (undo) để khôi phục.
- Khi chúng ta muốn **tìm kiếm** trên văn bản, gõ kí tự / sau đó gõ kí tự muốn tìm, muốn đi đến kết quả tiếp theo ta gõ chữ n (next).
- Khi chúng ta muốn **thay thế từ** trong văn bản ta gõ `% s/[từ muốn thay thế]/[từ mới để thay thế]/g`. VD: %s/day/thu/g.
- Muốn xem **số thứ tự** dòng văn bản trên vi, gõ : **set nu** ( nu là number), nếu muốn bỏ đánh số thứ tự thì gõ:  **set nonu**

- Để lưu tệp tin và thoát "vi," bạn nhấn phím `Esc` để chắc chắn bạn đang ở chế độ Command Mode. Sau đó, gõ `:wq` và nhấn Enter. "wq" có nghĩa là "write" (lưu) và "quit" (thoát). Nếu bạn chỉ muốn lưu mà không thoát, bạn có thể gõ `:w` và nhấn Enter.
- Để thoát "vi" mà không lưu thay đổi, bạn nhấn phím `Esc` để đảm bảo bạn ở chế độ Command Mode, sau đó gõ `:q!` và nhấn Enter. "q!" có nghĩa là "quit" (thoát) và "force" (buộc thoát).

## Copy file
1. **Sao chép file**
- Câu lệnh: `# cp nguồn đích `

![Imgur](https://i.imgur.com/rOil4xT.png)

2. **Sao chép nhiều file vào một thư mục**
- Câu lệnh: `# cp file1.txt file2.txt /đường/dẫn/mục/đích`

![Imgur](https://i.imgur.com/5nZzBw9.png)

3. **Sao chép thư mục và nội dung bên trong**
- Câu lệnh : `cp -r thư_mục_nguồn /đường/dẫn/mục/đích`
- *Lưu ý*: Tùy chọn -r (hoặc --recursive) là cần thiết khi bạn muốn sao chép toàn bộ cây thư mục và nội dung bên trong.

![Imgur](https://i.imgur.com/fARDdIe.png)

- *Các tùy chọn phổ biến của lệnh `cp`*
1. **-r (hoặc --recursive)**: Được sử dụng để sao chép thư mục và nội dung bên trong của nó. Nếu bạn muốn sao chép toàn bộ cây thư mục, tùy chọn này là cần thiết.

Ví dụ: cp -r /nguồn /đích

2. **-i (hoặc --interactive)**: Yêu cầu xác nhận trước khi ghi đè lên file đích nếu file đích đã tồn tại.

Ví dụ: cp -i file1.txt /đích

![Imgur](https://i.imgur.com/7SthuO4.png)

3. -v (hoặc --verbose): Hiển thị thông báo chi tiết về quá trình sao chép, bao gồm tên của file hoặc thư mục được sao chép.

Ví dụ: cp -v file1.txt /đích

![Imgur](https://i.imgur.com/72hxlsx.png)

4. **-u (hoặc --update)**: Chỉ sao chép file nếu file nguồn mới hơn hoặc không tồn tại trong thư mục đích.

Ví dụ: cp -u file1.txt /đích

5. **-n (hoặc --no-clobber)**: Không ghi đè lên file đích nếu file đích đã tồn tại.

Ví dụ: cp -n file1.txt /đích

6. **-p (hoặc --preserve)**: Giữ nguyên các thuộc tính của file gốc như thời gian sửa đổi, quyền truy cập, ...

Ví dụ: cp -p file1.txt /đích

7. **-a (hoặc --archive)**: Kết hợp các tùy chọn -d, -r, và -p để sao chép các file và thư mục với tất cả các thuộc tính và đệ quy.

Ví dụ: cp -a /nguồn /đích

## So sánh các file
Lệnh **diff** trong Linux được sử dụng để so sánh và tìm ra sự khác biệt giữa hai tập tin hoặc thư mục. Đây là một số cách sử dụng thông dụng của lệnh diff:
1. **So sánh 2 file**:
- Câu lệnh: `# diff file1.txt file2.txt`
- Lệnh này sẽ so sánh hai file file1.txt và file2.txt và hiển thị các dòng có sự khác biệt giữa chúng.

![Imgur](https://i.imgur.com/RwDOm0h.png) 

2. **So sánh nội dung giữa thư mục**
- Câu lệnh: `# diff -r thư_mục_1 thư_mục_2`
- Tùy chọn -r hoặc --recursive sẽ cho phép so sánh đệ quy giữa hai thư mục thư_mục_1 và thư_mục_2. Lệnh này sẽ hiển thị các file hoặc thư mục khác nhau trong cả hai thư mục.

![Imgur](https://i.imgur.com/Pk1D2Nv.png)

3. **Ghi kết quả vào file**
- Câu lệnh: `# diff file1.txt file2.txt > ketqua.diff`
- Dùng dấu > để chuyển kết quả so sánh vào một file mới, ở đây là ketqua.diff.

![Imgur](https://i.imgur.com/W3DoogG.png)

4. **Xem chỉ những dòng khác biệt**
- Câu lệnh: `# diff -u file1.txt file2.txt`
- Tùy chọn -u (hoặc --unified) hiển thị kết quả với định dạng thống nhất và dễ đọc hơn, với thông tin chi tiết về những thay đổi.

5. **Xem thông tin chi tiết về các dòng cụ thể**
- Câu lệnh: `# diff -c file1.txt file2.txt`
- Tùy chọn -c (hoặc --context) cung cấp thông tin chi tiết hơn về những sự khác biệt, bao gồm cả các dòng xung quanh để giúp bạn dễ hiểu hơn về ngữ cảnh của sự thay đổi.

## Xác định kiểu file
-  xác định kiểu file trong Linux, bạn có thể sử dụng lệnh **file**. Lệnh này sẽ cho bạn thông tin về loại file dựa trên nội dung và cấu trúc của file đó

1. **Xác định kiểu file cụ thể**
- Câu lệnh: `# file <tên file>`
2. **Xác định kiểu nhiều file cùng lúc**
- Câu lệnh: `# file file1.txt file2.jpg file3.pdf`

## Nén và giải nén 
Trong Linux, để nén và giải nén các file hoặc thư mục, có thể sử dụng các công cụ như tar, gzip, bzip2, zip, và unzip. Dưới đây là một số cách thực hiện nén và giải nén:
#### Sử dụng tar
Nén 
- Câu lệnh: `# tar -czvf ten_file.tar.gz /duong/dan/thu_muc_hoac_file`
- Lệnh tar sẽ nén toàn bộ nội dung từ thư mục được chỉ định và tạo thành thư mục có tên được đặt với đuôi .tar.gz
Trong đó: 
	- **-c**: Tạo file tar mới.
	- **-z**: Sử dụng gzip để nén.
	- **-v**: Hiển thị thông tin chi tiết khi nén.
	- **-f**: Xác định tên file đầu ra.

![Imgur](https://i.imgur.com/xWCKWRB.png)

- Nén nhiều file hoặc thư mục
	- Câu lệnh: `# tar -czvf ten_file.tar.gz file1 file2 folder1 folder2`
	- Lệnh này sẽ nén file1, file2, folder1, folder2 vào ten_file.tar.gz

![Imgur](https://i.imgur.com/xun7Qp2.png)

- Xem nội dung file nén
	- Câu lệnh: `# tar tar -tzvf filenen.gz.tar | more`
	- **-t** cho biết đang muốn xem nội dung file nén 

![Imgur](https://i.imgur.com/mHGlTwx.png)

Giải nén
- Câu lệnh: `tar -xzvf ten_file.tar.gz`
Trong đó: 
	- **-x**: Giải nén file tar.
	- **-z**: Sử dụng gzip để giải nén.
	- **-v**: Hiển thị thông tin chi tiết khi giải nén.
	- **-f**: Xác định file đầu vào.

#### Sử dụng gzip
Nén
- Câu lệnh: `# gzip ten_file`
- Sẽ tạo ra file nén `ten_file.gz`

![Imgur](https://i.imgur.com/aEDpXt8.png)

- Các tùy chọn phổ biến: 
1. **-f, --force**: Nén mạnh mẽ, ghi đè lên file nén nếu đã tồn tại
Câu lệnh: gzip -f ten_file

2. **-k, --keep**: Giữ file gốc sau khi nén, không xóa file gốc.
Câu lệnh: gzip -k ten_file

3. **gzip -9 ten_file**
Điều chỉnh mức độ nén từ 1-9 (1: nén ít, 9 nén mạnh). Mặc định là 6

Giải nén
- Câu lệnh: `# gzip -d ten_file.gz`


#### Sử dụng bzip2
Nén
- Câu lệnh: `# bzip2 ten_file`
- Sẽ tạo ra file nén `ten_file.bz2`

Kết hợp với tar
- Câu lệnh: `# tar -cjvf ten_file.tar.bz2 /duong/dan/thu_muc_hoac_file`
- Trong đó **-j** là tham số để sử dụng bzip2 để nén file.

Giải nén
- Câu lệnh: `# bzip2 -d ten_file.bz2`

Kết hợp với tar
- Câu lệnh: `# tar -xjvf ten_file.tar.bz2`

#### Sử dụng zip
Nén
- Câu lệnh: `# zip ten_file.zip /duong/dan/thu_muc_hoac_file`

Giải nén
- Câu lệnh: `# unzip ten_file.zip`

# File Permissions
File permissions trong Linux quy định quyền truy cập và điều khiển người dùng, nhóm và các quyền khác liên quan đến file hoặc thư mục. Mỗi file hoặc thư mục có ba loại quyền cơ bản:

1. **Read (đọc - r)**: Cho phép xem nội dung của file hoặc thư mục. Với thư mục, quyền này cho phép đọc danh sách các file và thư mục trong đó.
2. **Write (ghi - w)**: Cho phép chỉnh sửa hoặc viết vào file hoặc thư mục. Với thư mục, quyền này cho phép thay đổi nội dung (tạo, xóa, đổi tên file hoặc thư mục).
3. **Execute (thực thi - x)**: Cho phép thực thi file nếu là file thực thi (executable file), hoặc truy cập vào thư mục để làm việc với nó.

Các quyền này được áp dụng cho ba nhóm người dùng:

1. **Chủ sở hữu (Owner)**: Người dùng mà file hoặc thư mục thuộc về.
2. **Nhóm (Group)**: Nhóm mà file hoặc thư mục thuộc về. Tất cả thành viên trong nhóm này có quyền truy cập như nhau.
3. **Khác (Others)**: Tất cả các người dùng còn lại không thuộc nhóm trên.

Quyền truy cập được hiển thị trong terminal khi sử dụng lệnh `ls -l` và sẽ hiển thị một chuỗi ký tự như `-rwxr-xr--`, trong đó:

- **r** là read (đọc).
- **w** là write (ghi).
- **x** là execute (thực thi).
- **-** có thể là khoảng trống, hoặc là một dấu hiệu không có quyền.

## Thay đổi người và nhóm người sở hữu file

Để thay đổi người và nhóm người sở hữu của một file trong Linux, bạn có thể sử dụng lệnh **chown** để thay đổi người sở hữu và **chgrp** để thay đổi nhóm người sở hữu.

Thay đổi người sở hữu 
- Câu lệnh: `# chown new_owner_name file_name`

![Imgur](https://i.imgur.com/z6j35De.png)

Thay đổi nhóm sở hữu
- Câu lệnh: `# sudo chgrp new_group_name file_name`

![Imgur](https://i.imgur.com/U4iJuoq.png) 

- Cách 2: vẫn sử dụng lệnh chown

![Imgur](https://i.imgur.com/KqiutZO.png)

- Hoặc để thay đổi cả hai: 

![Imgur](https://i.imgur.com/KTT3efe.png) 


## Thay đổi quyền truy cập file 
Để thay đổi quyền truy cập của file trong Linux, bạn sử dụng lệnh **chmod (change mode)**. Lệnh này cho phép bạn thay đổi quyền truy cập theo ba loại quyền cơ bản: đọc (r), ghi (w), và thực thi (x).

Mỗi file được quản lý bởi 3 đối tượng: 
- User onwer: u
- Group onwer: g
- Others: o

Thay đổi quyền truy cập theo ký tự biểu diễn: 
- Phân quyền: 
	- **+**: Thêm quyền.
	- **-**: Loại bỏ quyền.
	- **=**: Đặt quyền chính xác.
- Câu lệnh: `# chmod u+rwx,g+rx,o+r file_name`
Trong đó: 
	- **u+rwx**: Thêm quyền đọc, ghi và thực thi cho người sở hữu.
	- **g+rx**: Thêm quyền đọc và thực thi cho nhóm sở hữu.
	- **o+r**: Thêm quyền đọc cho người dùng khác.

![Imgur](https://i.imgur.com/5MaPM72.png)

Thay đổi quyền truy cập theo số nguyên biểu diễn
- Trong thay đổi quyền theo số, ta cần biết
	- Quyền **read (r)** có giá trị là 4
	- Quyền **write (w)** có giá trị là 2
	- Quyền **execute (x)** có giá trị là 1

- Câu lệnh :`# sudo chmod 755 file_name`
Trong đó: 
	- 7: Quyền đọc, ghi và thực thi cho người sở hữu.
	- 5: Quyền đọc và thực thi cho nhóm sở hữu.
	- 5: Quyền đọc và thực thi cho người dùng khác.

![Imgur](https://i.imgur.com/BGgVurh.png)


Các tùy chọn phổ biến: 
-c ( --changes): Hiển thị thông báo chỉ khi quyền truy cập thực sự được thay đổi.
Ví dụ: chmod -c u+rwx file.txt

-f ( --silent, --quiet): Không hiển thị thông báo lỗi khi có vấn đề xảy ra.
Ví dụ: chmod -f u+rwx file.txt

-v ( --verbose): Hiển thị thông báo chi tiết cho mỗi file được thay đổi quyền truy cập.
Ví dụ: chmod -v u+rwx file.txt



