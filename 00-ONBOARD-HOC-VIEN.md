# 🧠 Onboard: Tự xây Second Brain Wiki bằng Claude Code

Chào bạn! Đây là bộ "starter kit" để bạn **tự tái tạo một kho kiến thức (second brain)** giống mô hình trong lớp — một nơi quản lý kiến thức cá nhân / công việc / cuộc sống, do **AI tự bảo trì**, xem được dạng **graph trong Obsidian**, và **đồng bộ qua Git**.

## Bạn sẽ có gì sau 15 phút
- Một thư mục kho kiến thức với cấu trúc 3 lớp: `raw/` (nguồn gốc) → `wiki/` (note do AI bảo trì) → `CLAUDE.md` (luật vận hành).
- File `index.md` (mục lục), `log.md` (nhật ký), `templates/` (mẫu note), `HUONG-DAN-SU-DUNG.md`.
- Tuỳ chọn: repo GitHub **private** + tự động sync.
- Mở bằng Obsidian để thấy mạng kiến thức dạng graph.

## Cách hoạt động (1 câu)
Bạn **đưa nguồn + đặt câu hỏi**, còn AI lo **toàn bộ việc bảo trì**: viết note, liên kết chéo, cập nhật mục lục, phát hiện mâu thuẫn. (Đây là *LLM Wiki pattern* — xem [02-GIAI-THICH-KIEN-THUC.md](02-GIAI-THICH-KIEN-THUC.md).)

## Các bước
1. **Cài công cụ:** [Claude Code](https://claude.com/claude-code) (CLI) và [Obsidian](https://obsidian.md/) (miễn phí). Muốn sync nhiều máy thì cần **Git** + tài khoản **GitHub** — *chưa có cũng không sao*: trong lúc chạy SETUP-PROMPT, Claude sẽ hướng dẫn bạn cài Git và lấy **token GitHub** từng bước (xem mục "Chuẩn bị Git & token" bên dưới).
2. **Tạo thư mục trống** cho kho, ví dụ `my-second-brain/`, rồi mở terminal tại đó và chạy `claude`.
3. **Dán SETUP-PROMPT:** mở [01-SETUP-PROMPT.md](01-SETUP-PROMPT.md), copy toàn bộ phần trong khung và dán vào Claude Code.
4. **Trả lời các câu hỏi** mà Claude đặt (về mảng kiến thức, lĩnh vực, nguồn dữ liệu, công cụ AI, Git…). Claude sẽ tự dựng toàn bộ cấu trúc theo câu trả lời của bạn.
5. **Mở Obsidian** → "Open folder as vault" → chọn thư mục kho → bật **Graph View**.
6. **Bắt đầu dùng:** đọc [04-HUONG-DAN-SU-DUNG-TEMPLATE.md](04-HUONG-DAN-SU-DUNG-TEMPLATE.md) (Claude cũng sẽ tạo bản riêng cho bạn).

## Chuẩn bị Git & token (chỉ cần nếu muốn sync GitHub)
Bạn có thể để Claude hướng dẫn ngay trong lúc setup, hoặc làm trước theo các bước sau:

1. **Cài Git** (nếu chưa có — kiểm tra bằng `git --version`):
   - macOS: `xcode-select --install` hoặc `brew install git`
   - Windows: tải tại https://git-scm.com/download/win
   - Linux: `sudo apt install git`
2. **Tạo tài khoản GitHub** (miễn phí): https://github.com/signup
3. **Lấy Personal Access Token (PAT):**
   - Vào https://github.com/settings/tokens → **Generate new token**.
   - Token *classic*: tick scope **`repo`**. (Hoặc *fine-grained*: quyền **Administration** + **Contents** = Read/write, phạm vi **All repositories** — để tạo được repo mới.)
   - **Copy token** (dạng `ghp_...` hoặc `github_pat_...`) và giữ lại — sẽ đưa cho Claude khi setup.
4. Khi chạy SETUP-PROMPT, Claude sẽ: dùng token tạo repo **private**, push, và **lưu token an toàn vào trình quản lý mật khẩu hệ thống** (không để plaintext).

> ⚠️ Bảo mật: token = mật khẩu. Đừng commit token vào repo, đừng chia sẻ công khai. Sau khi setup xong nên cân nhắc revoke token cũ và tạo mới nếu nó từng hiển thị ở nơi không an toàn.

## Bộ file trong kit này
| File | Dùng để |
|---|---|
| `00-ONBOARD-HOC-VIEN.md` | Bạn đang đọc — tổng quan & các bước |
| `01-SETUP-PROMPT.md` | **Prompt chính** dán vào Claude Code để dựng kho |
| `02-GIAI-THICH-KIEN-THUC.md` | Hiểu *vì sao* hệ thống này hoạt động (LLM Wiki, 3 lớp, workflow) |
| `03-CLAUDE-TEMPLATE.md` | Mẫu `CLAUDE.md` (luật vận hành) — Claude sẽ tuỳ biến từ đây |
| `04-HUONG-DAN-SU-DUNG-TEMPLATE.md` | Mẫu hướng dẫn dùng hằng ngày |

> Mẹo: Không cần hiểu hết kỹ thuật. Cứ chạy SETUP-PROMPT, trả lời câu hỏi, là có kho riêng. Phần "giải thích kiến thức" để đọc khi muốn hiểu sâu.
