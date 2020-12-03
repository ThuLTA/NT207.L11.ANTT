## 1. Web Application Firewall
Web Application Firewall – WAF là lớp bảo vệ nằm giữa người dùng và website, nơi các yêu cầu truy cập của người dùng đi qua. Tại đây, WAF giám sát, lọc và chặn các gói dữ liệu khi chúng di chuyển đến và đi từ một trang web hoặc ứng dụng web.
Cách thức hoạt động: WAF phân tích các yêu cầu HTTP/HTTPS và áp dụng một bộ quy tắc xác định phần nào của cuộc trao đổi thông tin đó là vô hại và phần nào là độc hại. Các phần chính của việc trao đổi thông tin HTTP/HTTPS mà WAF phân tích là các yêu cầu GET và POST.

**Các phương pháp WAF tiếp cận để phân tích và lọc nội dung có trong các yêu cầu:**
- Whitelisting (mô hình Positive):  WAF chỉ cho phép các yêu theo một danh các IP được cho là an toàn.
	- Ưu điểm: Whitelisting ít tốn tài nguyên hơn so với danh sách đen. Dễ kiểm soát truy cập.
	- Nhược điểm: vô tình chặn lưu lượng truy cập vô hại. Mặc dù nó tạo ra một mạng lưới rộng và có thể hiệu quả, nhưng nó cũng có thể không chính xác.
- Blacklisting (mô hình negative):  mặc định cho phép các gói tin đi qua và chỉ chặn những lưu lượng mà WAF cho là độc hại dựa vào danh sách các quy tắc chỉ ra các gói độc hại.
	- Ưu điểm: thích hợp hơn cho các trang web và ứng dụng web công cộng vì chúng nhận được nhiều lưu lượng truy cập từ các địa chỉ IP không quen thuộc mà không được biết là độc hại hoặc lành tính.
	- Nhược điểm: tốn nhiều tài nguyên hơn; nó yêu cầu nhiều thông tin hơn để lọc các gói dựa trên các đặc điểm cụ thể, trái ngược với việc mặc định là địa chỉ IP đáng tin cậy.
- Hybrid security (Kết hợp): Mô hình bảo mật kết hợp sử dụng các yếu tố của cả Whitelisting và Blacklisting
Có thể triển khai WAF theo các mô hình: bridge mode, proxy mode, one-arm proxy*

## 2. Database Firewall
Database Firewall (DBF) là một phần WAF, mục tiêu là xác định và bảo vệ hệ thống khỏi các cuộc tấn công tìm cách khai thác các thông tin nhạy cảm nhắm đến database, cho phép giám sát và kiểm soát các truy cập đến database thông qua việc ghi chép nhật ký.

**Một DBF sẽ đảm bảo các tính chất:**
- Confidentiality: đảm bảo csdl được bảo mật khỏi các vi phạm bên ngoài lần bên trong hệ thống; chỉ được truy cập bởi các user được phép; hành động của các user đều được ghi lại.
- Intergrity: xác minh dữ liệu tuân theo các quy tắc, báo cáo các hoạt động thay đổi dữ liệu.
- Available: dữ liệu luôn sẵn sàng khi cần thiết và với những đối tượng thích hợp.
- Authenticity: dữ liệu được chỉnh sửa bởi người được ủy quyền; biết chính xác người truy cập hệ thống; dữ liệu đến đúng đối tượng muốn gửi.

DBF bao gồm các hính sách kiểm tra bảo mật được xác định trước và có thể tùy chỉnh. DBF dựa vào các signature của các cuộc tấn công trong quá khứ để xác định một câu truy vấn có nguy hại đến database hay không. Các signature này được cập nhật thường xuyên.

## 3. SIEM
Security information and event management (SIEM – hệ thống giám sát an ninh mạng) là hệ thống được thiết kế nhằm thu thập và phân tích nhật ký, các sự kiện an ninh từ các thiết bị đầu cuối và được lưu trữ tập trung. SIEM cho phép phân tích tập trung và báo cáo về các sự kiện an ninh mạng của tổ chức, phát hiện thông qua các bộ luật tương quan (correlation rule), giúp phát hiện các cuộc tấn công mà không thể phát hiện được bởi các giải pháp thông thường (IDS/IPS, Firewall…).

**Quá trình tổng quan đơn giản của SIEM:**
>Thu thập data từ các file log do các endpoint cung cấp --> tương quan sự kiện --> cảnh báo sự cố --> tạo report --> lưu trữ để phân tích.

**Mục tiêu:**
- Phát hiện tấn công bằng cách duy trì giám sát liên tục
- Cải thiện hệt thống lưu trữ
- Phát hiện hành vi bất thường
- Tạo dashboard trực quan
DBF bao gồm các hính sách kiểm tra bảo mật được xác định trước và có thể tùy chỉnh. DBF dựa vào các signature của các cuộc tấn công trong quá khứ để xác định một câu truy vấn có nguy hại đến database hay không. Các signature này được cập nhật thường xuyên.

**Những lợi ích mà SIEM mang lại:**
- Quản lí tập trung: tập hợp dữ liệu về các sự kiện an nình từ các thiết bị đầu cuối và chuyển về máy chủ SIEM; sau đó SIEM thực hiện thống kê, phân tích, báo cáo để cung cấp sự tương quan giữa các sự kiện an ninh của các thiết bị
- Giám sát an ninh mạng: SIEM thu thập dữ liệu, quan sát và tạo ra nhật ký, có khả năng phân tích; vì vậy mà có thể phát hiện các sự cố à một số thiết bị thông thường không phát hiện được. Bằng việc thu thập sự kiện của toàn hệ thống, SIEM cho thấy được nhiều phần khác nhau của các cuộc tấn công thông qua nhiều thiết bị, từ đó tái cấu trúc chuỗi sự kiện và xác định tính chất của cuộc tấn công. 
- Cải thiện hoạt động phát hiện và xử lý sự cố: phát hiện nhanh chóng các thiệt bị đầu cuối bị ảnh hưởng bời cuộc tấn công; cung cấp cơ chế tự động nhằm ngăn chặn các cuộc tấn công đang diễn ra và cách ly.

## 4. Endpoint security
Endpoint Security (EPS) là giải pháp tập trung vào việc bảo vệ các thiết bị ở điểm cuối trong hệ thống (PC, điện thoại, máy in,…) để giữ an toàn cho mạng. Các thiết bị cuối được cài đặt các công cụ bảo mật và được quản lý tập trung.

**Một mô hình EP cơ bản gồm:** 
- Agent: chạy ở chế độ nền trên các thiết bị cuối
- Manage: theo dõi và kiểm soát các agent một cách tập trung.
Một hệ thống EPS được thiết kế để nhanh chóng phát hiện, phân tích, ngăn chặn các cuộc tấn công. Để làm được điều này thì cần nhiều công cụ bảo mật kết hợp, cung cấp cho manager các khả năng về các mối nguy hại có thể xảy ra nhằm tăng khả năng phản ứng và thời gian khắc phục hậu quả nếu có.

## 5. Backup
Backup là quá trình sao lưu và lưu trữ toàn bộ thông tin dữ liệu phòng khi máy tính/hệ thống máy tính gặp sự cố. Hiểu đơn giản, backup sẽ tạo bản sao để đảm bảo khi bạn mất dữ liệu gốc vẫn có dữ liệu khác phục hồi.

Quá trình backup sẽ được thực hiện thường xuyên và có lịch trình nhằm cập nhật các dữ liệu mới trong quá trình sử dụng. Dữ liệu sẽ được backup vào ổ cứng vật lý hoặc lên cloud. 

**Một số tình huống xấu dẫn đến việc chúng ta cần sử dụng đến dữ liệu backup như:**
- Sự cố hệ thống, cháy, nổ, hư hỏng phần cứng
- Bị tin tặc tấn công, phá hoại dữ liệu
- Do người dùng thao tác sai, sửa/xóa dữ liệu quan trọng.
- …

**Một số kỹ thuật backup:**
- Full backup: sao lưu toàn bộ dữ liệu đang có
- Differential backup: sao lưu những phần dữ liệu thay đổi so với lần full backup gần nhất
- Incremental backup: chỉ sao lưu những dữ liệu mới so với lần incremental backup gần nhất

Mỗi kỹ thuật đều có ưu nhược điểm và yêu cầu chi phí về phần cứng để lưu trữ khác nhau. Vì vậy, người dùng có thể thực hiện backup theo lộ trình: FB hàng tháng, DB hàng tuần, IB hàng ngày.

## 6. Antivirus
Antivirus là một loại phần mềm dùng để ngăn chặn, quét, phát hiện và xóa virus khỏi máy tính. Sau khi được cài đặt, hầu hết các phần mềm chống virus sẽ tự động chạy nền để cung cấp khả năng bảo vệ theo thời gian thực trước các cuộc tấn công.

Các chương trình bảo vệ chống vi-rút toàn diện giúp bảo vệ tệp và phần cứng của bạn khỏi phần mềm độc hại như worm, Trojan và phần mềm gián điệp, đồng thời cũng có thể cung cấp biện pháp bảo vệ bổ sung như tường lửa có thể tùy chỉnh và chặn trang web.

**Cách thức một chương trình Antivirus bảo vệ máy tính:**
- Về bản chất: Antivirus đi kèm với một thư mục gồm các mã virus được thu thập. Nếu một tệp hay chương trình nào đó có chứa mã trùng khớp với một loại virus đã được Antivirrus định nghĩa thì chúng sẽ bị cách ly.
- Với các loại virus được mã hóa hoặc chưa được xác định, Antivirus sẽ theo dõi các hành vi của chương trình, kích hoạt cảnh báo hoặc cách li nếu các hành động là được thực thi như:
	- Thay đổi cài đặt của các chương trình khác
	- Sửa đổi/xóa các tệp khác
	- Tạo kết nối từ xa khi chưa được cho phép
	- …
## 7. Load Balancing
Cân Bằng Tải là việc phân bố đồng đều lưu lượng truy cập giữa hai hay nhiều các máy chủ có cùng chức năng trong cùng một hệ thống về các vấn đề liên kết mạng, CPU, không gian đĩa,… 

**Lợi ích khi triển khai giải pháp cân bằng tải cho hệ thống:**
- Giúp cho hệ thống giảm thiểu tối đa tình trạng một máy chủ bị quá tải và ngưng hoạt động.
- Khi một máy chủ gặp sự cố, Cân Bằng Tải sẽ phân phối công việc của máy chủ đó cho các máy chủ còn lại, cải thiện năng suất hoạt động tổng thể, không 	làm gián đoạn dịch vụu người dùng.
- Là cơ chế rất quan trọng trong việc mở rộng quy mô của mạng máy tính.Khi lắp đặt một máy chủ mới vào hệ thống, Cân Bằng Tải sẽ tự động cắt giảm khối lượng công việc từ các máy chủ cũ và chuyển sang máy chủ datacenter mới.

**Các phương pháp cân bằng tải:**
| So sánh | Hardware LB | Software LB | Proxy server LB | 
| ------- | ----------- | ----------- | ----------- |
| Khả năng theo dõi trạng thái ứng dụng | Kém | Tốt | Kém |
| Mở rộng | Tốt | Kém | Tốt |
| Tăng tốc, hiệu năng ứng dụng | Tốt | Kém | Kém |
| Bảo mật | Kém | Chấp nhận được | Tốt (firewall) |

**Thuật toán CBT:**
- Weighted Balancing: cân bằng theo tỉ lệ mà người quản trị đặt ra
- Priority: các WAN sẽ được người quản trị sắp đtajw mức độ ưu tiên, đường WAN có mức ưu tiên cao nhất sẽ đảm nhận lưu lượng truy cập của user. Khi WAN ưu tiên cao nhất mất kết nối thì WAN ưu tiê thấp hơn sẽ được kích hoạt.
- Overflow: Các WAN cũng được phân mức độ ưu tiên. Lúc cao điểm WAN ưu tiên cáo trước khi bị tắt nghen băng thông, các WAN còn lại sẽ được kích hoạt để chia sẽ lưu lượng, tránh tắt nghẽn.
- Persistence: dựa vào địa chỉ IP nguồn và đích, kết nối sẽ được chỉ định cố định dựa vào 2 địa chỉ IP đó để lưu thông cho tới khi phiên kết nối đó kết thúc.
- Least used: Băng thông sẽ được chia sẻ lần lượt đến các WAN có lượt truy cập ít hơn 
- Lowest latency: Truy cập sẽ được chỉ định đến WAN có độ trễ truy cập thấp nhất.
- Enforced: Chỉ định 1 IP, 1 Subnet, 1 MAC address … đến 1 Subnet, 1 IP, 1 Domain nào đó đi 1 đường duy nhất dù đường WAN đó up hay down
- Fastest Response Time: Sử dụng kết nối có phản hồi sớm nhất (low ltency) từ đích trong suốt phiên hoạt động.

**Phân loại:**
- LB layer 4: 
	- Cách đơn giản để cân bằng lưu lượng mạng. 
	- Chuyển tiếp lưu lượng truy cập của người udngf dựa trên phạm vi IP và port.
	- Tất cả các web-backend server đều có nội dung đồng nhất.
	- Tất cả web server đều kết nối đến cùng một database server.
- LB layer 7:
	- Chuyển tiếp các requests đến các backend server khác nhau dựa vào nội dung request.
	- Cho phép chạy nhiều web application servers trong cùng một domain và port.	


