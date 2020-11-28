## 1. Tổng quan VDI
VDI (Virtual Desktop Infrastructure) là công nghệ được sử dụng để tạo môi trường máy tính để bàn ảo hóa trên máy chủ từ xa. VDI phân các máy chủ thành nhiều máy tính để bàn ảo khác nhau mà người dùng có thể truy cập từ xa thông qua thiết bị của họ. Các máy tính để bàn ảo này được lưu trữ trên Máy ảo (VM) được điều khiển thông qua phần mềm quản lý.
Với VDI, tất cả các máy tính đều là ảo, người dùng có thể truy cập chúng ngay cả với một thiết bị nhỏ hơn (máy tính bảng, điện thoại,...).

**Các thành phần của VDI:**
- Virtualization: là việc tạo phiên bản ảo của máy tính để bàn, hệ điều hành, máy chủ hoặc bộ nhớ
- Hypervisor: Là một chương trình phần mềm giám sát máy ảo, có chức năng quản lý một hoặc nhiều máy ảo, tách hệ điều hành khỏi phần cứng bên dưới bằng cách tạo ra một môi trường ảo hóa. Cho phép mỗi máy ảo truy cập vào tài nguyên phần cứng vật lý như CPU, RAM và lưu trữ.
- Connection broker: Là một chương trình phần mềm cho phép người dùng cuối kết nối với một máy tính ảo từ xa. Nó cũng chịu trách nhiệm xác thực người dùng và gửi họ đến các phiên bản máy tính để bàn của họ. Theo dõi các máy tính để bàn hoạt động và không hoạt động. Khi người dùng gửi yêu cầu kết nối với máy tính để bàn, nó sẽ cung cấp cho người dùng một phiên bản máy tính không hoạt động. Khi người dùng ngắt kết nối máy tính để bàn, nó sẽ cập nhật trạng thái thành không hoạt động.
- Desktop pools: là một nhóm máy tính để bàn ảo có cấu hình giống nhau(hệ điều hành, bộ nhớ, ứng dụng,...) đáp ứng cho một bộ phận, phòng ban với những yêu cầu đặc trưng.
- Application Virtualization: là công nghệ được sử dụng để tạo image ứng dụng ảo hóa và sao chép nó sang tất cả các máy tính để bàn ảo trong một Desktop pools. Nó giúp việc triển khai ứng dụng dễ dàng và đồng nhất.

## 2. Cách thức hoạt động:
- Khi user gửi yêu cầu đăng nhập vào Desktop ảo từ phần mềm tại end point, Connection Broker sẽ phân tích yêu cầu và điều hướng người dùng đến Desktop ảo phù hợp trong Desktop pools.
- Hypervisor cài đặt trên các máy chủ cung cấp tính sẵn sàng cao khi có thể di chuyển các máy ảo đến máy chủ khác nếu cần.
- Với mô hình VDI, có thể đáp ứng lượng người dùng lớn hơn dung lượng thực của máy chủ. Vì manager có thể shutdown các máy ảo khi không có người sử dụng.
- Các image của master Desktop ảo được phản ánh lên các Desktop ảo khác. Có 2 cách thức để thực hiện việc này:
  - Full cloning: clone Desktop không yêu cầu kết nối liên tục với master Desktop, nó hoạt động như một Desktop độc lập, sử dụng không gian đĩa riêng biệt, không chia sẻ với các máy ảo khác. Phương pháp tập trung vào hiệu suất hoạt động.
  - Linked cloning: clone Desktop luôn phải được kết nối với master Desktop. Không gian đĩa được chia sẻ, dữ liệu của tất cả người dùng được lưu riêng. Phương pháp tập trung vào khả năng đáp ứng đối với các tác vụ nhỏ, tiết kiệm không gian đĩa cho máy chủ.
