# 📚 Giải thích kiến thức: Vì sao Second Brain này hoạt động

Đọc file này khi bạn muốn hiểu *tại sao* hệ thống được thiết kế như vậy — không bắt buộc để dùng, nhưng giúp bạn customize tốt hơn.

## 1. Vấn đề: con người ghét "bookkeeping"
Ai cũng muốn có kho ghi chú gọn gàng, liên kết chặt. Nhưng việc **bảo trì** mới giết chết hầu hết hệ thống: cập nhật liên kết chéo, giữ tóm tắt mới, gỡ mâu thuẫn, dọn note trùng. Con người mệt và quên; **AI thì không** — nó có thể sửa 10-15 file cùng lúc, không bao giờ quên cập nhật link.

→ Ý tưởng cốt lõi: **con người curate nguồn + đặt câu hỏi; AI làm toàn bộ bảo trì.**

## 2. LLM Wiki pattern (Andrej Karpathy)
Khác với RAG (tra lại thông tin mỗi lần hỏi), LLM Wiki coi kho kiến thức là **một artifact bền vững, cộng dồn** mà AI liên tục viết và làm giàu. Nguồn: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f

## 3. Kiến trúc 3 lớp
```
┌─────────────────────────────────────────────┐
│  raw/      Nguồn gốc bất biến (AI chỉ ĐỌC)    │  ← bạn bỏ bài viết, PDF, ảnh, ghi chú thô
├─────────────────────────────────────────────┤
│  wiki/     Tri thức do AI SỞ HỮU & bảo trì    │  ← note .md liên kết chéo, chia theo mảng
├─────────────────────────────────────────────┤
│  CLAUDE.md Schema = LUẬT vận hành             │  ← quy ước + workflow + luật sync
└─────────────────────────────────────────────┘
        +  index.md (mục lục, AI đọc trước)
        +  log.md   (nhật ký append-only)
```

## 4. Ba workflow
- **INGEST (nạp):** đưa nguồn → AI lưu `raw/`, chắt lọc, tạo/cập nhật note trong `wiki/`, thêm `[[liên kết]]`, cập nhật mục lục, ghi log, sync git. *Một nguồn có thể chạm 5–15 note.*
- **QUERY (hỏi):** AI đọc `index.md` → tìm note → trả lời kèm trích dẫn `[[..]]`. Hiểu biết mới đáng giữ → đề xuất tạo note (không để trôi vào chat).
- **LINT (dọn):** định kỳ rà mâu thuẫn, note mồ côi, link treo, đề xuất hợp nhất.

## 5. Vì sao dùng Obsidian + Markdown + Git
- **Markdown** = file `.md` thuần → mở được mọi nơi, không khoá vào app nào.
- **Obsidian** = giao diện đọc/sửa + **Graph View** trực quan hoá mạng `[[wikilink]]` (local-first, miễn phí).
- **Git** = lịch sử phiên bản + đồng bộ nhiều máy + cộng tác, miễn phí với repo private.

## 6. Vì sao đặt luật trong `CLAUDE.md`
Vì luật nằm trong file, **bất kỳ AI/agent nào** đọc nó (Claude Code, Claude Desktop, MCP…) đều vận hành **giống nhau** — đây chính là "context engineering": cấu trúc ngữ cảnh để hành vi nhất quán, linh hoạt cắm vào nhiều nguồn AI.

## 7. Cách customize theo bạn
- **Mảng (domains):** đổi `ca-nhan/cong-viec/cuoc-song` thành bất cứ gì hợp với bạn (vd `hoc-tap`, `khach-hang`, `tai-chinh`).
- **Nguồn dữ liệu:** cắm Notion / Google Drive / Gmail / Slack… qua MCP connector; ghi cách kết nối vào `CLAUDE.md` để AI biết lấy dữ liệu ở đâu.
- **Quy ước note:** giữ "1 note = 1 ý" + liên kết nhiều → graph càng giàu, AI tổng hợp càng tốt.

## Nguồn tham khảo (đọc thêm)
- LLM Wiki — Karpathy: https://gist.github.com/karpathy/442a6bf555914893e9891c11519de94f
- Building a Second Brain — Tiago Forte: https://www.buildingasecondbrain.com/book
- How to Take Smart Notes (Zettelkasten) — Sönke Ahrens: https://www.soenkeahrens.de/en/takesmartnotes
- Evergreen notes — Andy Matuschak: https://notes.andymatuschak.org/Evergreen_notes
- Obsidian: https://obsidian.md/
