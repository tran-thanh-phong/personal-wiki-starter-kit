# Mẫu CLAUDE.md (schema)

> Đây là MẪU. Khi chạy SETUP-PROMPT, Claude sẽ tạo `CLAUDE.md` thật theo cấu hình của bạn.
> Bạn cũng có thể copy nội dung dưới, thay các `<...>` và lưu thành `CLAUDE.md` ở gốc kho.

---

```markdown
# CLAUDE.md — Schema của Second Brain

Đây là **bộ não thứ hai** của <TÊN BẠN>, xây theo *LLM Wiki pattern*: con người **đưa nguồn + đặt câu hỏi**, AI lo **toàn bộ việc bảo trì** (viết note, liên kết chéo, cập nhật mục lục, phát hiện mâu thuẫn). File này là LUẬT vận hành — mọi AI làm việc trong repo PHẢI tuân theo.

Mở vault: Obsidian → "Open folder as vault" → thư mục này. Dùng `[[wikilink]]` để Graph View hiện mạng kiến thức.

## Kiến trúc 3 lớp
1. `raw/` — Nguồn gốc bất biến (bài viết, PDF, ảnh ở `raw/assets/`). AI **chỉ đọc**.
2. `wiki/` — Tri thức do AI bảo trì, chia mảng:
   - `wiki/<mảng-1>/` — <mô tả>
   - `wiki/<mảng-2>/` — <mô tả>
   - `wiki/<mảng-3>/` — <mô tả>
3. `CLAUDE.md` (file này) — Schema.
Hạ tầng: `index.md` (mục lục, đọc đầu tiên), `log.md` (nhật ký append-only), `templates/` (mẫu note).

## Nguồn dữ liệu ngoài (tuỳ chọn — điền nếu có)
- <Notion / Google Drive / Gmail / Slack / Linear …>: kết nối qua MCP connector "<tên>". Khi cần dữ liệu từ đây, AI dùng tool tương ứng để lấy rồi INGEST vào wiki.

## Quy ước note
- 1 note = 1 chủ đề; tên file kebab-case không dấu.
- Frontmatter: title, category (<mảng>), tags[], created, updated, sources[].
- Liên kết bằng `[[ten-file]]`; mỗi mảng có `_moc.md` làm cửa ngõ; MOC chủ đề lớn đặt tên `moc-<chu-de>.md`.

## 3 Workflow
- **INGEST:** lưu nguồn vào `raw/` → chắt lọc, tạo/cập nhật note `wiki/` → liên kết chéo → cập nhật MOC + `index.md` → ghi `log.md` → sync git.
- **QUERY:** đọc `index.md` → tìm note → trả lời kèm trích dẫn `[[..]]` → đề xuất tạo note nếu có ý mới.
- **LINT:** rà mâu thuẫn, note mồ côi, link treo, đề xuất hợp nhất; cập nhật `index.md`.

## Luật đồng bộ Git (nếu bật sync)
1. Đầu phiên `git pull --rebase`. 2. Check: `git fetch && git log HEAD..origin/main --oneline`.
3. Remote đi trước → thông báo & pull, KHÔNG ghi đè. 4. Auto push khi data đổi (trừ nội dung nhạy cảm).
5. Push thẳng `main`, không nhánh/PR. 6. Commit message tiếng Việt, ngắn gọn. 7. Repo mới luôn PRIVATE.

## Nguyên tắc
- Repo private — không đưa nội dung nhạy cảm ra log/tool ngoài.
- Giữ kho nhất quán: mỗi lần đụng vào, cập nhật luôn liên kết + mục lục.
- Con người curate & hỏi; AI làm bookkeeping.
```
