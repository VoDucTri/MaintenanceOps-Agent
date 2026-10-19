# Nội dung Pitch Deck — MaintenanceOps Agent (10 slide, ~10 phút)

> Đây là **ghi chú nói và Q&A** đi kèm deliverable #7 [`pitch-deck.pdf`](pitch-deck.pdf) (10 trang 16:9, dựng 2026-10-18). Chương 9 chỉ yêu cầu file PDF, nên không nộp `.html` hay `.pptx`. Cấu trúc theo [chương 9 §9.6](guide/chapter-09.md). Mọi con số bên dưới đã kiểm với dữ liệu thô trong repo ngày 2026-10-17; số nào đổi thì sửa ở đây rồi dựng lại PDF.
> Quy tắc slide: 10 slide, chữ ≥ 24 pt, nền trắng, ≤ 80 âm tiết mỗi slide. Phong cách theo 2 mẫu người dùng đưa 2026-10-18 (GrantFinder AI + Campus 24/7): tiêu đề hai tông dạng khẳng định, số liệu lớn, bảng bằng chứng, khung cam cho rủi ro/ca sai — thay quy tắc "≤ 30 từ" của bản trước để slide mang số đo thật như mẫu. Mỗi số trên slide phải có nguồn máy trong repo. "Ghi chú nói" là lời thuyết trình (~1 phút), không đưa lên slide.
> Kiểm PDF: 10 trang 960×540 pt, ≤ 80 âm tiết/trang, chữ nhỏ nhất ≥ 24 pt (`pypdf`), không chữ nào cách mép < 0,15 in (`pymupdf`). Bản 2026-10-18: max 78 âm tiết, min 24,0 pt, mép OK. Tương phản chữ/nền ≥ 4,79:1.

## Slide 1 — Tiêu đề

- **Trên slide:** logo MO + MaintenanceOps Agent · "Đúng người. Đúng mức an toàn. Có truy vết." · "Agent đọc phản ánh của cư dân, kiểm tra an toàn trước rồi giao đúng phòng ban." · nhãn "Dữ liệu mô phỏng (SIM-)" · ảnh màn Cư dân · thanh "NHÓM P-151" + tên 4 thành viên.
- **Ghi chú nói:** giới thiệu tên, nhóm, một câu giá trị. Nói ngay: dữ liệu là mô phỏng.
- **Nguồn:** [README](../README.md).

## Slide 2 — Vấn đề

- **Trên slide:** "Phản ánh đủ kiểu, ca nguy hiểm dễ bị lẫn" · Pain point: ban tiếp nhận tự đọc, phân loại, giao từng phản ánh · 4 thẻ: thiếu vị trí/thiết bị · một tin hai việc · phản ánh trùng · tín hiệu nguy hiểm (cam) · "Giả thuyết nghiệp vụ; chưa có số liệu thực địa".
- **Ghi chú nói:** ai gặp vấn đề (cư dân, ban tiếp nhận, phòng ban), vì sao khó (thiếu vị trí, một phản ánh chứa hai việc, trùng, ca nguy hiểm lẫn trong ca thường). **Không nói số liệu thực địa vì nhóm chưa có**; nói rõ đây là giả thuyết được kiểm bằng dữ liệu mô phỏng.
- **Nguồn:** [01_problem_statement.md](01_problem_statement.md) §A, §F. **Chỗ cần điền nếu có:** số ticket thật, thời gian xử lý thật (chưa có, xem [02_product_brief.md](02_product_brief.md) mục "Bối cảnh, đối thủ").

## Slide 3 — Giải pháp

- **Trên slide:** "Một luồng có trạng thái, an toàn chạy trước" · 5 bước 01 Cư dân gửi → 02 Agent kiểm an toàn → 03 Agent phân loại → 04 Phòng ban xử lý → 05 BQL nghiệm thu (bước Agent tô xanh) · điểm người quyết: Bậc 1 → BQL · Bậc 2 → Tiếp nhận; BQL đóng / trả làm lại · "Agent không đóng, hủy hay gán người" · "Mọi thao tác có audit".
- **Ghi chú nói:** sáu vai (Cư dân, Tiếp nhận, Vệ sinh, Kỹ thuật, Kho, BQL). Agent không đóng, không hủy, không gán nhân viên. Khác biệt: tầng an toàn chạy trước phân loại; mọi thao tác có audit.
- **Nguồn:** [03_lean_prd.md](03_lean_prd.md) §1–§3.

## Slide 4 — Sản phẩm (demo)

- **Trên slide:** "Sáu vai, một nơi theo dõi" · 4 ảnh trong khung trình duyệt: 01 Cư dân gửi · 02 Tiếp nhận · 03 Kỹ thuật · 04 BQL theo dõi · "Web Next.js + PWA điện thoại" · "6 vai dùng chung một dữ liệu".
- **Ghi chú nói:** đi theo một phản ánh "đèn hành lang tầng 12 tắt" qua 6 vai. Nhấn: cư dân thấy trạng thái đơn giản, nhân viên thấy thông tin theo quyền.
- **Nguồn:** ảnh ở [screenshots/](screenshots/README.md); luồng ở [04_ui_flow_wireframe.md](04_ui_flow_wireframe.md) §3.

## Slide 5 — Kiến trúc

- **Trên slide:** "Engine giữ luật, Agent chỉ suy luận" · bảng Thành phần/Vai trò: Portal Next.js + PWA (6 vai, web và điện thoại) · FastAPI (token ký HMAC, phân quyền theo vai) · Engine (10 trạng thái, tầng an toàn, audit, fail closed) · Agent LangGraph (7 node, gpt-6-luna, kiểm danh mục đóng) · PostgreSQL/Supabase (ticket, audit, ảnh trên Storage) · khung "Vì sao LangGraph". Sơ đồ đầy đủ: [Diagrams Components.svg](diagrams/Diagrams%20Components.svg).
- **Ghi chú nói:** vì sao tách engine (luật, trạng thái, audit, fail closed) khỏi Agent (suy luận ngữ nghĩa). Vì sao LangGraph (~20 giây): "Bài toán không phải nhiều agent trò chuyện, mà là một đường quyết định có điều kiện: luật an toàn chạy trước, có thể cắt luồng; model lỗi thì rơi về luật. LangGraph vẽ đúng đường đó thành graph 7 node, mỗi node test riêng được và mọi nhánh lỗi dồn về một fallback." Nhắc **không dán nhãn "GPT-4o", "Phoenix", "LangSmith" như đã chạy**: đang chạy là `gpt-6-luna` và log tự ghi.
- **Nguồn:** [ARCHITECTURE.md](../ARCHITECTURE.md) §2, §10.

## Slide 6 — Cách tiếp cận AI

- **Trên slide:** "Luật giữ sàn, Agent chỉ được nâng mức" · chuỗi Luật sàn → LLM hiểu nghĩa → Kiểm schema → Kiểm danh mục → Đối chiếu luật (khớp `src/maintenance/agent/graph.py`), nhánh "Khẩn cấp ⇒ BQL ngay" và "Lỗi ⇒ về luật" · bảng Luật/Agent trên 91 câu khó: gán đúng 72/91 → 82/90 · recall khẩn cấp 32/38 → 36/37 · đầu vào bất thường 57/66 → 63/65 · chống chèn lệnh 7/7 → 7/7 · trích vị trí 7/9 → 8/9 · "Nhóm tự viết · 1 lần chạy · chưa held-out".
- **Ghi chú nói:** bất biến của nhóm: ngữ nghĩa do LLM hiểu, không vá bằng regex. Ví dụ thật: "m ù i k h é t" (chữ tách) luật cho `NONE`, Agent nâng lên khẩn cấp. Ca Agent sai cũng nêu: `h03` ("tiếng nổ lớn từ phòng điện") chỉ cho `UNCLEAR`.
- **Số đã kiểm:** luật cố định 72/91 (79,1%) → Agent LLM 82/90 (91,1%); ca khẩn cấp 32/38 → 36/37; một lần chạy, bộ câu do nhóm viết.
- **Nguồn:** [evaluation.md](evaluation.md) §7.1; 8 trace thật: [ai-logs.md](ai-logs.md).

## Slide 7 — Điểm nổi bật kỹ thuật

- **Trên slide:** "Kiểm bằng số đo máy, không bằng lời" · 3 ô lớn: 3.852 test pass (Docker, 0 fail) · 92,0% coverage (`src/`; Agent 98,0%) · p95 6,15 s (54 lượt gọi, máy dev) · chip: "CI xanh: ruff + pytest + coverage ≥ 60%" · ≈ 2.551 token/ticket · Docker, Vercel, /health · 242 commit, 26 ngày ([worklog.md](worklog.md)).
- **Ghi chú nói:** chạy trong image Docker đã ghim phiên bản: 3.852 pass, 40 xfail (lỗi đã biết, có cờ), 102 test Postgres chạy riêng. Độ trễ đo trên máy dev, không gồm mạng người dùng. CI: GitHub Actions của tổ chức bị chặn do billing nên CI chạy ở repo mirror công khai [`tuanank2112-crypto/P-151`](https://github.com/tuanank2112-crypto/P-151): workflow "Org CI (public mirror)" lấy từng commit của repo tổ chức, chạy chính `ci.yml` của commit đó và báo trạng thái về commit; khi `main` xanh thì đẩy sang `main` của mirror để Vercel deploy. Nếu bị hỏi "CI có xanh không": có, lượt trên `main` = `5676a4f` (trùng `main` của nhóm) xanh ngày 18/10 — ruff, pytest có coverage ≥ 60%, test thời gian chạy riêng.
- **Đã kiểm 2026-10-18 (API GitHub công khai):** [run 39105089281](https://github.com/tuanank2112-crypto/P-151/actions/runs/39105089281) `success`, head `5676a4f28b91…` = `origin/main`; `ci.yml` của run giống hệt `ci.yml` trên `main` của nhóm; 10 lượt gần nhất (CI + Org CI) đều `success`; `/health` production trả 200 `{"status":"ok","env":"production"}`. Chưa đọc được log chi tiết (số test trong CI) vì tải log cần đăng nhập GitHub.
- **Nguồn:** [evaluation.md](evaluation.md) §5, §7.3; [outputs-20261017/](eval/runs/outputs-20261017/).

## Slide 8 — Video demo

- **Trên slide:** "Xem sản phẩm trong 3 phút" · QR + link <https://youtu.be/WBRYQv9sZlI> · 3:04 · "YouTube · công khai". Không dùng thumbnail YouTube (khung hình giữa animation hiện "0/16 · 0/16", dễ hiểu sai); không mô tả cảnh vì chưa đối chiếu bản YouTube.
- **Ghi chú nói:** video công khai trên YouTube, dùng làm dự phòng khi demo trực tiếp lỗi.
- **Nguồn:** [video-demo.md](video-demo.md). **Chưa đối chiếu:** từng cảnh của bản YouTube (giới thiệu team, ca biên).

## Slide 9 — Thách thức và bài học

- **Trên slide:** "Ghi cả chỗ đã gỡ, lẫn chỗ còn sai" · bảng Thách thức/Cách gỡ: phiên trên serverless → token ký HMAC · DB hết slot kết nối → không giữ pool · Agent trả lời 16–20 s → portal chờ 60 s · khung cam "Agent còn sai": h03 tiếng nổ phòng điện → chỉ "chưa rõ"; f04 trích "Tòa S9" → bị chặn, hỏi lại · bài học: cần nhãn held-out độc lập · LLM hiểu nghĩa, không vá regex · tài liệu bám code.
- **Ghi chú nói:** thách thức thật đã gặp, ghi trong changelog và journal: phiên đăng nhập trên serverless (token ký HMAC), kết nối DB hết slot (`MO_DB_POOL=none`), thời gian chờ Agent 16–20 giây. Nếu làm lại: đo held-out và user test sớm hơn.
- **Nguồn:** [brain4agent/changelog.md](../brain4agent/changelog.md) (v1.17.2, v1.17.3); [journal.md](journal.md) cho dòng thời gian từng tuần.

## Slide 10 — Team và bước tiếp theo

- **Trên slide:** "Nhóm P-151 và việc còn phải đo" · bảng Thành viên/Vai trò: Lê Thị Châm Anh (Trưởng nhóm, Backend) · Lê Như Ý (AI Agent) · Cao Văn Trường (BA/PO) · Võ Đức Trí (Frontend) · Hướng phát triển: held-out độc lập · user test 3–5 người · đo độ trễ bản online · Phoenix/LangSmith · dải "Mục tiêu: không sót ca nguy hiểm, giao đúng phòng ban, mọi bước có truy vết." + "Cảm ơn · Q&A".
- **Ghi chú nói:** bước tiếp đầy đủ: held-out độc lập, user test 3–5 người, đo độ trễ trên bản online, nối Phoenix/LangSmith, kiểm thử tải. Cảm ơn và Q&A.
- **Nguồn:** [README](../README.md) Team; [evaluation.md](evaluation.md) §8.

