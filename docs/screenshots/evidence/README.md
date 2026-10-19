# Ảnh bằng chứng nộp bài

Chụp ngày 2026-10-19 trên `develop` (`f5a3826`). Ảnh 01–03 chụp tự động bằng Chrome headless từ địa chỉ công khai, ảnh 04–05 dựng từ output máy của lệnh ghi trong ảnh (không sửa tay).

| # | Ảnh | Chứng minh | Ghi chú |
|---|---|---|---|
| 1 | [01-api-docs-swagger.png](01-api-docs-swagger.png) | API backend đang chạy và có tài liệu | <https://p151-backend.vercel.app/docs>, lấy phần đầu trang |
| 2 | [02-health-endpoint.png](02-health-endpoint.png) | Health check production | `{"status":"ok","env":"production"}` |
| 3 | [03-ci-green-public-mirror.png](03-ci-green-public-mirror.png) | CI xanh | Repo mirror công khai [`tuanank2112-crypto/P-151`](https://github.com/tuanank2112-crypto/P-151/actions); lượt "CI #6" là commit `5676a4f` = `main` của nhóm. Actions của repo tổ chức bị chặn billing nên CI chạy ở mirror |
| 4 | [04-pytest-coverage-ruff.png](04-pytest-coverage-ruff.png) | Test, coverage, lint | `3850 passed, 40 xfailed`, coverage 92,02% (ngưỡng 60%), `ruff check` exit 0. Máy dev, `LLM_MODE=mock`; 104 test bị loại là 102 test Postgres và 2 test thời gian (chạy riêng như CI) |
| 5 | [05-docker-compose-ps.png](05-docker-compose-ps.png) | Docker Compose chạy được | `backend` và `db` ở trạng thái `healthy`, `portal` chạy; `/health` local trả 200 (`env: development`) |

Chưa có: ảnh LangSmith/Phoenix (chưa nối), ảnh trace Agent (8 trace nằm dạng văn bản trong [../../ai-logs.md](../../ai-logs.md)).
