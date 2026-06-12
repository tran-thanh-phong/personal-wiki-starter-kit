# Mẫu HUONG-DAN-SU-DUNG.md

> Đây là MẪU hướng dẫn dùng hằng ngày. Claude sẽ tạo bản riêng cho kho của bạn khi chạy SETUP-PROMPT.

---

```markdown
# Hướng dẫn sử dụng Second Brain

Kho này vận hành theo nguyên tắc: **bạn đưa nguồn + đặt câu hỏi, AI lo bảo trì.**

## 0. Mở kho
- **Obsidian:** Open folder as vault → thư mục này. Bật **Graph View**. (Tuỳ chọn: cài plugin Web Clipper để cắt bài web vào `raw/`.)
- **Claude Code:** mở terminal tại thư mục, chạy `claude`. AI tự đọc `CLAUDE.md`.

## 1. Đầu mỗi phiên — đồng bộ
Nói: **"pull và check có gì mới"**.

## 2. Nạp kiến thức (INGEST)
- Dán nội dung/link và nói: **"ingest cái này vào second brain"**, hoặc
- Bỏ file vào `raw/` rồi nói: **"ingest các nguồn mới trong raw/"**.
→ AI lưu nguồn, tạo/cập nhật note, liên kết chéo, cập nhật mục lục, auto push.

## 3. Hỏi đáp (QUERY)
Hỏi tự nhiên: **"tôi đã ghi gì về <chủ đề>?"**, **"tổng hợp giúp tôi về <X>"**.
→ AI đọc mục lục, trả lời kèm trích dẫn `[[note]]`.

## 4. Thêm note nhanh (INSERT)
- Trong Obsidian: tạo file từ `templates/note.md`, điền frontmatter, đặt vào `wiki/<mảng>/`. Hoặc
- Nói với AI: **"thêm note <chủ đề> vào mảng <tên>"**.

## 5. Dọn dẹp định kỳ (LINT)
Hằng tuần/tháng: **"lint second brain"**.

## 6. Đồng bộ Git
- AI auto push sau ingest/lint. Trên máy khác: `git clone <repo>` → mở Obsidian; nhớ `git pull` trước khi sửa.

## Mẹo
- 1 note = 1 ý; liên kết nhiều → graph càng giàu, AI tổng hợp càng tốt.
- Cứ tạo `[[link]]` kể cả note chưa tồn tại — đó là "việc cần viết".
- Đừng tự sửa `index.md`/MOC bằng tay — để AI làm, tránh lệch.
```
