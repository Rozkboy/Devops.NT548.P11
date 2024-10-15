Devops.NT548.P11
Họ và tên: Huỳnh Viết Tuấn  
MSSV: 22521602  
Lớp: NT548.P11  

Hướng dẫn sử dụng VPC và kết nối EC2

1. Kết nối SSH vào Public EC2 Instance

Yêu cầu:
- File .pem: File này dùng để kết nối SSH vào EC2 từ terminal hoặc các ứng dụng tương thích với SSH.
- File .ppk: Dùng cho ứng dụng Putty để kết nối từ xa vào EC2.

2. Kết nối thông qua SSH
Để kết nối vào EC2 instance thông qua SSH (terminal), bạn cần sử dụng file khóa .pem và thực hiện lệnh sau:

ssh -i "Tuan1602EC2.pem" ec2-user@ec2-54-153-239-209.ap-southeast-2.compute.amazonaws.com

- Public DNS: ec2-54-153-239-209.ap-southeast-2.compute.amazonaws.com
- Thay thế "Tuan1602EC2.pem" bằng đường dẫn tới file .pem của bạn.

3. Kết nối thông qua Putty
- Nếu bạn dùng Putty, cần phải sử dụng file .ppk.
- Thực hiện các bước sau để kết nối:
  - Mở Putty và trong phần "Host Name", nhập địa chỉ:  
    ec2-54-153-239-209.ap-southeast-2.compute.amazonaws.com.
  - Trong phần "Connection > SSH > Auth", chọn file .ppk tương ứng.
  - Nhấn "Open" để kết nối.

4. Thông tin về VPC và Instance
- Public DNS: ec2-54-153-239-209.ap-southeast-2.compute.amazonaws.com
- Public IP: 54.153.239.209 (sử dụng IP công cộng đã được gán cho EC2)
- Private IP: 10.0.2.173
  
5. Lưu ý
- File .pem dùng cho kết nối SSH, đảm bảo quyền hạn của file phù hợp:
  
chmod 400 Tuan1602EC2.pem

- File .ppk chỉ sử dụng cho Putty.

6. Kiểm tra kết nối Private EC2 từ Public EC2
Sau khi kết nối thành công vào Public EC2, thực hiện lệnh SSH sau để kết nối đến Private EC2 (dùng IP private của EC2):

- Kiểm tra file .pem ở mục Dowloads
ls /home/ec2-user/Downloads

- Nếu không cung cấp file .pem, bạn sẽ gặp lỗi sau:
Permission denied (publickey,gssapi-keyex,gssapi-with-mic).

- Thực hiện SSH sau kèm theo đường dẫn file .pem trước đó
ssh -i /home/ec2-user/Downloads/Tuan1602EC2.pem ec2-user@10.0.2.173

- Nếu không tồn tại file .pem và câu lệnh ssh truy cập vào Private EC2 báo lỗi Permission denied (publickey,gssapi-keyex,gssapi-with-mic). Thì hãy tải file .pem từ bên ngoài vào thư mục có sẵn sau đó gắn đường dẫn đến file .pem đó trong câu lệnh ssh kết nối đến Private EC2.

7. Kiểm tra kết nối Internet từ Private Instance qua NAT Gateway
Từ Private EC2, kiểm tra kết nối Internet bằng cách:

ping google.com
