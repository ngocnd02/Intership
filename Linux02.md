## Process priorities
#### renice
- Trong hệ thống Linux, lệnh renice được sử dụng để thay đổi độ ưu tiên của tiến trình đã tồn tại. Điều này cho phép bạn điều chỉnh cách hệ thống ưu tiên việc phục vụ các tiến trình, tăng hoặc giảm ưu tiên của chúng đối với tài nguyên hệ thống như CPU.
#### nice value
- **nice value** (giá trị nice) là một cách để xác định độ ưu tiên của một tiến trình đối với việc sử dụng CPU. Nó đo lường mức độ ưu tiên mà một tiến trình được cấp phép để sử dụng tài nguyên CPU so với các tiến trình khác.
- Giá trị nice nằm trong khoảng từ -20 đến +19. Càng thấp giá trị nice, tiến trình đó càng được ưu tiên cao hơn trong việc sử dụng CPU. 
## Background processes
#### jobs
- Lệnh jobs trong môi trường dòng lệnh Linux/Unix được sử dụng để liệt kê các tiến trình nền (background jobs) đang chạy trong phiên làm việc hiện tại của terminal.
- Khi bạn chạy một tiến trình trong chế độ nền (ví dụ: bằng cách thêm & vào cuối lệnh), nó sẽ chạy dưới dạng tiến trình nền. Lệnh jobs sẽ hiển thị danh sách các tiến trình này cùng với số thứ tự job và trạng thái của chúng (đang chạy hoặc đã dừng).
#### jobs -p
- Hiển thị các process id (PID) của các tiến trình đang chạy dưới nền. 
#### control -Z
- Tổ hợp phím **Ctrl + Z** thường được sử dụng trong môi trường dòng lệnh (command line) của Unix và Linux để tạm dừng (suspend) một tiến trình đang chạy trong terminal hiện tại. Khi bạn nhấn **Ctrl + Z** khi một tiến trình đang chạy, tiến trình đó sẽ bị tạm dừng và trả về sang trạng thái nền (background).
- Sau khi sử dụng **Ctrl + Z** để tạm dừng tiến trình, bạn có thể sử dụng các lệnh như **fg** để đưa tiến trình đó trở lại và tiếp tục chạy ở trạng thái foreground, hoặc **bg** để tiến trình tiếp tục chạy ở chế độ nền.
## Disk devices
### Thuật ngữ
#### ata
- Một bộ điều khiển ATA (AT Attachment) cho phép hai thiết bị trên mỗi bus, một là thiết bị master và một là thiết bị slave. Trừ khi bộ điều khiển và các thiết bị hỗ trợ cable select, bạn phải thiết lập điều này bằng cách thủ công với các chân jumper. Khi SATA (Serial ATA) được giới thiệu, ATA gốc được đổi tên thành ATA song song. Ổ đĩa quang thường sử dụng ATAPI, đây là một giao diện ATA sử dụng giao thức truyền thông SCSI.
#### scsi
- Bộ điều khiển SCSI (Small Computer System Interface) cho phép nhiều hơn hai thiết bị. Khi sử dụng SCSI, mỗi thiết bị nhận một định danh SCSI duy nhất (SCSI ID). Bộ điều khiển SCSI cũng cần một SCSI ID, không sử dụng ID này cho thiết bị được kết nối qua SCSI.
#### solid state drive (SSD)
- Ổ đĩa SSD (Solid State Drive) là một loại thiết bị lưu trữ dữ liệu không sử dụng các thành phần cơ học (ví dụ như các đĩa quay trong ổ cứng thông thường), mà thay vào đó sử dụng bộ nhớ flash để lưu trữ dữ liệu.
### device naming
#### ata device naming
- Cách đặt tên thiết bị ATA (AT Attachment) trong hệ thống Linux thường được thực hiện theo quy ước cụ thể, phản ánh vị trí và vai trò của từng ổ đĩa ATA trong hệ thống. Các thiết bị ATA được đặt tên dựa trên cấu trúc /dev, trong đó:
	- /dev/hdX: Trong quá khứ, thiết bị ATA (hoặc IDE) thường được đặt tên theo dạng /dev/hdX, trong đó X là một chữ cái từ a đến z để đại diện cho từng ổ đĩa. Ví dụ: /dev/hda, /dev/hdb, /dev/hdc, /dev/hdd, và tiếp tục.
	- Master và Slave: Thông thường, mỗi bộ điều khiển ATA có thể kết nối hai ổ đĩa: một ổ đĩa chính (master) và một ổ đĩa phụ (slave). Đối với bộ điều khiển ATA đầu tiên, các thiết bị có thể được gán nhãn /dev/hda (master) và /dev/hdb (slave). Tương tự, đối với bộ điều khiển thứ hai, có thể là /dev/hdc (master) và /dev/hdd (slave).
#### scsi divce naming
- Trong hệ thống Linux, thiết bị SCSI (Small Computer System Interface) được đặt tên dựa trên cấu trúc /dev, nhằm phản ánh vị trí và vai trò của từng thiết bị trong hệ thống. Các thiết bị SCSI có thể được đặt tên theo một số quy tắc nhất định:
	- /dev/sdX: Cấu trúc đặt tên chung cho các thiết bị SCSI trong hệ thống Linux là /dev/sdX, trong đó X là một chữ cái từ a đến z, đại diện cho từng ổ đĩa SCSI được phát hiện. Ví dụ: /dev/sda, /dev/sdb, /dev/sdc, và tiếp tục.
	- Numbering: Các thiết bị SCSI có thể được đánh số theo thứ tự mà chúng được phát hiện trong quá trình khởi động hệ thống. Do đó, /dev/sda có thể là ổ đĩa đầu tiên, /dev/sdb là ổ thứ hai, và cứ tiếp tục.
### discovering disk device
#### fdisk
- Lệnh fdisk trong hệ điều hành Linux được sử dụng để quản lý các phân vùng trên ổ đĩa. Đây là một số tùy chọn thường được sử dụng với lệnh fdisk:
	- fdisk -l: Hiển thị thông tin về các ổ đĩa có sẵn trong hệ thống, bao gồm dung lượng, số lượng phân vùng và các thông tin liên quan.
	- fdisk /dev/sdX: Mở fdisk để quản lý ổ đĩa được chỉ định (vd: /dev/sda, /dev/sdb, ...). Đây là cách để tạo, xóa hoặc sửa đổi các phân vùng trên ổ đĩa này.
	- fdisk -u /dev/sdX: Sử dụng đơn vị đo lường là sectors thay vì cylinders.
	- fdisk -m /dev/sdX: Hiển thị thông báo cảnh báo trước khi ghi thay đổi vào bảng phân vùng.
	- fdisk -t type /dev/sdX: Đặt loại phân vùng khi tạo mới một phân vùng.
#### dmesg
- Lệnh **dmesg** trong hệ điều hành Linux được sử dụng để hiển thị log kernel, cung cấp thông tin về các sự kiện và thông điệp từ kernel của hệ thống. 
#### lshw
- Lệnh **lshw** trong Linux được sử dụng để hiển thị thông tin chi tiết về phần cứng của hệ thống. Khi chạy lshw, nó sẽ truy vấn các thông số kỹ thuật về phần cứng và hiển thị chúng dưới dạng cấu trúc.
#### /proc/scsi/scsi
- Tệp **/proc/scsi/scsi** chứa thông tin về các thiết bị SCSI được nhận diện bởi hệ thống. Khi bạn đọc tệp này, thông tin chi tiết về các thiết bị SCSI sẽ được hiển thị, bao gồm thông tin về nhà sản xuất, mô hình, số serie, và các thông tin khác về các thiết bị đó.

## Disk partitions
### Parition naming
- Tên phân vùng trong Linux thường được xác định dựa trên quy tắc chuẩn và có các định dạng nhất định. Các phân vùng trên hệ điều hành Linux thường được đặt tên theo một số quy tắc cơ bản:
 	- /dev/sdXY: Trong đó 'sd' đại diện cho "scsi disk", 'X' thường là một chữ cái (a, b, c, ...) chỉ số thứ tự của ổ đĩa (sda, sdb, ...), và 'Y' là số thứ tự của phân vùng trên ổ đĩa đó (sda1, sda2, ...).
	- /dev/nvmeXnYpZ: Đối với ổ đĩa NVMe, định dạng tên có thể là 'nvmeXnYpZ', trong đó 'X' là chỉ số thiết bị, 'Y' là chỉ số phân vùng, và 'Z' là chỉ số chuẩn.
	- /dev/hdXY: Trong quá khứ, ổ đĩa IDE có thể sử dụng định dạng tên 'hdXY', trong đó 'X' là chữ cái (a, b, c, ...) chỉ số thứ tự của ổ đĩa và 'Y' là số thứ tự của phân vùng trên ổ đĩa (hda1, hda2, ...).
### Proc/partitions
- Tệp /proc/partitions chứa thông tin về các phân vùng và các thiết bị lưu trữ hiện có trên hệ thống. Khi bạn đọc tệp này, nó sẽ hiển thị một danh sách các phân vùng và các thiết bị lưu trữ được nhận diện bởi hệ thống, cùng với kích thước và thông tin chi tiết về chúng.
- Định dạng thông tin trong tệp /proc/partitions thường là các cột, bao gồm:
	- major number: Số chính của thiết bị.
	- minor number: Số phụ của thiết bị.
	- blocks: Số lượng block trên phân vùng hoặc thiết bị.
	- name: Tên thiết bị hoặc phân vùng.
## Partitioning new disk
- Phân vùng ổ đĩa mới thường được thực hiện bằng các công cụ quản lý phân vùng như fdisk, parted, hoặc gparted. Dưới đây là một số bước cơ bản để phân vùng một ổ đĩa mới:
**Sử dụng fdisk**
- Kiểm tra danh sách ổ:
	```sh
	fdisk -l
	```
- Mở fdisk cho ổ đĩa mới
	```sh
	fdisk /dev/sdX
	```
Thay thế **/dev/sdX/** bằng địa chỉ của ổ đĩa mới
- Tạo phân vùng 
	- Nhấn n để tạo một phân vùng mới.
	- Chọn loại phân vùng (primary, extended, logical).
	- Đặt kích thước và vị trí cho phân vùng.
	- Nhấn w để lưu và thoát.
## Primary, Extened, Logical
Có ba loại phân vùng cơ bản:
- **Primary Partition** (Phân vùng chính): Đây là loại phân vùng cơ bản và được sử dụng để cài đặt hệ điều hành và lưu trữ dữ liệu. Một ổ đĩa có thể có tối đa bốn phân vùng chính.
- **Extended Partition** (Phân vùng mở rộng): Phân vùng mở rộng không chứa dữ liệu trực tiếp mà nó chứa các phân vùng logic bên trong. Bởi vì mỗi ổ đĩa chỉ có thể có tối đa bốn phân vùng chính, nếu bạn muốn có nhiều hơn, bạn có thể tạo một phân vùng mở rộng để chứa các phân vùng logic bên trong nó.
- **Logical Partition** (Phân vùng logic): Các phân vùng logic là các phân vùng nằm bên trong phân vùng mở rộng. Chúng được sử dụng để tạo nhiều hơn bốn phân vùng trên một ổ đĩa và không được sử dụng để cài đặt hệ điều hành. Một phân vùng mở rộng có thể chứa nhiều phân vùng logic tùy thuộc vào số lượng bạn muốn tạo.

# Flie system
## Common fiel systems
### ext2 and ext3
**ext2** và **ext3** là hai loại hệ thống tệp (file system) phổ biến trong các hệ điều hành Linux. Dưới đây là một số điểm khác biệt chính giữa chúng:
**ext2** (Second Extended File System):
- Không có Journaling: ext2 không có tính năng ghi nhật ký (journaling), điều này có nghĩa là khi có sự cố như mất điện, máy tính bị treo, dữ liệu có thể bị mất hoặc hỏng và có thể cần thời gian lâu để kiểm tra và sửa chữa.
- Performance Tốt: Do không có việc ghi nhật ký, ext2 thường có hiệu suất tốt hơn ext3 trong một số tình huống, đặc biệt là ở các ứng dụng cần tốc độ ghi nhanh và thường xuyên.
**ext3** (Third Extended File System):
- Journaling: ext3 đã bổ sung tính năng ghi nhật ký (journaling) so với ext2. Điều này giúp bảo vệ dữ liệu khi xảy ra sự cố hệ thống bằng cách ghi lại các thay đổi vào một nhật ký trước khi thực hiện thay đổi thực tế trên đĩa.
- Sự Ổn Định Hơn: Vì có journaling, ext3 thường ổn định hơn trong các tình huống mất điện hoặc máy tính bị treo, giúp tránh được việc mất dữ liệu và giảm thời gian khôi phục sau khi xảy ra sự cố.
### /proc/filesystems
- Tệp **/proc/filesystems** là một tệp ảo trong hệ thống tệp /proc của Linux. Tệp này cung cấp thông tin về các hệ thống tệp được hỗ trợ trong kernel của hệ điều hành. Khi xem nội dung của tệp này, bạn sẽ thấy danh sách các loại hệ thống tệp mà kernel hỗ trợ.
