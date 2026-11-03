# Testing_ZhongGuoXiaoHuozi_Nhom7
49.01.104.084 - Nguyễn Lương Hoàng Long - QA

49.01.104.029 - Hoàng Đạo Duy Đạt - Thiết kế test case

49.101.104.054- Nguyễn Văn Đoàn Bảo Huy - Phân tích yêu cầu 

49.01.104.022 - Phạm Ngọc Duy - Thực hiện kiểm thử
# KẾ HOẠCH KIỂM THỬ NHÁP – TELIET APP

> **Trạng thái:** Bản nháp
> **Học phần:** COMP1307 – Kiểm thử phần mềm cơ bản  
> **Nhóm/Lớp:** Nhóm 7 – 2611COMP130702  
> **Đề tài:** Kiểm thử ứng dụng đặt đồ uống tích điểm trên Android  
> **Đối tượng kiểm thử:** TELIET App – Ứng dụng đặt đồ uống và tích điểm khách hàng  
> **Phiên bản tài liệu yêu cầu:** TELIET_SRS v1.0 (ngày 02/11/2026)  
> **Repository mã nguồn ứng dụng:** https://github.com/HoangLongg17/Coffee-App_TELIET  
> **Repository nộp tài liệu kiểm thử:** https://github.com/HoangLongg17/Testing_ZhongGuoXiaoHuozi_Nhom7  
> **Ngày lập kế hoạch:** 03/11/2026  
> **Hạn nộp tiểu luận:**

---

## 1. Mục đích và mục tiêu kiểm thử

### 1.1. Mục đích

Lập kế hoạch cho hoạt động kiểm thử chức năng của TELIET App trên Android, căn cứ theo TELIET_SRS v1.0 và phạm vi đã đăng ký trong Phiếu đăng ký đề tài của Nhóm 7. Kế hoạch này xác định phạm vi, cách tiếp cận, điều kiện thực hiện, rủi ro, phân công và lịch trình để các thành viên phối hợp thực hiện.

### 1.2. Mục tiêu

1. Kiểm tra chức năng đăng ký và đăng nhập đáp ứng các điều kiện dữ liệu đầu vào và xác thực đã mô tả trong SRS.
2. Kiểm tra việc hiển thị sản phẩm, tìm kiếm theo tên và lọc theo danh mục.
3. Kiểm tra thông tin chi tiết sản phẩm, lựa chọn size/số lượng, thao tác giỏ hàng và tính tổng tiền.
4. Kiểm tra luồng đặt hàng: điều kiện người dùng, thông tin cửa hàng/phương thức nhận hàng/thời gian và dữ liệu đơn hàng được lưu.
5. Kiểm tra quy tắc DRIPS: tính theo tổng tiền trước khuyến mãi, chỉ cộng khi xác nhận đã nhận hàng và không cộng khi đơn bị hủy.
6. Ghi nhận, phân loại, theo dõi lỗi và tổng hợp kết quả kiểm thử làm căn cứ đánh giá chất lượng trong phạm vi đã chọn.

### 1.3. Căn cứ và giới hạn quyền kiểm thử

**“Tự xây dựng”**. Nhóm thực hiện kiểm thử trên bản ứng dụng và môi trường/dữ liệu thử nghiệm thuộc phạm vi nhóm được phép sử dụng. Không kiểm thử phá hoại, không truy cập hoặc thay đổi dữ liệu người dùng thật, không chạy kiểm thử trên môi trường production khi chưa có sự cho phép riêng.

## 2. Phạm vi kiểm thử

### 2.1. Trong phạm vi

Kiểm thử trên ứng dụng Android, tập trung vào 5 chức năng được ghi trong Phiếu đăng ký đề tài:

| STT | Chức năng | Nội dung kiểm thử chính | Căn cứ SRS |
|---:|---|---|---|
| 1 | Đăng ký và đăng nhập | Dữ liệu bắt buộc; email/mật khẩu hợp lệ hoặc không hợp lệ; đăng ký thành công/thất bại; đăng nhập thành công/thất bại; điều hướng sau xác thực. | FR-01, FR-02 |
| 2 | Xem, tìm kiếm và lọc sản phẩm | Danh sách sản phẩm; tìm theo tên; lọc theo danh mục; trường hợp không có kết quả; cập nhật danh sách khi đổi danh mục. | FR-03, FR-04 |
| 3 | Chi tiết sản phẩm và giỏ hàng | Thông tin sản phẩm; giá theo size; ưu tiên size mặc định M, sau đó S rồi L; chọn số lượng; thêm/sửa/xóa; gộp cùng productId và size; tính tổng tiền. | FR-05, FR-06; mục 8.1 |
| 4 | Đặt hàng | Chặn đặt hàng khi chưa đăng nhập; chọn cửa hàng và phương thức nhận hàng; kiểm tra thời gian nhận hàng; tạo đơn hàng trong Firestore với các trường theo SRS; trạng thái ban đầu là Đang chờ. | FR-08, FR-09; mục 8.4 |
| 5 | Tích điểm DRIPS | Tính điểm theo totalBeforeDiscount; cập nhật drips và totalSpent khi xác nhận nhận hàng; không cộng điểm đối với đơn đã hủy. | FR-10, FR-11; mục 8.3 |

**Lưu ý về phạm vi:** Việc kiểm tra chuyển trạng thái đơn hàng từ `Đang chờ` sang `Đã nhận hàng` hoặc `Đã hủy` được thực hiện ở mức cần thiết để xác minh quy tắc tích điểm DRIPS. Đây không phải là kiểm thử toàn diện mọi chức năng quản lý đơn hàng.

### 2.2. Ngoài phạm vi

- Thanh toán trực tuyến qua cổng ngân hàng hoặc ví điện tử; SRS hiện mô tả phương thức thanh toán tại quầy.
- Kiểm thử chuyên sâu hệ thống phân quyền quản trị viên.
- Quản lý kho tồn hàng đầu vào.
- Chat, AI hoặc nhắn tin nội bộ.
- Báo cáo doanh thu và thống kê quản trị chi tiết.
- Phân loại thành viên/cấp bậc khách hàng mở rộng.
- Kiểm thử riêng chuyên sâu toàn bộ quy tắc khuyến mãi fixed/percent/gift. Dữ liệu khuyến mãi chỉ được xem xét khi cần xác minh dữ liệu đơn hàng và tổng tiền trước khuyến mãi cho DRIPS.
- Kiểm thử trên iOS và Web; phạm vi đề tài đăng ký là ứng dụng Android.
- Kiểm thử tải/hiệu năng chuyên sâu, kiểm thử xâm nhập và đánh giá bảo mật chuyên sâu.

## 3. Cách tiếp cận và phương pháp kiểm thử

### 3.1. Cách tiếp cận

- **Kiểm thử dựa trên yêu cầu:** đối chiếu ca kiểm thử với các FR và quy tắc nghiệp vụ tương ứng trong TELIET_SRS v1.0.
- **Kiểm thử hộp đen:** áp dụng phân vùng tương đương (EP) và phân tích giá trị biên (BVA) cho email, mật khẩu, số lượng, giá trị đơn hàng và tổng tiền trước khuyến mãi dùng tính DRIPS.
- **Bảng quyết định/chuyển trạng thái:** kiểm tra điều kiện đăng nhập, quy tắc gộp giỏ hàng, điều kiện đặt hàng và chuyển trạng thái nhận hàng/hủy đơn liên quan đến DRIPS.
- **Kiểm thử hộp trắng:** tập trung các hàm/logic đã nêu trong Phiếu đăng ký: kiểm tra đăng ký/đăng nhập; tìm kiếm/lọc; lấy giá theo size; thêm sản phẩm vào giỏ; cập nhật số lượng; tính tổng tiền giỏ hàng; tính DRIPS; xác nhận nhận hàng và cập nhật điểm/tổng tiền.
- **Kiểm thử theo lớp:** Unit Test cho logic độc lập; UI Test cho thao tác trên Android; Integration Test cho tương tác Firebase Authentication/Firestore; Regression Test cho luồng đã kiểm thử sau khi sửa lỗi.
- **Ưu tiên theo rủi ro:** ưu tiên xác thực, dữ liệu đơn hàng, giỏ hàng và DRIPS vì sai sót có thể ảnh hưởng đến quyền đặt hàng, số tiền hoặc điểm khách hàng.

### 3.2. Công cụ dự kiến

| Hạng mục | Công cụ theo Phiếu đăng ký | Mục đích |
|---|---|---|
| Unit Test | Jest + jest-expo | Kiểm thử logic kiểm tra dữ liệu, giỏ hàng, tính tổng tiền và DRIPS. |
| UI Test | Maestro | Tự động hóa thao tác giao diện Android cho các luồng đã chọn. |
| API/Integration | Firebase Emulator Suite | Kiểm thử tích hợp Firebase Authentication và Firestore trong môi trường thử nghiệm. |
| CI | GitHub Actions | Tự động chạy các bước kiểm thử phù hợp khi có cập nhật mã nguồn. |
| Quản lý lỗi | GitHub Issues | Ghi nhận mô tả lỗi, bước tái hiện, kết quả mong đợi/thực tế, mức độ và trạng thái xử lý. |

Các công cụ trên là công cụ **dự kiến** theo Phiếu đăng ký; nhóm cần kiểm tra cấu hình và script thực tế của repository trước khi thiết lập chạy tự động.

### 3.3. Dữ liệu kiểm thử trọng tâm

| Trường/đối tượng | Dữ liệu hoặc điểm kiểm tra dự kiến | Mục đích |
|---|---|---|
| Email | Bỏ trống, sai định dạng, hợp lệ; tài khoản tồn tại/không tồn tại khi đăng nhập | EP và kiểm tra xác thực |
| Mật khẩu | Bỏ trống, thông tin sai, thông tin hợp lệ | EP và kiểm tra xác thực; không tự đặt giới hạn độ dài vì SRS chưa nêu |
| Từ khóa/danh mục | Từ khóa có kết quả/không có kết quả; các danh mục TRÀ SỮA, FREEZE, CÀ PHÊ, TRÀ, KHÁC | Kiểm tra tìm kiếm và lọc |
| Size sản phẩm | S, M, L; sản phẩm thiếu một hoặc nhiều mức giá; kiểm tra ưu tiên M → S → L | Kiểm tra giá theo size |
| Số lượng | 0, 1, 2; giảm số lượng về 0 | Kiểm tra biên và quy tắc xóa khỏi giỏ |
| Tổng tiền trước khuyến mãi | 9.999, 10.000, 10.001; 19.999, 20.000, 20.001 VNĐ | Kiểm tra ranh giới công thức DRIPS |
| Đơn hàng/trạng thái | Đang chờ, Đã nhận hàng, Đã hủy | Kiểm tra chuyển trạng thái và điều kiện cộng điểm |

SRS không quy định giới hạn chiều dài mật khẩu hoặc mọi ràng buộc số học khác; nhóm không tự xem các giới hạn chưa được đặc tả là tiêu chí chính thức.

## 4. Tiêu chí đầu vào và đầu ra

### 4.1. Tiêu chí đầu vào (Entry Criteria)

Chỉ bắt đầu vòng kiểm thử chính khi đáp ứng các điều kiện sau:

1. TELIET_SRS v1.0 và Phiếu đăng ký đề tài đã được nhóm thống nhất làm căn cứ kiểm thử.
2. Có bản ứng dụng TELIET có thể cài đặt/chạy trên thiết bị Android hoặc Android Emulator.
3. Có môi trường Firebase thử nghiệm được nhóm cho phép sử dụng (Firebase Emulator Suite hoặc dự án phát triển riêng); không dùng dữ liệu người dùng thật khi chưa được cho phép.
4. Có dữ liệu mẫu cần thiết cho sản phẩm, tài khoản, giỏ hàng và đơn hàng; có tài khoản thử nghiệm cho luồng đăng ký/đăng nhập.
5. Các thành viên có quyền truy cập repository mã nguồn và repository kiểm thử của Nhóm 7.
6. Các công cụ dự kiến đã được cài đặt/cấu hình ở mức cần thiết; có người phụ trách và cách ghi nhận lỗi.

### 4.2. Tiêu chí đầu ra (Exit Criteria)

Kết thúc vòng kiểm thử khi:

1. Tất cả ca kiểm thử đã được duyệt trong phạm vi 5 chức năng được thực thi hoặc được ghi rõ lý do chưa thể thực thi.
2. Mỗi ca kiểm thử có kết quả Pass/Fail/Blocked và bằng chứng phù hợp (ảnh chụp, log hoặc dữ liệu kiểm tra).
3. Lỗi phát hiện được ghi nhận trên GitHub Issues, có mức độ ưu tiên, bước tái hiện và người theo dõi.
4. Không còn lỗi mức nghiêm trọng/chặn (Blocker/Critical) chưa được xử lý hoặc chưa có quyết định chấp nhận rủi ro của nhóm.
5. Các lỗi mức cao còn tồn tại (nếu có) được mô tả rõ, đánh giá ảnh hưởng và báo cáo trong kết quả kiểm thử.
6. Hoàn thành báo cáo tổng kết gồm phạm vi thực tế, số ca đã chạy, số Pass/Fail/Blocked, danh sách lỗi và các giới hạn còn lại.

## 5. Rủi ro kiểm thử

Thang điểm sơ bộ:
- **K – Khả năng xảy ra:** 1 (hiếm) đến 5 (rất thường xuyên).
- **A – Ảnh hưởng:** 1 (rất thấp) đến 5 (rất nghiêm trọng).
- **Điểm rủi ro = K × A.** Mức tham khảo: 1–4 thấp; 5–9 trung bình; 10–16 cao; 17–25 rất cao.

| STT | Rủi ro | K | A | K × A | Mức | Biện pháp giảm thiểu |
|---:|---|---:|---:|---:|---|---|
| 1 | Firebase Authentication/Firestore hoặc cấu hình môi trường thử nghiệm không sẵn sàng, làm gián đoạn đăng ký, đăng nhập và lưu đơn hàng. | 3 | 5 | 15 | Cao | Chuẩn bị Firebase Emulator/dự án test trước; kiểm tra kết nối và quyền truy cập; chuẩn bị dữ liệu thử nghiệm dự phòng; ghi log lỗi môi trường riêng với lỗi ứng dụng. |
| 2 | Dữ liệu tài khoản thiếu/sai hoặc xử lý email, mật khẩu không đúng, dẫn đến đăng ký/đăng nhập sai hoặc không hiển thị thông báo phù hợp. | 3 | 4 | 12 | Cao | Thiết kế EP cho dữ liệu trống, sai định dạng và hợp lệ; dùng tài khoản thử nghiệm; kiểm tra cả kết quả xác thực và thông báo trên UI. |
| 3 | Dữ liệu sản phẩm thiếu Name, Category hoặc Sizes/giá theo size, khiến danh sách/chi tiết sản phẩm hiển thị sai hoặc phát sinh lỗi. | 3 | 4 | 12 | Cao | Chuẩn bị dữ liệu mẫu có đủ trường và dữ liệu thiếu trường; kiểm tra null-safe; kiểm tra giá theo thứ tự ưu tiên M → S → L. |
| 4 | Logic giỏ hàng gộp sai sản phẩm/size, xử lý số lượng bằng 0 không đúng hoặc tính tổng tiền sai. | 3 | 4 | 12 | Cao | Viết ca kiểm thử cùng id+cùng size, cùng id+khác size, khác id; kiểm tra số lượng 0/1/2 và đối chiếu tổng unitPrice × quantity. |
| 5 | Đặt hàng khi thiếu đăng nhập hoặc thiếu store/method/time; đơn hàng thiếu trường bắt buộc hoặc trạng thái ban đầu không đúng. | 3 | 5 | 15 | Cao | Kiểm tra guest và người dùng đã đăng nhập; thử dữ liệu null/thiếu; đối chiếu document Orders với danh sách trường và trạng thái trong SRS; chỉ chạy trên môi trường test được phép. |
| 6 | Tính DRIPS sai do dùng total sau khuyến mãi thay vì totalBeforeDiscount, sai mốc 10.000 VNĐ hoặc cộng điểm cho đơn đã hủy. | 4 | 5 | 20 | Rất cao | Kiểm tra BVA quanh các mốc 10.000; xác minh nguồn totalBeforeDiscount; kiểm tra nhánh Đang chờ → Đã nhận hàng và Đang chờ → Đã hủy; đối chiếu drips và totalSpent sau xử lý. |

## 6. Phân công thành viên

| Thành viên | Vai trò theo phiếu | Phân công đề xuất |
|---|---|---|
| Nguyễn Lương Hoàng Long – 49.01.104.084 | Trưởng nhóm | Điều phối kế hoạch và tiến độ; rà soát SRS/phạm vi; tham gia vào các hoạt động kiểm thử; tổng hợp kết quả; kiểm tra Pull Request và bản nộp cuối. |
| Hoàng Đạo Duy Đạt – 49.01.104.029 | Thành viên | Thiết kế và thực hiện kiểm thử đăng ký/đăng nhập; chuẩn bị dữ liệu tài khoản; ghi nhận lỗi liên quan xác thực. |
| Phạm Ngọc Duy – 49.01.104.022 | Thành viên | Thiết kế và thực hiện kiểm thử tìm kiếm/lọc, chi tiết sản phẩm và giỏ hàng; kiểm tra giá size, số lượng và tổng tiền. |
| Nguyễn Văn Đoàn Bảo Huy – 49.01.104.054 | Thành viên | Thiết kế và thực hiện kiểm thử đặt hàng và DRIPS; kiểm tra document đơn hàng, trạng thái, drips và totalSpent. |

Tất cả thành viên cùng tham gia review ca kiểm thử, chạy Regression Test khi có bản sửa lỗi và hoàn thiện báo cáo. Trưởng nhóm theo dõi các công việc bị trễ hoặc bị chặn.

## 7. Lịch trình và mốc đến hạn nộp tiểu luận

| Mốc | Thời điểm tương đối | Công việc | Sản phẩm bàn giao |
|---|---|---|---|
| 1 | D-14 đến D-12 | Chốt phạm vi, đọc SRS, xác nhận môi trường và phân công | Kế hoạch kiểm thử nháp được nhóm review |
| 2 | D-11 đến D-9 | Thiết kế checklist/ca kiểm thử; chuẩn bị dữ liệu và tài khoản test | Danh sách ca kiểm thử và dữ liệu test |
| 3 | D-8 đến D-6 | Thực hiện Unit/UI/Integration Test cho đăng ký, đăng nhập, tìm kiếm, sản phẩm và giỏ hàng | Kết quả chạy test, bằng chứng và GitHub Issues |
| 4 | D-5 đến D-4 | Kiểm thử đặt hàng, trạng thái đơn và DRIPS; kiểm tra các giá trị biên | Kết quả test đặt hàng/DRIPS, lỗi được cập nhật |
| 5 | D-3 | Sửa lỗi trong khả năng, chạy Regression Test và rà soát phần còn tồn tại | Kết quả Regression Test, danh sách lỗi còn mở |
| 6 | D-2 | Hoàn thiện báo cáo, đối chiếu yêu cầu và rà soát hình thức | Bản tiểu luận dự thảo được nhóm duyệt |
| 7 | D-1 | Trưởng nhóm kiểm tra lần cuối, kiểm tra file và liên kết GitHub | Bản nộp cuối đã sẵn sàng |
| 8 | D – [ngày hạn nộp chính thức] | Nộp tiểu luận theo hướng dẫn của giảng viên | Tiểu luận được nộp đúng hạn |

## 8. Quản lý lỗi trên GitHub

- **Repository kiểm thử của nhóm:** https://github.com/HoangLongg17/Testing_ZhongGuoXiaoHuozi_Nhom7
- **Repository mã nguồn ứng dụng:** https://github.com/HoangLongg17/Coffee-App_TELIET
- **Quản lý lỗi:** tạo GitHub Issue cho mỗi lỗi; tiêu đề ngắn gọn; mô tả môi trường, điều kiện tiên quyết, bước tái hiện, kết quả mong đợi, kết quả thực tế, bằng chứng và mức độ ảnh hưởng.

## Lịch sử phiên bản

| Phiên bản | Ngày | Nội dung |
|---|---|---|
| 0.1 | 03/11/2026 | Kế hoạch kiểm thử nháp |
