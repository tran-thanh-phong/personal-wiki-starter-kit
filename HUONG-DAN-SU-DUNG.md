# Hướng dẫn sử dụng Second Brain

Kho này vận hành theo *LLM Wiki pattern*: **bạn đưa nguồn + đặt câu hỏi, AI lo phần bảo trì.** Dưới đây là cách dùng tối ưu hằng ngày.

## 0. Mở kho
- **Obsidian:** Open folder as vault → chọn `my-second-brain`. Bật **Graph View** để thấy mạng note. Cài plugin **Web Clipper** để cắt bài viết web thành markdown bỏ vào `raw/`.
- **Claude Code / AI:** mở terminal tại thư mục `my-second-brain` rồi chạy `claude`. AI tự đọc `CLAUDE.md` để biết luật.

## 1. Đầu mỗi phiên — đồng bộ
Nói với AI: **"pull và check có gì mới"**. AI sẽ:
```
git pull --rebase
git fetch && git log HEAD..origin/main --oneline
```

## 2. Nạp kiến thức mới (INGEST)
Hai cách:
- Dán nội dung / link và nói: **"ingest cái này vào second brain"**.
- Tự bỏ file vào `raw/` (hoặc dùng Web Clipper) rồi nói: **"ingest các nguồn mới trong raw/"**.

AI sẽ: lưu nguồn vào `raw/` → chắt lọc, tạo/cập nhật note trong `wiki/` → thêm liên kết `[[...]]` → cập nhật `index.md` + MOC → ghi `log.md` → **auto push git**.

## 3. Hỏi đáp (QUERY)
Hỏi tự nhiên: **"tôi đã ghi gì về tài chính cá nhân?"**, **"tổng hợp giúp tôi về dự án X"**.
AI đọc `index.md` → tìm note → trả lời kèm trích dẫn `[[note]]`. Nếu sinh ra hiểu biết mới đáng giữ, AI đề xuất tạo note để không trôi mất.

## 4. Tự thêm thông tin nhanh (INSERT)
- Trong Obsidian: tạo file mới từ `templates/note.md`, điền frontmatter, đặt vào `wiki/<mảng>/`.
- Hoặc nói với AI: **"thêm note <chủ đề> vào mảng công việc"** — AI tạo đúng format và liên kết hộ.

## 5. Dọn dẹp định kỳ (LINT)
Mỗi tuần/tháng nói: **"lint second brain"**. AI rà mâu thuẫn, note mồ côi, link treo, đề xuất hợp nhất/bổ sung liên kết.

## 6. Đồng bộ git
- AI **auto push** sau mỗi ingest/lint (đã cấu hình token trong macOS Keychain).
- Trên máy khác: `git clone https://github.com/<tai-khoan>/<ten-kho>.git` rồi mở bằng Obsidian. Nhớ `git pull` trước khi sửa.

## Mẹo dùng tối ưu
- **1 note = 1 ý.** Note nhỏ, liên kết nhiều → Graph View càng giàu, AI càng dễ tổng hợp.
- Cứ tạo link `[[...]]` kể cả note chưa tồn tại — đó là "việc cần viết".
- Đừng tự đi cập nhật `index.md`/MOC bằng tay — để AI làm, tránh lệch.
- Cắm vào nhiều nguồn AI: vì luật nằm trong `CLAUDE.md`, bất kỳ agent nào đọc file đó đều vận hành giống nhau.

## Cấu trúc thư mục
```
my-second-brain/
├── CLAUDE.md              # schema / luật vận hành (AI đọc trước)
├── index.md              # mục lục mọi note
├── log.md                # nhật ký ingest/query/lint
├── HUONG-DAN-SU-DUNG.md  # file này
├── templates/note.md     # mẫu note
├── raw/                  # nguồn gốc bất biến (+ assets/)
└── wiki/                 # note do AI bảo trì
    ├── ca-nhan/   (_moc + note)
    ├── cong-viec/ (_moc + note)
    └── cuoc-song/ (_moc + note)
```
