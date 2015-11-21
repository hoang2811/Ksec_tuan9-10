**SSH** (có tên tiếng Anh: Secure Shell) là một giao thức mạng dùng để thiết lập kết nối mạng một cách bảo mật.
**SSH** hoạt động ở lớp trên trong mô hình phân lớp TCP/IP. Các công cụ **SSH** (như là OpenSSH,…) cung cấp cho người dùng cách thức để thiết lập kết nối mạng được mã hoá để tạo một kênh kết nối riêng tư. Hơn nữa tính năng tunneling của các công cụ này cho phép chuyển tải các giao vận theo các giao thức khác. Do vậy có thể thấy khi xây dựng một hệ thống mạng dựa trên SSH, chúng ta sẽ có một hệ thống mạng riêng ảo VPN đơn giản.

#####SSH là gì?
**SSH** là một chương trình tương tác giữa máy chủ và máy khách có sử dụng cơ chế mã hoá đủ mạnh nhằm ngăn chặn các hiện tượng nghe trộm, đánh cắp thông tin trên đường truyền. Sử dụng SSH là biện pháp hữu hiệu bảo mật dữ liệu trên đường truyền từ hệ thống này đến hệ thống khác.

#####Cách thức làm việc của SSH

SSH thường làm việc thông qua 3 bước:

Định danh host – xác định định danh của hệ thống tham gia phiên làm việc **SSH**.<br>
Mã hoá – thiết lập kênh làm việc mã hoá.<br>
Chứng thực – xác thực người sử dụng có quyền đăng nhập hệ thống.(user|pass)<br>

1 **SSH** thường có dạng như sau:

>IP(Host)|user|pass.

Ví dụ: 192.168.123.255|admin|admin hoặc abc.com|root|root

### Cấu hình SSH

SSH hoạt động đc hầu hết trên các Linux distro.

Cài gói openssh-server
 
>sudo apt-get install openssh-server

Kiểm tra Open SSH có hoạt động không<br>
	**`ps -e | grep openssh`**<br>
Nếu không hoạt động, ta khởi động openssh<br>
	**`sudo /etc/init.d/ssh start`**<br>
Cấu hình cho ssh<br>
	**`sudo gedit /etc/ssh/sshd_config`**
	
Chỉnh sửa tùy vào chính sách bảo mật riêng. Chỉnh sửa port , 1024 port đầu dùng cho các giao thức, ta chỉnh port < 65535 (tốt nhất là từ 1500-5000). 

Ví dụ , chỉnh port là 1500

	 # What ports, IPs and protocols we listen for
	 Port 1500`
	
P/S: Sử dụng nmap để tránh các port đã sử dụng

>	sudo apt-get install nmap<br>
>	nmap -v <IP address>
	
	
`#Listen address 0.0.0.0`

Lắng nghe ở interface 0.0.0.0, phần này chỉ thiết lập cho hệ thống có nhiều interface

>`#PermitRootLogin  yes`

Cho phép login vào tài khoản root. Khuyến cáo: ko nên để yes!

>`#AllowUsers <account>`

Đồng ý cho phép login thông qua tài khoản nhất định

>`#DenyUsers<account>`

Không cho phép login thông qua tài khoản nhất định

Save lại, restart lại ssh<br>
	**`sudo /etc/init.d/ssh restart`**<br>
Kết nối vào hệ thống:<br>
	**`ssh -p 1500 <address máy cần kết nối> -l <user>`**<br>
Gõ “yes” & pass của user => ^^


