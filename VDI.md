## 1. Tổng quan VDI
VDI (Virtual Desktop Infrastructure) là công nghệ được sử dụng để tạo môi trường máy tính để bàn ảo hóa trên máy chủ từ xa. VDI phân các máy chủ thành nhiều máy tính để bàn ảo khác nhau mà người dùng có thể truy cập từ xa thông qua thiết bị của họ. Các máy tính để bàn ảo này được lưu trữ trên Máy ảo (VM) được điều khiển thông qua phần mềm quản lý.
Với VDI, tất cả các máy tính đều là ảo, người dùng có thể truy cập chúng ngay cả với một thiết bị nhỏ hơn (máy tính bảng, điện thoại,...).

**Các thành phần của VDI:**
- Virtualization: là việc tạo phiên bản Desktop ảo, hệ điều hành, máy chủ hoặc bộ nhớ
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
    - Ví dụ: Khi có sự thay đổi bất kỳ hoặc shutdown master Desktop thì cũng sẽ không làm ảnh hưởng đến máy ảo full clone.
  - Linked cloning: clone Desktop luôn phải được kết nối với master Desktop. Không gian đĩa được chia sẻ, dữ liệu của tất cả người dùng được lưu riêng. Phương pháp tập trung vào khả năng đáp ứng đối với các tác vụ nhỏ, tiết kiệm không gian đĩa cho máy chủ.
    - Ví dụ: Vì chia sẻ không gian đĩa nên kết nối luôn được duy trì, khi có bất kỳ cập nhật, thay đổi, nâng cấp phần mềm tại master Desktop thì các máy linked clone đều được cập nhật giống với master desktop.

## 3. Lợi ích khi triển khai mô hình văn phòng VDI
**Simplified and Centralized Management:** Quản lí tập trung và đơn giản hóa
- Giải quyết các vấn đề về cơ sở hạ tầng như:
  - Không gian để triển khai văn phòng.
  - Nơi đặt server
  - Thiết bị để làm việc
- Công việc có thể được thực hiện từ xa để giải quyết các lỗi từ 1 server trạm duy nhất.
**Flexibility:** Tính linh hoạt
- Thực hiện nâng cấp update trên master Destop, các bản sao sẽ được triển khai lên các VM, không mất thời gian cho việc cài đặt cho từng máy.
- Tạo ra VM mới một cách nhanh chóng mà không làm ảnh hưởng đến người dùng khác.
**Accessibility:** Khả năng tiếp cận
Các thiết bị như điện thoại di động, máy tính bảng,... đều có thể được sử dụng thay cho desktop truyền thống. Ngoài ra, người dùng có thể sử dụng một số phần mềm không có sẵn, chẳng hạn như các gói phần mềm riêng biệt trên Windows trên Mac.
**Cost Efficiency:** Hiệu quả về chi phí
VDI thể hiện rất rõ việc tiết kiệm chi phí hơn một mô hình truyền thống, nhất là chi phí để triển khai văn phòng. Bên cạnh đó, thiết bị endpoint sử dụng trong VDI cũng không đắt như một PC thông thường dù có tuổi thọ cao hơn, cấu hình mạnh mẽ hơn.
**Data Security and Instant Backup Capabilities:** Bảo mật dữ liệu và sao lưu tức thì
Thực tế phổ biến ở các công ty đang vận hành các hệ thống quan trọng là triển khai VDI trong hai trung tâm dữ liệu riêng biệt. Một cái đóng vai trò cếu vì bất kỳ lý do gì mà một trung tâm ngừng hoạt động do thỏa hiệp về bảo mật hoặc lỗi thành phần chính, thì sẽhính trong khi cái kia là một trang dự phòng để dự phòng. N có sự chuyển giao ngay lập tức cho trang web dự phòng để các dịch vụ tiếp tục liền mạch và không bị gián đoạn.
**Bring your own device (BYOD)**
Cung cấp khả năng sử dụng bất kì thiết bị nào để làm việc.
