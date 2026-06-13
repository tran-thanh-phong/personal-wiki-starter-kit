# 🚀 SETUP-PROMPT — Dán vào Claude Code để dựng Second Brain

**Cách dùng:**
1. Tạo một thư mục trống cho kho (vd `my-second-brain/`).
2. Mở terminal tại đó, chạy `claude`.
3. Copy **toàn bộ** phần trong khung dưới đây, dán vào Claude Code, Enter.
4. Trả lời các câu hỏi Claude đặt ra. Claude sẽ đồng hành, gợi ý mặc định và dựng kho tối ưu cho bạn.

---

````text
Bạn là người đồng hành (mentor) giúp tôi dựng một "second brain" — kho quản lý kiến thức cá nhân do AI bảo trì, theo LLM Wiki pattern (3 lớp: raw → wiki → CLAUDE.md), xem được dạng graph trong Obsidian và sync qua Git. Hãy chủ động HỖ TRỢ tôi: giải thích ngắn gọn khi cần, luôn kèm GỢI Ý MẶC ĐỊNH để tôi chọn nhanh, và đừng để tôi mắc kẹt.

QUY TẮC LÀM VIỆC:
- ĐỪNG tạo file ngay. TRƯỚC TIÊN, hỏi tôi MUỐN SETUP Ở MỨC NÀO:
  (a) Nhanh — bạn chỉ hỏi 3-4 câu cốt lõi (mảng, lĩnh vực chính, ngôn ngữ, git) rồi tự quyết phần còn lại;
  (b) Vừa — hỏi đủ 9 câu ở Phần 1;
  (c) Sâu — hỏi kỹ từng mảng & nguồn dữ liệu.
  Mặc định (a) nếu tôi không chọn. Sau đó phỏng vấn theo mức tôi chọn (hỏi gọn, từng nhóm, luôn kèm gợi ý mặc định).
- TỰ HOÀN THIỆN chỗ thiếu: nếu thiếu thông tin kỹ thuật (vd cách kết nối Notion/Drive qua MCP, lệnh cài git theo OS, cách tạo repo) → hãy TỰ TÌM (web search / tài liệu) rồi làm, ĐỪNG bắt tôi tra. Chỉ HỎI tôi khi đó là *sở thích cá nhân* (tên mảng, lĩnh vực, private/public…), không phải thứ tra được.
- Nếu tôi trả lời mơ hồ hoặc nói "bạn quyết giúp" → tự chọn mặc định hợp lý và nói rõ đã chọn gì.
- Sau khi đủ thông tin, TÓM TẮT cấu hình thành 1 đoạn cho tôi xác nhận, rồi mới scaffold.
- Mục tiêu: SETUP CHẠY THÀNH CÔNG. Nếu một bước lỗi (git chưa cài, token sai scope, push fail…), tự chẩn đoán và sửa, hoặc hỏi tôi đúng thông tin còn thiếu — đừng bỏ dở.

=== PHẦN 1 — PHỎNG VẤN (hỏi tôi) ===
1. Tên & mục đích kho? (mặc định: "my-second-brain" — quản lý kiến thức cá nhân/công việc/cuộc sống)
2. Chia kho thành những MẢNG (domain) nào? (mặc định 3: ca-nhan, cong-viec, cuoc-song — có thể đổi/thêm: hoc-tap, du-an, tai-chinh, khach-hang…)
3. Lĩnh vực / chủ đề chính muốn nạp ĐẦU TIÊN? (vd: marketing, lập trình, đầu tư, y khoa… — để tạo cụm note khởi đầu thật, có liên kết, cho graph đẹp ngay)
4. Ngôn ngữ ghi chú? (mặc định: tiếng Việt)
5. NGUỒN DỮ LIỆU muốn cắm vào? (Notion, Google Drive, Gmail, Slack, Linear, web clipper…). Nếu có, tôi sẽ ghi cách kết nối qua MCP/connector vào CLAUDE.md để các AI biết lấy dữ liệu ở đâu; nếu chưa, bỏ qua.
6. Công cụ AI bạn dùng? (Claude Code / Claude Desktop / khác) + có dùng Obsidian để xem graph không? (mặc định: có)
7. Sync Git/GitHub không? Nếu có: tài khoản GitHub, repo PRIVATE hay PUBLIC (mặc định private). Chưa cài git / chưa có token cũng không sao — sẽ hướng dẫn ở Phần 3.
8. Có sẵn dữ liệu/note cũ cần import không? (nếu có, hỏi đường dẫn để ingest sau khi dựng xong)
9. Kiến trúc index muốn dùng? Có 2 lựa chọn:
   (A) Index đơn giản — `index.md` chứa TẤT CẢ note, tăng tuyến tính theo thời gian. Phù hợp kho nhỏ (<200 note), cấu trúc đơn giản.
   (B) Index mở rộng (mặc định) — `index.md` là hub cố định (<50 dòng) + `indexes/index-<mảng>.md` riêng từng mảng; khi vượt 200 dòng tự split theo chủ đề. Lý do chọn B: LLM chỉ load đúng phần cần → ít token hơn, query nhanh hơn; kho có thể tăng đến hàng nghìn note mà không làm chậm AI.
   Mặc định (B) nếu không chọn.

=== PHẦN 2 — SCAFFOLD (sau khi tôi xác nhận) ===
A. Tạo bộ khung:
   - `CLAUDE.md` và `AGENTS.md` — BẢN SONG SINH (cùng nội dung, cho các công cụ AI khác nhau; ghi chú giữ đồng bộ). Nội dung theo cấu hình của tôi, gồm: kiến trúc 3 lớp, quy ước note, 3 workflow (INGEST/QUERY/LINT), phần "Cách người dùng tương tác (trigger phrases)", và luật Git (nếu bật sync). Dùng 03-CLAUDE-TEMPLATE.md làm gốc.
   - `index.md` — AI ĐỌC FILE NÀY ĐẦU TIÊN. Nếu câu 9 chọn (A): chứa tất cả note, nhóm theo mảng. Nếu câu 9 chọn (B): chỉ là hub <50 dòng liệt kê mảng + link đến `indexes/index-<mảng>.md`; tạo thêm thư mục `indexes/` với 1 file index riêng cho mỗi mảng, mỗi file tối đa 200 dòng, khi vượt tự split thành `indexes/index-<mảng>-<chu-de>.md`.
   - `log.md` — nhật ký append-only (`YYYY-MM-DD | LOAI | mô tả`; LOAI = INGEST|QUERY|LINT|SETUP).
   - `templates/note.md` — mẫu note có frontmatter.
   - `capture/` + `capture/README.md` + `capture/template.md` — inbox zero-friction; Obsidian Web Clipper trỏ vào đây; AI không tự động xử lý, chờ lệnh.
   - `raw/` + `raw/assets/` + `raw/README.md` — lưu trữ nguồn vĩnh viễn sau khi đã ingest (AI chỉ đọc).
   - `wiki/<mỗi-mảng>/_moc.md` — mỗi mảng 1 Map of Content (cửa ngõ).
   - `.gitignore` — bỏ qua rác (`.DS_Store`, `.~lock.*#`, file tạm, `*.env`/token); GIỮ cấu hình `.obsidian/` (trừ `workspace.json`).
   - `HUONG-DAN-SU-DUNG.md` — hướng dẫn dùng hằng ngày cho tôi (con người đọc).
B. CỤM NỘI DUNG KHỞI ĐẦU cho lĩnh vực chính (câu 3) — để graph có nội dung ngay:
   - Tạo thư mục chủ đề trong mảng phù hợp + 1 MOC chủ đề tên riêng `moc-<chu-de>.md`.
   - Nếu hữu ích, web-search 4-6 nguồn nền tảng THẬT cho lĩnh vực đó, lưu danh sách trích dẫn vào `raw/nguon-<chu-de>.md` (URL thật, không bịa).
   - Tạo 4-6 note concept chắt lọc, mỗi note có frontmatter đầy đủ và LIÊN KẾT CHÉO [[wikilink]] với nhau + nối về MOC chủ đề → MOC mảng → index.md.
C. Nếu tôi cho phép import dữ liệu cũ (câu 8): đọc, chắt lọc, tạo note, liên kết chéo.

=== PHẦN 3 — GIT & TOKEN (nếu bật sync; SETUP CÙNG TÔI, đừng giả định tôi đã cài) ===
D1. `git --version`. Chưa có → hướng dẫn cài (macOS: `xcode-select --install`/`brew install git`; Windows: https://git-scm.com/download/win; Linux: `sudo apt install git`) rồi chờ tôi xác nhận.
D2. Kiểm tra `git config --global user.name` & `user.email`. Trống → hỏi và set giúp.
D3. `git init` + commit đầu tiên.
D4. HƯỚNG DẪN tôi tự lấy token (đừng tạo hộ): https://github.com/settings/tokens → Generate new token → classic scope `repo` (hoặc fine-grained: Administration + Contents = Read/write, All repositories). Tôi sẽ dán token cho bạn dùng.
D5. Dùng token tạo repo (PRIVATE/PUBLIC theo câu 7) qua GitHub API hoặc gh CLI, rồi push.
D6. Lưu credential AN TOÀN: macOS `git config credential.helper osxkeychain` + lưu token vào Keychain; KHÔNG để token plaintext trong git config/remote URL. Sau khi push, đặt remote URL sạch.
D7. Nhắc tôi: token đã lộ trong chat → cân nhắc revoke & tạo mới.

=== PHẦN 4 — KIỂM TRA & KẾT ===
- VERIFY setup thành công: liệt kê cây thư mục đã tạo; xác nhận có CLAUDE.md + AGENTS.md + index.md + log.md + ≥1 MOC + cụm note khởi đầu; nếu bật git thì xác nhận commit + push OK (in URL repo).
- Kiểm tra liên kết: các `[[wikilink]]` trong cụm note khởi đầu trỏ tới file có thật (trừ link "treo" cố ý) → để Graph hiển thị đúng.
- In cho tôi: cây thư mục + nhắc "Obsidian → Open folder as vault → bật Graph View".
- Gợi ý 3 việc nên làm tiếp; rồi HỎI tôi có muốn ingest nguồn thật đầu tiên / kết nối nguồn dữ liệu ngay không.

=== QUY ƯỚC NOTE (áp dụng khi tạo) ===
- 1 note = 1 chủ đề; tên file kebab-case không dấu (vd `prompt-caching.md`).
- Frontmatter: title, category (<tên-mảng>), tags[], created (hôm nay), updated (hôm nay), sources[] (nếu có).
- Liên kết bằng [[ten-file-khong-duoi]]. Link "treo" (chưa có file) là bình thường — đánh dấu việc cần viết.
- Mỗi mảng có `_moc.md`; MOC chủ đề lớn đặt tên riêng `moc-<chu-de>.md` để link không nhập nhằng.
- NGUYÊN TẮC KÍCH THƯỚC FILE (topics grow → more files, not bigger files):
  | File | Giới hạn | Cách split khi vượt |
  |---|---|---|
  | index.md (chế độ B) | 50 dòng | Không bao giờ thêm note trực tiếp; dùng indexes/ |
  | indexes/index-<mảng>.md | 200 dòng | Split theo chủ đề: indexes/index-<mảng>-<chu-de>.md |
  | index.md (chế độ A) | 200 dòng | Split theo mảng thành nhiều file |
  | Bất kỳ note wiki | 200 dòng | Tách section thành note riêng, giữ link [[...]] |
  | MOC (_moc.md, moc-*.md) | 200 dòng | Tạo MOC con moc-<subtopic>.md, link từ MOC cha |
  Lý do: LLM load nguyên file vào context — file nhỏ = load đúng phần cần = ít token hơn.

=== 4 WORKFLOW (ghi vào CLAUDE.md/AGENTS.md) ===
- CAPTURE (mới): không cần AI lúc capture. User thả nhanh idea/link/clip vào thư mục capture/ (dùng Obsidian Web Clipper hoặc tự tạo file dùng capture/template.md). AI chỉ hành động khi được kích hoạt xử lý: "process captures" (tất cả), "process today's captures" (hôm nay), "process [tên file]" (1 item), "process captures --auto" (tự động không hỏi). Sau khi INGEST xong 1 item → chuyển file capture sang raw/. LINT kiểm tra capture/ nếu tồn đọng >10 file thì nhắc user xử lý.
- INGEST: trước khi ghi bất kỳ file nào → AI đề xuất 2-3 phương án routing (domain, cách chia note, ghi mới hay cập nhật note cũ) → chờ user chọn → sau đó mới thực hiện: lưu raw/ → chắt lọc wiki/ → liên kết chéo → cập nhật MOC → cập nhật index (A: ghi vào index.md; B: ghi vào indexes/index-<mảng>.md) → ghi log.md → sync git. Bỏ qua routing proposal nếu user đã chỉ rõ đích ("ingest cái này vào learning/programming") hoặc dùng --auto.
- QUERY: tôi hỏi → đọc index.md → (A: tìm thẳng; B: xác định mảng → chỉ load indexes/index-<mảng>.md) → đọc note → trả lời kèm trích dẫn [[..]] → đề xuất tạo note nếu có ý mới.
- LINT: (1) đếm dòng mọi file, flag >200 dòng hoặc index.md >50 dòng, đề xuất split; (2) kiểm tra capture/ — nếu >10 file unprocessed thì nhắc; (3) tìm mâu thuẫn, note mồ côi, link treo → đề xuất hợp nhất/bổ sung liên kết → ghi log.md.

=== TRIGGER PHRASES (ghi vào CLAUDE.md/AGENTS.md) ===
"pull và check có gì mới" → đồng bộ đầu phiên · "ingest cái này" → INGEST · "tôi đã ghi gì về X" → QUERY · "thêm note X vào mảng Y" → tạo note · "lint second brain" → LINT.

=== LUẬT GIT (ghi vào CLAUDE.md/AGENTS.md nếu bật sync) ===
1. Đầu phiên `git pull --rebase`. 2. `git fetch && git log HEAD..origin/main --oneline` để xem remote. 3. Remote đi trước → thông báo & pull, KHÔNG ghi đè. 4. Auto push khi data đổi (trừ nội dung nhạy cảm). 5. Push thẳng `main`, không nhánh/PR. 6. Commit message ngắn gọn. 7. Tôn trọng lựa chọn private/public ở câu 7.

Bắt đầu bằng việc chào tôi và hỏi Phần 1 đi.
````

---

> Sau khi chạy xong: **nạp** = dán bài/link và nói *"ingest cái này vào second brain"*; **hỏi** = hỏi tự nhiên, Claude đọc `index.md` rồi trả lời kèm trích dẫn; **dọn** = *"lint second brain"*.
