# 🚀 SETUP-PROMPT — Dán vào Claude Code để dựng Second Brain

**Cách dùng:**
1. Tạo một thư mục trống cho kho (vd `my-second-brain/`).
2. Mở terminal tại đó, chạy `claude`.
3. Copy **toàn bộ** phần trong khung dưới đây, dán vào Claude Code, Enter.
4. Trả lời các câu hỏi Claude đặt ra. Xong, bạn sẽ có kho hoàn chỉnh.

---

````text
Bạn là người đồng hành giúp tôi dựng một "second brain" — kho quản lý kiến thức cá nhân do AI bảo trì, theo LLM Wiki pattern (raw → wiki → CLAUDE.md), xem được dạng graph trong Obsidian và sync qua Git.

QUAN TRỌNG: ĐỪNG tạo file ngay. TRƯỚC TIÊN hãy PHỎNG VẤN tôi bằng các câu hỏi dưới đây (hỏi gọn, có gợi ý mặc định để tôi chọn nhanh). Sau khi tôi trả lời, hãy tóm tắt lại cấu hình rồi mới scaffold.

=== CÁC CÂU HỎI CẦN HỎI TÔI ===
1. Tên & mục đích kho? (mặc định: "my-second-brain" — quản lý kiến thức cá nhân/công việc/cuộc sống)
2. Bạn muốn chia kho thành những MẢNG nào? (mặc định 3 mảng: ca-nhan, cong-viec, cuoc-song — tôi có thể thêm/bớt, vd: hoc-tap, du-an, tai-chinh)
3. Lĩnh vực / chủ đề chính bạn muốn nạp ĐẦU TIÊN là gì? (vd: marketing, lập trình, y khoa, đầu tư… — để tôi tạo MOC và vài note khởi đầu đúng lĩnh vực)
4. Ngôn ngữ ghi chú? (mặc định: tiếng Việt)
5. Bạn muốn cắm những NGUỒN DỮ LIỆU nào vào kho? (vd: Notion, Google Drive, Gmail, Slack, Linear, web clipper… — nếu có, tôi sẽ ghi chú cách kết nối qua MCP/connector và để chỗ trong CLAUDE.md; nếu chưa, bỏ qua)
6. Bạn dùng công cụ AI nào để làm việc với kho? (Claude Code / Claude Desktop / khác) và có dùng Obsidian để xem graph không? (mặc định: có)
7. Có sync Git/GitHub không? Nếu có: tài khoản GitHub là gì, và muốn repo PRIVATE đúng không? (mặc định: có, private). Lưu ý: nếu chưa cài git hoặc chưa có token, ĐỪNG lo — ở bước sau bạn sẽ hướng dẫn tôi cài git và lấy token GitHub từng bước.
8. Bạn có sẵn dữ liệu/note cũ cần import không? (nếu có, tôi sẽ hỏi đường dẫn và ingest sau)

=== SAU KHI TÔI TRẢ LỜI, HÃY LÀM ===
A. Tóm tắt cấu hình tôi đã chọn (1 đoạn) để tôi xác nhận.
B. Tạo cấu trúc thư mục:
   - `CLAUDE.md`        — schema/luật vận hành (xem mẫu bên dưới, điền theo cấu hình của tôi)
   - `index.md`         — mục lục, nhóm theo mảng, mỗi note 1 dòng tóm tắt; AI đọc file này đầu tiên
   - `log.md`           — nhật ký append-only (mỗi dòng: `YYYY-MM-DD | LOAI | mô tả`; LOAI = INGEST|QUERY|LINT|SETUP)
   - `templates/note.md`— mẫu note có frontmatter
   - `raw/` + `raw/assets/` + `raw/README.md` — nơi để nguồn gốc (AI chỉ đọc)
   - `wiki/<mỗi-mảng>/_moc.md` — mỗi mảng 1 Map of Content (cửa ngõ)
   - `HUONG-DAN-SU-DUNG.md` — hướng dẫn dùng hằng ngày cho tôi
C. Trong lĩnh vực chính tôi chọn (câu 3), tạo 3-5 note khởi đầu thật sự liên kết chéo bằng [[wikilink]] để Obsidian Graph có nội dung; mỗi note có frontmatter (title, category, tags, created, updated, sources) và nối về MOC của mảng.
D. Nếu tôi chọn sync Git, hãy SETUP GIT CÙNG TÔI theo trình tự (đừng giả định tôi đã cài sẵn):
   D1. Kiểm tra git: chạy `git --version`. Nếu CHƯA có, hướng dẫn tôi cài (macOS: `xcode-select --install` hoặc `brew install git`; Windows: tải https://git-scm.com/download/win; Linux: `sudo apt install git`) rồi chờ tôi xác nhận xong.
   D2. Kiểm tra danh tính: `git config --global user.name` và `user.email`. Nếu trống, hỏi tên + email và set giúp tôi.
   D3. `git init` trong thư mục kho + commit đầu tiên.
   D4. Lấy TOKEN GitHub (hướng dẫn tôi từng bước, đừng làm hộ token):
       - Vào https://github.com/settings/tokens → "Generate new token".
       - Loại classic: chọn scope `repo`. (Hoặc fine-grained: quyền Administration + Contents = Read/write, phạm vi All repositories — để tạo được repo mới.)
       - Copy token (dạng `ghp_...` hoặc `github_pat_...`) và dán cho tôi biết để bạn dùng.
   D5. Dùng token tạo repo PRIVATE trên tài khoản tôi (qua GitHub API hoặc gh CLI), rồi push.
   D6. Lưu credential AN TOÀN: macOS → `git config credential.helper osxkeychain` + lưu token vào Keychain; Windows → manager; KHÔNG để token plaintext trong remote URL hay git config. Sau khi push, đặt lại remote URL sạch (không chứa token).
   D7. Nhắc tôi: token vừa dán đã lộ trong chat → nên cân nhắc revoke & tạo mới sau khi xong.
E. In ra cho tôi: cây thư mục đã tạo + 3 việc nên làm tiếp theo.

=== QUY ƯỚC NOTE (áp dụng khi tạo) ===
- 1 note = 1 chủ đề; tên file kebab-case không dấu (vd `prompt-caching.md`).
- Frontmatter:
  ---
  title: ...
  category: <tên-mảng>
  tags: [..]
  created: <hôm nay>
  updated: <hôm nay>
  sources: [raw/...]   # nếu có
  ---
- Liên kết note khác bằng [[ten-file-khong-duoi]]. Link "treo" (chưa có file) là bình thường — đánh dấu việc cần viết.
- Mỗi mảng có 1 note `_moc.md` làm cửa ngõ; MOC theo chủ đề lớn đặt tên riêng `moc-<chu-de>.md` để link không nhập nhằng.

=== 3 WORKFLOW MÀ KHO NÀY VẬN HÀNH (ghi vào CLAUDE.md) ===
- INGEST: tôi đưa nguồn → bạn lưu vào raw/, chắt lọc tạo/cập nhật note trong wiki/, thêm liên kết chéo, cập nhật MOC + index.md, ghi log.md, rồi sync git.
- QUERY: tôi hỏi → bạn đọc index.md, tìm note liên quan, trả lời kèm trích dẫn [[..]]; phát hiện mới đáng giữ thì đề xuất tạo note.
- LINT: tôi nói "dọn dẹp" → bạn tìm mâu thuẫn, note mồ côi, link treo, đề xuất hợp nhất/bổ sung liên kết.

=== LUẬT GIT (ghi vào CLAUDE.md, nếu tôi bật sync) ===
1. Đầu phiên: `git pull --rebase`. 2. Check remote: `git fetch && git log HEAD..origin/main --oneline`.
3. Phát hiện remote đi trước → thông báo & pull trước, KHÔNG ghi đè. 4. Auto push khi data đổi (trừ nội dung nhạy cảm thì hỏi).
5. Push thẳng `main`, không tạo nhánh/PR. 6. Commit message tiếng Việt, ngắn gọn. 7. Repo mới luôn PRIVATE mặc định.

Bắt đầu bằng việc hỏi tôi 8 câu trên đi.
````

---

> Sau khi chạy xong, để **nạp kiến thức**: dán một bài viết / link / ảnh và nói *"ingest cái này vào second brain"*. Để **hỏi**: hỏi tự nhiên, Claude sẽ đọc `index.md` rồi trả lời kèm trích dẫn. Để **dọn dẹp**: nói *"lint second brain"*.
