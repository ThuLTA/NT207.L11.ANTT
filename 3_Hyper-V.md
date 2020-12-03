## 1. Khái niệm
Hyper-V là sản phẩm ảo hóa phần cứng của Microsoft, cho phép bạn tạo và chạy phiên bản phần mềm của máy tính, được gọi là máy ảo. Mỗi máy ảo hoạt động như một máy tính hoàn chỉnh, chạy hệ điều hành và các chương trình.

**Lợi ích Hyper-V mang lại:**
- Thiết lập hoặc mở rộng môi trường đám mây riêng. Cung cấp các dịch vụ CNTT theo yêu cầu, linh hoạt hơn bằng cách chuyển sang hoặc mở rộng việc sử dụng các tài nguyên được chia sẻ và điều chỉnh việc sử dụng khi nhu cầu thay đổi.
- Sử dụng phần cứng hiệu quả hơn, hợp nhất các máy chủ và khối lượng công việc vào ít máy tính vật lý hơn, sử dụng ít năng lượng và không gian vật lý hơn.
- Thiết lập hoặc mở rộng cơ sở hạ tầng máy tính để bàn ảo (VDI). Sử dụng chiến lược máy tính để bàn tập trung với VDI có thể giúp tăng cường sự linh hoạt trong kinh doanh và bảo mật dữ liệu.
- Làm cho việc phát triển và kiểm tra hiệu quả hơn. Tái tạo các môi trường máy tính khác nhau mà không cần phải mua hoặc duy trì tất cả phần cứng bạn cần nếu bạn chỉ sử dụng hệ thống vật lý.

**Những tính năng của Hyper-V:**
- Computing environment - Máy ảo Hyper-V bao gồm các bộ phận cơ bản giống như máy tính vật lý, có thể cấu hình theo các cách khác nhau tùy theo nhu cầu.
- Disaster recovery and backup - Để khôi phục sau thảm họa, Hyper-V Replica tạo bản sao của máy ảo, nhằm mục đích lưu trữ ở một vị trí thực khác, vì vậy có thể khôi phục máy ảo từ bản sao. Hyper-V cung cấp hai loại sao lưu: sử dụng các trạng thái đã lưu ; sử dụng Volume Shadow Copy Service (VSS) để bạn có thể tạo các bản sao lưu phù hợp với ứng dụng cho các chương trình hỗ trợ VSS.
- Optimization - Mỗi hệ điều hành khách được hỗ trợ có một bộ dịch vụ và trình điều khiển tùy chỉnh, được gọi là dịch vụ tích hợp, giúp sử dụng hệ điều hành trong máy ảo Hyper-V dễ dàng hơn.
- Portability - Các tính năng như di chuyển trực tiếp, di chuyển bộ nhớ và nhập / xuất giúp di chuyển hoặc phân phối máy ảo dễ dàng hơn so với hệ thống vật lý.
- Remote connectivity - Hyper-V bao gồm Virtual Machine Connection, một công cụ kết nối từ xa để sử dụng với cả Windows và Linux. Công cụ này cung cấp cho bạn quyền truy cập bảng điều khiển, vì vậy bạn có thể xem những gì đang xảy ra với khách ngay cả khi hệ điều hành chưa được khởi động, vượt trội hơn so với remote Desktop.
- Security - Khởi động an toàn giúp bảo vệ khỏi phần mềm độc hại và các truy cập trái phép khác vào máy ảo và dữ liệu của máy ảo.

## 2. Cấu trúc Hyper-V
Hyper-V phân chia mỗi máy ảo thành một partition. Một partition là một đơn vị cách ly về mặt logic và có thể chứa một hệ điều hành làm việc trong đó. Thường có ít nhất 1 partition gốc chứa OS và ngăn ảo hóa, có quyền truy cập trực tiếp các thiết bị phần cứng. Tiếp theo đó, partition gốc có thể sinh các partition con (được gọi là máy ảo) để chạy (guest OS). Một partition con cũng có thể sinh tiếp các partition con của mình.

Hyper-V gồm 3 phần chính:
- Hypervisor: 
  - Là một chương trình phần mềm giám sát máy ảo, có chức năng quản lý một hoặc nhiều máy ảo (VM) được tách biệt các hệ điều hành và ứng dụng của máy tính với phần cứng vật lý cơ bản.
  - Các hypervisor cho phép mỗi máy ảo truy cập vào tài nguyên phần cứng vật lý như CPU, RAM và lưu trữ. Đồng thời nó cũng có thể giới hạn số lượng tài nguyên hệ thống mà mỗi máy ảo có thể sử dụng để đảm bảo cho nhiều máy ảo cùng sử dụng đồng thời trên một hệ thống.
- Parent Partition: 
  - Đây là phân vùng giữ nhiệm vụ tạo và quản lý các phân vùng con trên hệ thống, giao tiếp trực tiếp với phần cứng và tài nguyên ảo hóa logic.
  - Phân vùng này quản lý và phân bố thiết bị phần cứng đồng thời hiển thị cho bộ xử lý và cấp phát bộ nhớ tất cả điều hoạt động thông qua lớp Hypervisor. Tài nguyên phần cứng của phân vùng cha sẽ được chia sẻ và cấp phát sử dụng bởi các phân vùng con. Bên cạnh đó còn mang nhiệm vụ quản lý điện năng tình trạng hoạt động và ghi nhận các sự cố lỗi khi xảy ra.
- Child Partitions:
  - Một partition con không có quyền truy cập trực tiếp tài nguyên vật lý, mà chỉ “nhìn thấy” chúng với danh nghĩa là thiết bị ảo (virtual device). 
  - Mọi yêu cầu đến thiết bị ảo sẽ được chuyển qua VMBus đến thiết bị ở partition cha. Thông tin hồi đáp cũng được chuyển hướng thông qua VMBus. Nếu thiết bị ở partition cha cũng là thiết bị ảo, nó sẽ được chuyển hướng tiếp tục cho đến khi gặp thiết bị thực ở partition gốc.
  