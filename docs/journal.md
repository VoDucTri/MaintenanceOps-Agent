# Nhật ký phát triển — MaintenanceOps (P-151)

## Week 1: 14/09 - 20/09 (Tìm hiểu vấn đề)

### Mục tiêu tuần này
- [x] Xem pain point có thật không và có đáng làm không
- [x] Viết Problem Statement
- [x] Dựng ít dữ liệu mô phỏng để kiểm tra bài toán có đủ cụ thể

### Đã hoàn thành
- Chốt bài toán: cư dân phản ánh sự cố bảo trì, vệ sinh bằng câu chữ tự do, ban quản lý phải đọc, phân loại rồi giao việc bằng tay
- Viết Problem Statement và một ít dữ liệu mô phỏng

### Khó khăn & Giải pháp
| Khó khăn | Giải pháp | Kết quả |
|----------|-----------|---------|
| Ý tưởng ban đầu là chatbot, nhưng chưa thật sự cần cho vấn đề này | Trao đổi, tìm hiểu thêm rồi bỏ hướng chatbot | Chuyển sang bài toán phân loại và giao việc phản ánh |

### Bài học
- Xác định vấn đề có đáng làm trước, chọn công nghệ sau

### Kế hoạch tuần sau
- [x] Viết MVP, PRD, luồng giao diện, bộ dữ liệu mẫu
- [x] Chốt phạm vi thí điểm nhỏ

---

## Week 2: 21/09 - 27/09 (Chốt MVP)

### Mục tiêu tuần này
- [x] Chốt phạm vi thí điểm nhỏ
- [x] Có bản chạy đầu tiên

### Đã hoàn thành
- Viết MVP, PRD, luồng giao diện và bộ dữ liệu mẫu
- Bản chạy đầu tiên: nhận phản ánh, phân loại, giao việc, cho đính kèm ảnh

### Khó khăn & Giải pháp
| Khó khăn | Giải pháp | Kết quả |
|----------|-----------|---------|
| Mỗi người hình dung sản phẩm hơi khác nhau (giao việc cho từng nhân viên, hay giao cho cả phòng ban) | Thống nhất lấy tài liệu MVP làm chuẩn, bỏ các luồng cũ | Cả nhóm cùng một phạm vi |

### Bài học
- Chốt phạm vi sớm thì code ít lệch spec

### Kế hoạch tuần sau
- [x] Đóng băng baseline v0.3
- [x] Làm giao diện app song song với backend

---

## Week 3: 28/09 - 04/10 (Đóng băng v0.3 và sửa luồng)

### Mục tiêu tuần này
- [x] Chốt baseline v0.3 (hai loại việc: vệ sinh và đèn; Agent chỉ đề xuất)
- [x] Làm giao diện app theo từng vai
- [x] Chốt CR-BPTN-03 (tầng an toàn)
- [x] Lưu dữ liệu bền vững

### Đã hoàn thành
- Baseline v0.3 chốt ngày 28–29/09
- Giao diện app: đăng nhập, màn hình theo vai (cư dân, ban bảo trì, phòng ban, quản lý), màn xem log AI, chế độ tối, hiển thị được trên điện thoại, ảnh đính kèm
- Đổi sang giao thẳng theo phòng ban (CR-BPTN-02), vì bắt ban bảo trì xác nhận mọi phiếu là thừa
- Đầu tháng 10 chốt CR-BPTN-03: tầng an toàn (phát hiện ca khẩn cấp), mức ưu tiên, gộp phiếu trùng, giữ vật tư khi thiếu
- Từ 02/10 dữ liệu lưu trên PostgreSQL/Supabase, không còn mất khi khởi động lại
- 04/10 chạy tay 9 ca trên máy cá nhân: 8 đạt, 1 chưa kiểm được vì khi đó vẫn dùng bộ nhớ tạm

### Khó khăn & Giải pháp
| Khó khăn | Giải pháp | Kết quả |
|----------|-----------|---------|
| Nhiều người sửa song song, merge chồng nhau, xung đột vài lần | Backup trước khi tích hợp, kéo `develop` về nhánh riêng thường xuyên hơn | Tích hợp được các nhánh |

### Bài học
- Thay đổi nghiệp vụ phải ghi thành yêu cầu thay đổi riêng, không sửa lặng lẽ vào bản đã chốt
- Test xanh chưa đủ, phải chạy ca thật

### Kế hoạch tuần sau
- [x] Đưa Agent suy luận vào luồng chính
- [x] Làm lại giao diện theo bản thiết kế mới

---

## Week 4: 05/10 - 11/10 (Agent suy luận và cổng thông tin mới)

### Mục tiêu tuần này
- [x] Đưa Agent suy luận vào luồng chính (tách, gộp phiếu, nhận ra giao nhầm phòng ban)
- [x] Làm lại giao diện thành một cổng thông tin gọi backend thật

### Đã hoàn thành
- Agent suy luận trong luồng chính; đầu ra của model luôn được kiểm lại theo danh mục có sẵn
- Chuyển phần hiểu ngữ nghĩa về an toàn sang Agent, luật cố định chỉ còn là lớp chặn cuối
- Cổng thông tin mới gọi backend thật cho mọi vai, bản chạy trên điện thoại cho các vai vận hành, màn quản lý kho và cổng nghiệm thu
- Chỉnh màn hình theo góp ý khi xem thử (form cư dân hỏi vị trí trước mô tả, mỗi phiếu một khung, danh sách phân trang)
- Gỡ tài khoản và mật khẩu cứng khỏi giao diện, siết quyền xem ảnh
- Cuối tuần có video demo chạy local và ảnh chụp các màn hình

### Khó khăn & Giải pháp
| Khó khăn | Giải pháp | Kết quả |
|----------|-----------|---------|
| Luật cố định bỏ sót câu viết lạ (tách chữ, không dấu, phủ định) | Chuyển phần hiểu ngữ nghĩa sang Agent | Luật chỉ còn là lớp chặn cuối |
| Kho vật tư sinh nhiều lỗi nhất: cùng lúc có phê duyệt, trả lại, huỷ và nhiều phiếu dùng chung tồn kho | Sửa qua nhiều vòng | Số tồn khớp ở cả đường trả lại và huỷ |

### Bài học
- Phần có tiền, kho, quyền cần test cả những đường ít gặp

### Kế hoạch tuần sau
- [x] Bỏ giao diện cũ, dùng một giao diện duy nhất trên PostgreSQL
- [x] Deploy lên Vercel
- [x] Đo chất lượng Agent

---

## Week 5: 12/10 - 18/10 (Triển khai, đo và nộp)

### Mục tiêu tuần này
- [x] Dùng một giao diện duy nhất trên PostgreSQL và deploy lên Vercel
- [x] Đo chất lượng Agent với model thật
- [x] Đủ 10 deliverable theo chương 9 để bàn giao ngày 18/10

### Đã hoàn thành
- Bỏ giao diện cũ; deploy Vercel, đặt vùng chạy gần Supabase nên trung vị API giảm từ khoảng 2,4 s xuống 0,7 s
- Đăng nhập bằng token có chữ ký, không giữ kết nối DB giữa các lần gọi; thử đăng nhập trên production được 12/12
- Chỉnh giao diện theo phản hồi thực tế: danh sách dài cuộn trong khung riêng, bảng việc theo phòng ban gọn hơn, lọc và tìm kiếm ở màn lễ tân, tab đã phân loại, biểu đồ và báo cáo hiệu suất phòng ban, xử lý ca khẩn cấp trùng, tách hai việc cùng vị trí, yêu cầu vật tư, lễ tân bổ sung thông tin thiếu
- 17/10 đo chất lượng: tầng luật cố định bắt đúng 219/219 ca khẩn cấp, phân loại đúng 151/151 câu dev
- 17/10 chạy 91 câu khó với model `gpt-6-luna` thật qua OpenAI API: độ trễ p50 4,8 s, trung bình ~4.250 token/lượt; lưu thành hồ sơ kiểm thử và bộ 8 trace mẫu trong log AI
- 18/10 bàn giao: hướng dẫn vận hành và rollback trong README, sửa cấu hình deploy để Vercel nhận thư mục `portal/`, chuyển CI sang repo mirror công khai
- 18/10 video demo công khai trên YouTube (3:04); CI xanh ở repo mirror đúng commit `main` (`5676a4f`); chú giải tiếng Việt cho trạng thái, mức ưu tiên, mức an toàn trong Problem Statement
- 18/10 nộp `docs/pitch-deck.pdf` (10 trang), sinh lại worklog từ git (263 commit, 28 ngày làm việc), chụp ảnh bằng chứng (Swagger, health, CI, pytest kèm coverage, docker compose ps) vào `docs/screenshots/evidence/`

### Khó khăn & Giải pháp
| Khó khăn | Giải pháp | Kết quả |
|----------|-----------|---------|
| Chạy serverless làm lộ vấn đề đăng nhập giữa các instance không đồng nhất | Token có chữ ký, không giữ kết nối DB giữa các lần gọi | Đăng nhập production 12/12 |
| Giao diện và backend đổi nhiều, phải sửa màn hình liên tục theo thay đổi nghiệp vụ | Chỉnh giao diện theo từng đợt phản hồi | Giao diện đã ổn định để bàn giao |
| GitHub Actions của tổ chức bị chặn do hết hạn mức (billing) | Test và đo ở máy cá nhân; CI chạy ở repo mirror công khai | CI xanh đúng commit `main` (`5676a4f`) |
| Thời gian dồn cuối nên đo với model thật bị trễ so với tiến độ xây tính năng | Đo 91 câu khó ngày 17/10 | Có số đo độ trễ, token và 8 trace; user test 3–5 người và nhãn held-out độc lập chưa làm kịp nên `docs/evaluation.md` ghi rõ là chưa có |

### Bài học
- Đo sớm hơn
- Giao diện càng tinh giản thì trải nghiệm người dùng càng tốt
- Nhãn dữ liệu cần người ngoài gán thì số liệu mới hoàn toàn khách quan
- Deliverable cần có bằng chứng kiểm được (ảnh, số đo, link) ngay khi làm, không để dồn đến ngày nộp

### Kế hoạch tuần sau
- [ ] User test 3–5 người
- [ ] Bộ nhãn held-out do người ngoài gán
- [ ] Đo độ trễ trên bản online
- [ ] Nối Phoenix/LangSmith

---
