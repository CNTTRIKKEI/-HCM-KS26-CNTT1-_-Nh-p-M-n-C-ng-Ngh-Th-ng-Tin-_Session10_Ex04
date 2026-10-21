# Phần 1. Phân tích : yêu cầu chức năng và phi chức năng
Trong việc xây dựng hệ thống phần mềm y tế (Healthcare Software), việc tách bạch rõ ràng giữa Yêu cầu chức năng (Functional Requirements) và Yêu cầu phi chức năng (Non-functional Requirements - đặc biệt là bảo mật) là yếu tố then chốt:
| Tiêu chí phân loại | yêu cầu chức năng | yêu cầu phi chức năng |
| --- | --- | --- | 
| Định Nghĩa | Mô tả hệ thống phải làm gì để đáp ứng các nghiệp vụ khám chữa bệnh thực tế của phòng khám | Mô tả hệ thống hoạt động ra sao về mặt chất lượng, hiệu năng và đặc biệt là chuẩn an toàn thông tin y tế |
| ví dụ | - tiếp nhận thông tin bệnh nhân | - Bảo mật dữ liệu  
|       |   - Ghi nhận huyết áp , nhiệt độ , nhịp tim | - phân quyền chặt chẽ : bác sĩ chỉ xem đc bệnh án của , lễ tân chỉ xem được thông tin hành chính |
|       | - lập phiếu khám bệnh và kê đơn | -theo dõi truy cập
# PHẦN 2. TRIỂN KHAI: HỆ THỐNG CLINIC-CLOUD TÍCH HỢP
1. Word – Tài liệu Đặc tả yêu cầu (SRS) Module Bệnh án điện tử
Quản lý cấu trúc bằng Navigation Pane: Tài liệu SRS được phân cấp chuẩn từ Heading 1 đến Heading 3, giúp dễ dàng kiểm soát các điều khoản về bảo mật dữ liệu y tế và quy trình khám bệnh.

Các nội dung cốt lõi trong SRS:

Tổng quan hệ thống phần mềm quản lý phòng khám Startup Clinic.   
JPG

Đặc tả chi tiết các tác vụ nghiệp vụ khám chữa bệnh (Functional).

Khung tiêu chuẩn bảo mật dữ liệu theo quy định y tế (Non-functional) gồm mã hóa AES-256, sao lưu định kỳ trên đám mây và cơ chế phân quyền RBAC.   
JPG

2. Excel – Quản lý 1000 hồ sơ bệnh nhân (Database Mindset & Xử lý bẫy dữ liệu)
Xử lý Bẫy dữ liệu (Ô trống do bệnh nhân không điền đủ thông tin):

Nguy cơ: Nếu bảng dữ liệu chứa hàng nghìn ô trống (Null), tính năng AutoFilter hoặc các hàm thống kê (COUNTA, VLOOKUP) sẽ dễ bị ngắt quãng, hiểu nhầm là kết thúc bảng hoặc lọc thiếu dữ liệu.

Giải pháp tiêu chuẩn Database:

Tuyệt đối không để ô trống hoàn toàn ở các trường quan trọng. Đối với dữ liệu chữ còn thiếu, chuẩn hóa bằng cách điền giá trị mặc định như "Chưa cập nhật" hoặc "N/A".

Đảm bảo tuân thủ 5 Quy tắc Vàng: Không dùng tính năng Merge Cell trong vùng dữ liệu và duy trì đúng 1 hàng tiêu đề (Header Row) ở dòng đầu tiên.   

Cấu trúc bảng quản lý mẫu (Mô phỏng giao diện minh họa):

Cột A: ID (Ví dụ: P001, P002, P003...)   

Cột B: Họ tên (Ví dụ: Nguyễn Văn A, Trần Thị B...)   

Cột C: Ngày sinh

Cột D: Giới tính (Nam / Nữ)   
JPG

Cột E: SĐT

Cột F: Trạng thái (Đang điều trị, Tái khám, Hoàn tất)   

3. PowerPoint – Slide báo cáo dịch bệnh & Trực quan hóa
Tiêu đề Assertion Title (Mang tính kết luận):

Tiêu đề sai (Chung chung): "Biểu đồ bệnh lý tháng này"

Tiêu đề chuẩn (Assertion Title): "Số hóa bệnh án giúp giảm 40% thời gian chờ đợi và bảo mật tuyệt đối 100% hồ sơ bệnh nhân"

Thiết kế trực quan:

Sử dụng Donut Chart tối giản để phân chia tỷ lệ các nhóm bệnh hoặc trạng thái điều trị của 1000 bệnh nhân.

Tích hợp khu vực hiển thị Checklist Bảo mật y tế (Phân quyền, Mã hóa dữ liệu, Sao lưu định kỳ, Theo dõi truy cập) giúp slide trực quan và súc tích.   
JPG

PHẦN 3. KIỂM THỬ: KHẮC PHỤC LỖI GÁN NHẦM HEADING STYLES BẰNG CTRL + SHIFT + N
1. Nguyên nhân và Hậu quả lỗi gán nhầm Heading
Nguyên nhân: Khi soạn thảo tài liệu SRS, người dùng vô tình bôi đen một đoạn văn bản mô tả triệu chứng hoặc ghi chú dài nhưng lại bấm nhầm vào Heading 1 hoặc Heading 2 trên thanh Ribbon.

Hậu quả: Đoạn văn bản thông thường bị biến thành tiêu đề cấp lớn, làm phình to Mục lục tự động (TOC) một cách vô lý và làm hỏng cấu trúc Navigation Pane của tài liệu.

2. Quy trình xử lý nhanh bằng tổ hợp phím Ctrl + Shift + N
Khi phát hiện đoạn văn bản bị gán nhầm style tiêu đề, bạn chỉ cần thực hiện 2 bước đơn giản sau:

Bước 1 (Chọn vùng bị lỗi): Bôi đen (hoặc đặt con trỏ chuột vào) đoạn văn bản đang bị dính định dạng Heading nhầm.

Bước 2 (Khôi phục Normal Style): Nhấn tổ hợp phím Ctrl + Shift + N.

Tác dụng: Lệnh này lập tức đưa định dạng của đoạn văn bản trở về Normal Style (văn bản thường mặc định của Word), loại bỏ hoàn toàn thuộc tính tiêu đề, giúp loại bỏ đoạn văn đó ra khỏi bảng Mục lục tự động và trả lại sự gọn gàng cho Navigation Pane.
